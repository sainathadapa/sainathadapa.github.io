---
layout: post
title: "Loading Amazon review data into PostgreSQL"
description: ""
tag:
  - sql
---

A large data set containing 140 million amazon reviews and associated metadata is available at the [Julian McAuley's website](http://jmcauley.ucsd.edu/data/amazon/links.html). There is a wealth of information in here and so can be used for general data analysis as well as for machine learning experimentation. As the dataset is large, it makes sense to load the data into a database (in this case, PostgreSQL) for faster and easier analysis of data. This is a code dump post listing the series of commands that I used to the load the data into the database. 

Download the following two files:
- `kcore_5.json.gz`: This file contains the review information - review text, time, reviewer name, etc.
- `metadata.json.gz`: This file contains the metadata information for a review - product name, price, category, etc.

The JSON files from the site are not valid JSON. Hence it is better to preprocess the data and save them in the standard JSON format. The following short python snippet does exactly that.

~~~ python
import json
def parse(path):
  g = open(path, 'r')
  for l in g:
    yield json.dumps(eval(l), allow_nan=False, ensure_ascii=True)

f = open("kcore_5_strict.json", 'w')
for l in parse("kcore_5.json"):
  f.write(l + '\n')

f = open("metadata_strict.json", 'w')
for l in parse("metadata.json"):
  f.write(l + '\n')
~~~

Create 2 single column tables with the column type being `text`.
~~~ sql
create table meta_json (values text);
create table reviews_json (values text);
~~~

Load the data from the json files into these tables. As there are backslashes in the data, they need to escaped. Each row in this table now contains one json record.
~~~ sql
copy meta_json from program 'sed -e ''s/\\/\\\\/g'' /home/ubu/metadata_strict.json';
copy reviews_json from program 'sed -e ''s/\\/\\\\/g'' /home/ubu/kcore_5_strict.json';
~~~

Convert the text data into PostgreSQL's jsonb column type. As the review data contains the `\u0000` unicode character, which is not valid in PSQL, it needs to be replaced with a blank character.
~~~ sql
alter table meta_json alter column values type jsonb using values::JSON;
alter table reviews_json alter column values type jsonb using regexp_replace(values, '\\u0000', '', 'g')::JSON;
~~~

Create tables that will hold the data in a structured format.
~~~ sql
create table meta (
  id serial primary key,
  asin text,
  price numeric,
  title text,
  also_viewed jsonb,
  buy_after_viewing jsonb,
  salesRank jsonb,
  categories jsonb,
  description text
);

create table reviews (
  id serial primary key,
  asin text,
  helpful_true integer,
  helpful_all integer,
  overall numeric,
  summary text,
  reviewText text,
  reviewTime text,
  reviewerID text,
  reviewerName text,
  unixReviewTime text
);
~~~

Move the data from the single column jsonb tables into these new tables. Note the usage of `->` vs `->>`. `->` returns a jsonb value, whereas `->>` returns a string.
~~~ sql
Insert into meta (asin, price, title, also_viewed, buy_after_viewing, salesRank, categories, description)
select
  values->>'asin' as asin,
  (values->>'price')::numeric as price,
  values->>'title' as title,
  values->'related'->'also_viewed' as also_viewed,
  values->'related'->'buy_after_viewing' as buy_after_viewing,
  values->'salesRank' as salesRank,
  values->'categories'->0 as categories,
  values->>'description' as description
from meta_json;

Insert into reviews (asin, helpful_true, helpful_all, overall, summary, reviewText, reviewTime, reviewerID, reviewerName, unixReviewTime)
select
  values->>'asin' as asin,
  (values->'helpful'->>0)::integer as helpful_true,
  (values->'helpful'->>1)::integer as helpful_all,
  (values->>'overall')::numeric as overall,
  values->>'summary' as summary,
  values->>'reviewText' as reviewText,
  values->>'reviewTime' as reviewTime,
  values->>'reviewerID' as reviewerID,
  values->>'reviewerName' as reviewerName,
  values->>'unixReviewTime' as unixReviewTime
from reviews_json;
~~~

Add indexes for faster joins.
~~~ sql
CREATE INDEX ON reviews (asin);
CREATE INDEX ON meta (asin);
~~~

Explore!
~~~ sql
select meta.categories->>0 as category1, count(*) from reviews join meta on reviews.asin = meta.asin group by meta.categories->>0 limit 10;
~~~
```
      category1       | count
----------------------+--------
                      | 158408
 #508510              |     17
 All Beauty           |  14650
 All Credit Cards     |   4100
 All Electronics      |  33089
 Alternative Rock     |   1565
 Amazon Coins         |    643
 Amazon Fashion       |  30876
 Amazon Fire TV       |   4574
 Amazon Instant Video | 317234
```

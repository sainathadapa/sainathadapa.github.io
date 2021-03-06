---
layout: post
title: "Introducing stubthat"
description: "A Stubbing framework for R"
tag:
  - rstats
  - unittest
---

[**stubthat**](https://github.com/sainathadapa/stubthat) is a new R package written by me and [Nitin Madasu](https://github.com/nitinmdsu). This package provides stubs for use while unit testing in R. The API is highly inspired by the [Sinon.js](http://sinonjs.org/).

This package is meant to be used along with the [testthat](https://cran.r-project.org/package=testthat) package, specifically the 'with\_mock' function. Please note that although this package was written with an intention to be used alongside testthat, this package doesn't depend on testthat or any other package.

To understand what a stub is and how they are used while unit testing, please take a look at this Stackoverflow question [What is a “Stub”?](http://stackoverflow.com/questions/463278/what-is-a-stub).

Usage
=====

There are three main steps for creating a stub of a function -

-   Invoke the *stub* function with the function that needs to be mocked

~~~ R
jedi_or_sith <- function(x) return('No one')
jedi_or_sith_stub <- stub(jedi_or_sith)
~~~

-   Define the behavior. This is explained in detail in the next section.

~~~ R
jedi_or_sith_stub$withArgs(x = 'Luke')$returns('Jedi')
~~~

-   Build the stub.

~~~ R
jedi_or_sith_stub <- jedi_or_sith_stub$build()
~~~

Once the stub is built, you can use the returned function.

~~~ R
jedi_or_sith('Luke')
#> [1] "No one"
jedi_or_sith_stub('Luke')
#> [1] "Jedi"
~~~

Stubs are generally used while testing. Here is an example:

~~~ R
library('httr')

check_api_endpoint_status <- function(url) {
  response <- GET(url)
  response_status <- status_code(response)
  ifelse(response_status == 200, 'up', 'down')
}
~~~

This function *check\_api\_endpoint\_status* should make a *GET* request to the specified url and it should return *'up'* if the status code is *'200'*. Return *'down'* otherwise.

Using stubs, without accessing any external source, the function can be tested as shown below:

~~~ R
stub_of_get <- stub(GET)
stub_of_get$withArgs(url = 'good url')$returns('good response')
stub_of_get$withArgs(url = 'bad url')$returns('bad response')
stub_of_get <- stub_of_get$build()

stub_of_status_code <- stub(status_code)
stub_of_status_code$withArgs(x = 'good response')$returns(200)
stub_of_status_code$withArgs(x = 'bad response')$returns(400)
stub_of_status_code <- stub_of_status_code$build()

library('testthat')
with_mock(GET = stub_of_get, status_code = stub_of_status_code,
          expect_equal(check_api_endpoint_status('good url'), 'up'))
#> As expected: check_api_endpoint_status("good url") equals "up"

with_mock(GET = stub_of_get, status_code = stub_of_status_code,
          expect_equal(check_api_endpoint_status('bad url'), 'down'))
#> As expected: check_api_endpoint_status("bad url") equals "down"
~~~

Behaviors
=========

withExactArgs
-------------

~~~ R
stub$withExactArgs(a = 1, b = 2, d = 3, c = 4)$returns(10)
~~~

If the function is called with the **exact** set of expected arguments, then the specified object will be returned.

~~~ R
stub$withExactArgs(a = 1, b = 2, d = 3, c = 4)$throws('err_msg')
~~~

If the function is called with the **exact** set of expected arguments, then an error is thrown with the specified message.

with Args
---------

~~~ R
stub$withArgs(a = 1, d = 3)$returns(10)
~~~

If the expected arguments are **part** of the function call, then the specified object will be returned.

~~~ R
stub$withArgs(a = 1, d = 3)$throws('err msg')
~~~

If the expected arguments are **part** of the function call, then an error is thrown with the specified message.

onCall
------

~~~ R
stub$onCall(2)$returns(10)
~~~

When the function is called the nth time, the specified object will be returned.

~~~ R
stub$onCall(2)$throws('err_msg')
~~~

When the function is called the nth time, an error is thrown with the specified message.

*onCall* can be used along with *withExactArgs* and *withArgs*.

~~~ R
stub$onCall(3)$withExactArgs(a = 1, b = 2, d = 3, c = 4)$returns(10)
stub$onCall(2)$withExactArgs(a = 1, b = 2, d = 3, c = 4)$throws('err_msg')
stub$onCall(3)$withArgs(a = 1, d = 3)$returns(10)
stub$onCall(3)$withArgs(a = 1, d = 3)$throws('err msg')
~~~

Defaults
--------

~~~ R
stub$returns(data.frame(x = 1, y = 2))
~~~

If no other expectation was defined or matched, the object specified in the above statement is returned.

~~~ R
stub$throws('there is an error')
~~~

If no other expectation was defined or matched, an error is thrown with the specified message.

~~~ R
stub$expects(a = 1, b = 2, d = 3, c = 4)
~~~

Stub will always check the incoming arguments for the specified set of arguments. Throws an error if there is a mismatch.

Notes
=====

-   All arguments must be named, when using *withArgs* or *withExactArgs* `stub_builder$withArgs(1)$return(T)` won't work. `stub_builder$withArgs(x = 1)$return(T)` will work.

-   Multiple expectations can be defined. Different types of expectations can be used with the same stub.

~~~ R
stub$withExactArgs(a = 1, b = 2, d = 3, c = 4)$returns(10)
stub$withExactArgs(a = 5, b = 6, d = 7, c = 8)$throws('err')
stub$onCall(2)$returns(2)
stub$throws('no expectation matched')
~~~

_Edit (2016-03-06): stubthat was featured as the 'Package Pick' in the [15th episode of the R-Podcast](https://www.r-podcast.org/posts/the-r-podcast-episode-15-introduction-to-shiny.html). Thanks guys!_

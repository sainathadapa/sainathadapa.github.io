---
layout: post
title: "Export a reddit thread to epub/mobi"
description: "long reddit thread (AMAs) -> html -> mobi"
tag:
  - reddit
  - nodejs
---

I needed a script to export long reddit threads (like AMAs) to an ebook so that I can read it on my kindle. I searched for such utility online and found nothing, so I wrote one.

[_Calibre_, a ebook reader software](http://calibre-ebook.com) has an utility named [_ebook-convert_](http://manual.calibre-ebook.com/cli/ebook-convert.html), which can convert to/from various ebook formats like epub, mobi, and html. 

My script (written for _nodejs_) uses the reddit API to export a thread into a simple html with nested posts and no special formatting. This can then be converted into ebook format of choice using _ebook-convert_.

## How to use
1. Install [NodeJS](http://nodejs.org/) and [npm](https://www.npmjs.com/)
2. Clone the [sainathadapa/reddit2mobi](https://github.com/sainathadapa/reddit2mobi) repo
3. `cd reddit2mobi; npm install`
4. Run _run_reddit2html.js_ script. 
	- Pass the url of the reddit post as an argument. Optionally, pass the depth (integer) to limit the maximum depth of subtrees in the thread.
  - Usage: `nodejs run_reddit2html.js url depth > out.html`
5. Install [Calibre](http://calibre-ebook.com/download)
6. Convert the generated html into epub/mobi using the _ebook-convert_ from Calibre.
  - Usage: `ebook-convert in.html out.mobi`

  Sample outputs are available in the [github repo](https://github.com/sainathadapa/reddit2mobi)

  Note: Since I wrote the script, [reddit2kindle](https://reddit2kindle.com/) came up, which does this in an easy and a better way.

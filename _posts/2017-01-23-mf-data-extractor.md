---
layout: post
title: "MF Statement data extractor"
description: "Script to extract data from the Consolidated Mutual Fund statement given by CAMS"
tag:
  - rstats
  - finance
---

CAMS provides a [service](https://www.camsonline.com/InvestorServices/COL_ISAccountStatementCKF.aspx) to get a pdf statement with all the mutual transactions within a specified period, from most of the fund houses. I needed a way to extract the data from the pdf, so that I can compute metrics on the data. Using the [tabulizer](https://github.com/ropensci/tabulizer) package, I was able to extract the data. The script and instructions to run it are given at the [repo](https://github.com/sainathadapa/mf-statement-data-extractor). Feel free to create an issue on the github, if you face any problems while running the script.

_Update: I abandoned the above project. [This code](https://github.com/sainathadapa/personalFinanceR/blob/master/R/cams-stmnt-extracter.R) might be useful to anyone who wants to do something similar._

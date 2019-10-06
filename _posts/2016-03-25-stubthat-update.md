---
layout: post
title: "Package update: stubthat v1.0.0"
description: "Changelog and the new API of stubthat"
tag:
  - rstats
  - unittest
---

A new version of [stubthat](https://github.com/sainathadapa/stubthat), v1.0.0, is on CRAN. Please note that this is a breaking release.

Changes from the previous version
=================================
- `stub$onCall(#)$withArgs(...)` is now `stub$onCall(#)$expects(...)`. Previously the stub didn't throw an error if the specified arguments are not present on the nth call. Now it does.
- `stub$onCall(#)$withExactArgs(...)` is now `stub$onCall(#)$strictlyExpects(...)`. Similar change in functionality as above. The stub now throws an error if any specified argument is found to be missing or if there is a mismatch in values.
- `stub$expects(...)` in the previous version used to check for the exact set of arguments. In the latest version, it checks if the expected arguments are **part** of the function call (**not exact** set).
- `stub$strictlyExpects(...)` will check for the exact set of specified arguments. No specied argument should be missing. And no unspecified argument should be present in the function call.
- `stub$calledTimes()` can be used to get the number of times the stub was called.
- No need for `stub$build()` step anymore. Mock is directly available from `stub$f`

The new API
===========
-   Check if the stub is called with specified arguments
    -   `stub$expects(...)`
    -   `stub$strictlyExpects(...)`
    -   `stub$onCall(#)$expects(...)`
    -   `stub$onCall(#)$strictlyExpects(...)`
-   Make the stub return a specified value
    -   `stub$returns(...)`
    -   `stub$onCall(#)$returns(...)`
    -   `stub$withArgs(...)$returns(...)`
    -   `stub$withExactArgs(...)$returns(...)`
-   Make the stub throw an error with a specified message
    -   `stub$throws('')`
    -   `stub$onCall(#)$throws('')`
    -   `stub$withArgs(...)$throws('')`
    -   `stub$withExactArgs(...)$throws('')`
-   Get the number of times the stub has been called
    -   `stub$calledTimes()`
-   Extra
    -   `stub$onCall(#)$expects(...)$returns(...)`
    -   `stub$onCall(#)$strictlyExpects(...)$returns(...)`
    -   `stub$onCall(#)$expects(...)$throws('')`
    -   `stub$onCall(#)$strictlyExpects(...)$throws('')`

Please go through [README](https://github.com/sainathadapa/stubthat/blob/master/README.md) for detailed API description & examples, instructions for installing the package and other details.

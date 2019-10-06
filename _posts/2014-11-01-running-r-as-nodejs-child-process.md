---
layout: post
title: "Running R as a child process in NodeJS"
description: "A fun little script that runs R as a child process in NodeJS"
tag:
  - nodejs
  - rstats
---

A fun little script that runs R as a child process in NodeJS.

~~~ javascript
var child_process = require('child_process');
var r_comm = 'R';
var rspawn = child_process.spawn(r_comm,['--vanilla','--slave']);

rspawn.stdout.on('data', function (data) {
  console.log('STDOUT: \n');
  console.log(data.toString());
});

rspawn.stderr.on('data', function (data) {
  console.log('STDERR: \n');
  console.log(data.toString());
});

rspawn.on('close', function (code) {
  console.log('child process exited with code ' + code);
});

var stdin = process.openStdin();

stdin.addListener("data", function(data) {
  rspawn.stdin.write(data.toString());
});
~~~

Sample input & output when the script is run:

~~~ bash
bash> nodejs running_R.js 
head(cars,1) # console input
STDOUT: 

  speed dist
1     4    2

warning('this is a test') # console input
STDERR: 

Warning message:
this is a test 

q() # console input
child process exited with code 0
bash>
~~~


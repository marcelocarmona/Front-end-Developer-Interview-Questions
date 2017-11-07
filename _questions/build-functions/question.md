---
title: Build functions
layout: question
permalink: build-functions
tags: intermediate Closure IIFE es6-let
---

### We're building a function that return an array of functions

The idea is to see why the ejecution of `fns[0]()`, `fns[1]()`, `fns[2]()` is not 1,2,3 and how we can do to resolve it.

```javascript
function buildFunctions() {
  var arr = [];
  for (var i = 0; i < 3; i++) {
    arr.push(
      function() {
        console.log(i)
      }
    )
  }
  return arr;
}

var fns = buildFunctions()

fns[0]();
fns[1]();
fns[2]();
```

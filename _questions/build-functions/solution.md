---
---

### 1) ES6 - let

let allows you to declare variables that are limited in scope to the block, statement, or expression on which it is used. This is unlike the var keyword, which defines a variable globally, or locally to an entire function regardless of block scope.

```javascript
function buildFunctions() {
  var arr = [];
  for (let i = 0; i < 3; i++) {
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

### 2) Closure - IIFE

With a closure we it's possible to create a new execution context that allow us to maintain the value of i for each ejecution context

```javascript
function buildFunctions() {
  var arr = [];
  for (var i = 0; i < 3; i++) {
    arr.push(
      (function(j) {
        return function() {
          console.log(j)
        } 
      })(i)
    )
  }
  return arr;
}

var fns = buildFunctions()

fns[0]();
fns[1]();
fns[2]();
```

---
title: Emulate block scope
layout: question
permalink: emulate-block-scope
tags: intermediate
---

### Emulating Block Scope in JavaScript
While there are many issues that trip up developers coming from other languages, variable scoping may be number one. The fundamental problem is that many expect variables to be scoped to a particular block (like a for loop), but in JavaScript variables declared with var are scoped to the nearest parent function.

First let's take a look at how this can go wrong.

```javascript
var avatar = "Ang";
var element = "Air";

var elements = [
    "Air",
    "Earth",
    "Fire",
    "Water"
];

for (var i = 0; i < elements.length; i++) {
    var element = elements[i];
    console.log(avatar + " has mastered " + element);
}

// Outputs: "Ang's primary element is Water"
console.log(avatar + "'s primary element is " + element);
```

---
title: Js scope
layout: question
permalink: js-scope
tags: intermediate hoisting
---

### If we execute this Javascript, what will the browser's console show?

```javascript
var text = 'outside';
function logIt(){
    console.log(text);
    var text = 'inside';
};
logIt();
```

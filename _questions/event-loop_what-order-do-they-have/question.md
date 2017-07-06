---
title: Event Loop - What order do they have
layout: question
---


### In what order will the numbers 1-4 be logged to the console when the code below is executed? Why?

```javascript
(function() {
    console.log(1); 
    setTimeout(function(){console.log(2)}, 1000); 
    setTimeout(function(){console.log(3)}, 0); 
    console.log(4);
})();
```

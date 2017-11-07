---
title: Simple bubbling
layout: question
permalink: simple-bubbling
tags: intermediate bubbling-event
---

### What happend if I click in the p element?
How I can cancel the events?

```html
<style>
  body * {
    margin: 10px;
    border: 1px solid blue;
  }
</style>

<form onclick="alert('form')">FORM
  <div onclick="alert('div')">DIV
    <p onclick="alert('p')">P</p>
  </div>
</form>
```

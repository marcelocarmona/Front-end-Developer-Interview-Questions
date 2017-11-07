---
---

### Solution 1

```html
<style>
  body * {
    margin: 10px;
    border: 1px solid blue;
  }
</style>

<form onclick="toAlert('form')">FORM
  <div onclick="toAlert('div')">DIV
    <p onclick="toAlert('p')">P</p>
  </div>
</form>

<script>
  function toAlert(event ,msg) {
    console.log(msg)
    event.stopPropagation()
  }
</script>
```

### Solution 2

```html
<style>
  body * {
    margin: 10px;
    border: 1px solid blue;
  }
</style>

<form onclick="alert('form');event.stopPropagation()">FORM
  <div onclick="alert('div');event.stopPropagation()">DIV
    <p onclick="alert('p');event.stopPropagation()">P</p>
  </div>
</form>
```

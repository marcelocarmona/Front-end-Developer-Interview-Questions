---
---

We can solve this by wrapping our anonymous function in another anonymous function that takes btnNum as an argument. Like so:

```html
<button id="btn-0">Button 1!</button>
<button id="btn-1">Button 2!</button>
<button id="btn-2">Button 3!</button>

<script type="text/javascript">
    var prizes = ['A Unicorn!', 'A Hug!', 'Fresh Laundry!'];
    for (var btnNum = 0; btnNum < prizes.length; btnNum++) {
        // for each of our buttons, when the user clicks it...
        document.getElementById('btn-' + btnNum).onclick = function(frozenBtnNum){
            return function() {
                // tell her what she's won!
                alert(prizes[frozenBtnNum]);
            };
        }(btnNum); // LOOK! We're passing btnNum to our anonymous function here!
    }
</script>
```

This "freezes" the value of btnNum. Why? Well...

So when we pass btnNum to the outer anonymous function as its one argument, we create a new number inside the outer anonymous function called frozenBtnNum that has the value that btnNum had at that moment (0, 1, or 2).

Our inner anonymous function is still a closure because it still reaches outside its scope, but now it closes over this new number called frozenBtnNum, whose value will not change as we iterate through our for loop.

<b>What We Learned</b>

Like several common interview questions, this question hinges on a solid understanding of closures and pass by reference vs pass by value. If you're shaky on either of those, look back at the examples in the solution.

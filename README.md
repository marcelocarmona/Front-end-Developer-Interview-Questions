### If we execute this Javascript, what will the browser's console show?

```javascript
var text = 'outside';
function logIt(){
    console.log(text);
    var text = 'inside';
};
logIt();
```

### In order to win the prize for most cookies sold, my friend Alice and I are going to merge our Girl Scout Cookies orders and enter as one unit.
Each order is represented by an "order id" (an integer).

We have our lists of orders sorted numerically already, in arrays. Write a function to merge our arrays of orders into one sorted array.

For example:
```javascript
var myArray     = [3, 4, 6, 10, 11, 15];
var alicesArray = [1, 5, 8, 12, 14, 19];

console.log(mergeArrays(myArray, alicesArray));
// logs [1, 3, 4, 5, 6, 8, 10, 11, 12, 14, 15, 19]
```

### We're building a web game where everybody wins and we are all friends forever.
It's simple—you click on one of three boxes to see what nice thing you've won. You always win something nice. Because we love you.

Here's what we have so far. Something's going wrong though. Can you tell what it is?

```html
<button id="btn-0">Button 1!</button>
<button id="btn-1">Button 2!</button>
<button id="btn-2">Button 3!</button>

<script type="text/javascript">
    var prizes = ['A Unicorn!', 'A Hug!', 'Fresh Laundry!'];
    for (var btnNum = 0; btnNum < prizes.length; btnNum++) {
        // for each of our buttons, when the user clicks it...
        document.getElementById('btn-' + btnNum).onclick = function() {
            // tell her what she's won!
            alert(prizes[btnNum]);
        };
    }
</script>
```
The Solution

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

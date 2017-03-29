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

A developer used to a language with block scoping might not see anything wrong with the code above, and would expect "Ang's primary element is Air" instead of the actual result.

This issue is easily avoided once you become aware of it. Avoiding variable declarations within blocks tends to prevent any confusion.

But suppose that we really wanted to use block scoping in JavaScript. How would we go about it? We could do something like this.

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
    (function() {
        var element = elements[i];
        console.log(avatar + " has mastered " + element);
    })();
}

// Outputs: "Ang's primary element is Air"
console.log(avatar + "'s primary element is " + element);
```

This solution uses an IIFE to emulate block scoping. Since functions are JavaScript's scoping mechanism, we define and immediately invoke a new function on each pass through the loop, therefore approximating the behavior of a block scope.

While this isn't idiomatic JavaScript, it does help give you an idea of just how flexible JavaScript can be.

It is also worth noting that drafts of the ECMAScript 6 specification (the next version of JavaScript) include a let keyword which is used to define block-scoped variables. If you are interested in playing around with this proposed keyword, it is available in FireFox.

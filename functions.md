## Learning Objectives

* Define a JS function
  * that accepts input arguments
  * that returns a value
* Differentiate between referencing function and calling a function
* Define DRY, and why DRY is good
* Define variable scope
* Explain how variable scope works in JavaScript

## Outline

### Intro

* Frame the day, set expectations
* input-output-sideEffect
* Speaking generally, every expression in programming has some input, produces some side-effect, and returns some value

```js
1 + 2

3 * 5

(3 + 4) * 5

const a = 10;
const b = 20;
const c = a + b;

const colors = ["indianred", "cadetblue", "whitesmoke"];
colors.pop();
```

* Let's look at some examples of this that we've already used.

```js
alert("Hi there!");
```

```js
const username = prompt("What is your name?");
```

* Explain the substitution that is going on here.
* Use this super example

```js
const message = prompt("What greeting?") + " " + prompt("To whom?");
```

**I do**

* A function is a chunk of code we define, that we can execute multiple times in our program.
* I write a function to add combine two strings with a space and return the result

```js
function combineWords(firstWord, secondWord) {
  const combination = firstWord + ' ' + secondWord;
  return combination;
};
```

**You do**

* Write a function `sumOfThree` that will accept three numbers as input
  arguments, and return their sum
* Write a function `productOfThree` that will accept three numbers as input arguments, and return their product

```js
function sumOfThree(a, b, c) {
  return a + b + c;
};
```

```js
function productOfThree(a, b, c) {
  return a * b * c;
};
```

**I do**

### DRY

* What is DRY? Why is DRY good?
* Functions can greatly DRY up your code. If you see repeated sections of code in your program, see if a function can help

```js
var myScores = [3, 4, 2, 2, 1, 4, 2];
var jimbobsScores = [5, 1, 2, 1, 1, 4, 3];
var flandersScores = [2, 2, 1, 1, 2, 1, 2];

var sum = 0;
for (var i = 0; i < myScores.length; i++) {
  sum += myScores[i];
}
var myTotal = sum;

sum = 0;
for (var i = 0; i < jimbobsScores.length; i++) {
  sum += jimbobsScores[i];
}
var jimbobsTotal = sum;

sum = 0;
for (var i = 0; i < flandersScores.length; i++) {
  sum += flandersScores[i];
}
var flandersTotal = sum;

console.log(myTotal);
console.log(jimbobsTotal);
console.log(flandersTotal);

// ----------------
// OR
// ----------------

var myScores = [3, 4, 2, 2, 1, 4, 2];
var jimbobsScores = [5, 1, 2, 1, 1, 4, 3];
var flandersScores = [2, 2, 1, 1, 2, 1, 2];

function total(arr) {
  const sum = 0;
  for (let i = 0; i < arr.length; i++) {
    sum += arr[i];
  }
  return sum;
};

var myTotal = total(myScores);
var jimbobsTotal = total(jimbobsScores);
var flandersTotal = total(flandersScores);

console.log(myTotal);
console.log(jimbobsTotal);
console.log(flandersTotal);
```

* Now let's DRY up Timmy's laps code

```js
const thisWeekTimes = [52, 51, 53, 52, 54];
const lastWeekTimes = [54, 57, 58, 53, 54, 58];
const weekBeforeTimes = [100, 102, 142, 133, 123, 141, 120];

const sum = 0;
for (let i = 0; i < thisWeekTimes.length; i++) {
  sum += thisWeekTimes[i];
}
const thisWeekAvg = sum / thisWeekTimes.length;

const sum = 0;
for (let i = 0; i < lastWeekTimes.length; i++) {
  sum += lastWeekTimes[i];
}
const lastWeekAvg = sum / lastWeekTimes.length;

const sum = 0;
for (let i = 0; i < weekBeforeTimes.length; i++) {
  sum += weekBeforeTimes[i];
}
const weekBeforeAvg = sum / weekBeforeTimes.length;

console.log(thisWeekAvg);
console.log(lastWeekAvg);
console.log(weekBeforeAvg);
```

**BREAK**

### Arguments

* What happens if we supply the wrong number of arguments when we call a
  function?

```js
function showMeYourArguments(arg1, arg2) {
  console.log("First argument: " + arg1);
  console.log("Second argument: " + arg2);
};
```

* Call this function with less than two arguments
* Call this function with more than two arguments

### OUTPUT && SIDE EFFECT

* Use examples below to demonstrate output vs side effect

```js
// Define the `zen` function
function zen() {
  const meaningOfLife = 42;
  console.log('The meaning of life is ' + meaningOfLife);
};

// Call the `zen` function
const resultOfZen = zen();

// Attempt to print `meaningOfLife`
console.log(resultOfZen); // undefined
```
* Common side effects include
    * Logging to the console
    * Writing to the screen
    * Writing to a file
    * Writing to the network
    * Triggering any external process
    * Calling any other functions with side-effects

### Scope

* Pitfalls of accidental global variables!
  * Remove the `var` to demonstrate that this works now
  * Explain why this is **BAD**

```js

function total(arr) {
  const sum = 0;
  for (let i = 0; i < arr.length; i++) {
    sum += arr[i];
  }
  return sum;
};

function globalBad() {
  total = "WHatttttt"
}

```

We can either add a `var`, `let`, or `const` in front of total to block scope this variable.

### You Do

How do we fix this???

Take a minute and figure out how to not pollute the global namespace

### I Do

Insteresting Gothca

```js
var hello = "Hello"
var x = true

if(x) {
  var hello = "????"
} else {
  var hello = "!!!!"
}
```

### You do

How do we fix this???

Take a minute and figure out how to not pollute the global namespace

### Exercises

### Javascript Functions Modeled for you

* Write a function called `sayHello` that console logs "Hello."

```js
sayHello();
```

* Write a function called `sayHelloTo` that accepts one input argument (string)
  called `name` and returns a hello message to that name

```js
sayHelloTo("JimBob"); // This should return "Hello, JimBob."
```

* Write a function called `bigOrSmall` that accepts one argument, a number, and returns "This number is big" if the number is greater than 10, and "This number is small" otherwise

* Write a function called `oddOrEven` that accepts one argument, a number, and returns "This number is odd" if the number is odd, and "This number is even" if the number is even

* Write a function called `embiggen` that accepts one argument, a string, and returns a CAPS LOCKED version of the string with an exclamation at the end

* Write a function called `reverser` that accepts one argument, a string, and returns a reversed version of the string

### Problem Modeling

### Pounds to Kilograms

How would you convert 120lbs to kilograms?

### Kilograms to Pounds

How would you convert 80 kilograms to pounds?

### Killer Caffeine

It's estimated that 6 grams per hundred pounds of body weight can cause death! Given an 8oz cup of coffee has 95mg of caffeine,
calculate how many cups it takes to kill YOU.


### Old Modems

How long would it take to download a 25GB ripped copy of Blade Runner over a $200 56k/s modem from 1995?

### A Long Long Long time

If you drove from Portland to Portland at a steady 55 miles per hour, how many
times could you listen to the Beatle's White Album in full?


### How much would it cost to drive around the world at the equator?
Assuming gas costs $2.675 and you drive at a steady 55 mph.

<img src="./Illustrations/JsRefresher.gif" />

## Adding Js to a html file
* Js can be added to a html file using <script> tags(cumbersome unless script is small), by writing js code directly in the tags or linking a js file using the tag(more maintainable).
* Script tags are not self closing and we need both opening and closing tags.
* These tags have an src attribute that we pass the path the js script to.
* We can pass a defer keyword in the tag to make sure the script is executed after the html has finished loading, to ensure the necessary elements needed for the script to run have been loaded.
* Alternatively we can put the script tags at the end of the html document.
* This tag also has a type attribute which gets passed "module" argument, instead of using defer, and this treats our imported scripts as a js module instead of a js script, giving us the benefit of adding imports and exports in out scripts.
```html
<!DOCTYPE html>
<html>
  <head>
    <title>JavaScript Refresher</title>
    <link rel="stylesheet" href="assets/styles/main.css" />
    <meta charset="UTF-8" />
    <!-- <script src="./scripts/app.js" defer></script> -->
    <script src="./scripts/app.js" type="module"></script>
  </head>
  <body>
    Some content
  </body>
</html>
```
* React uses a build process which injects scripts into our html code. This means that the code we write is not the code that is run directly, its transformed and then handed off to the browser. Libraries such as react-scripts add the script tags into our html code for us.
* Build process not only makes the jsx code we write in react execute in the browser, it also optimizes the code for production(minification).


## import and export
* Make sure to add type attribute set to "module" in the html file.
* We can export stuff from a file using named exports or default export.
* Name exports need to be declared and defined but default export are exported directly.
* Named exports are destructured and imported, default imports are imported directly.

util.js
```js
export let x = "export 1 named x";
export let y = "export 2 named y";
export default "default export";
```

app.js
```js
import string, { x, y } from "./util.js";
console.log(x, y, string);
console.log("finished");
```

* We can also import everything as an object and access the imports from it. Default export is available under default field.

app.js
```js
import * as vars from "./util.js";
console.log(vars.x, vars.y, vars.default);
console.log("finished");
```

## Values and variables and constants

* There are different types of values such as strings, numbers, boolean, null and undefined and also an object value.
* Variable store values, has name of your choice, have reusability and readability.
* Variables created using **let** keyword and must follow some rules
  * No white space or special characters.
  * May contain a number but not at the start.
  * Must not clash with reserved keywords.
  * Should use camel casing, eg. userName, isCorrect.
  * Should identify the thing it contains.
* Constants are created using the const keyword and follow the naming conventions of the varibales as well.
* The difference between cariables and constants is that constants cannot be reassigned.

app.js
```js
let userName="Abhishek";
console.log(userName);
const dataPoint="xyz1Abc2";
console.log(dataPoint);
// dataPoint="abcd1xyz2"; //throws error
```

## Operators

* **+,-,*,/** can be used for math operations. **+** opearator is also used for string concatenations. Other comaparison operations include **<,>,<=,>=** etc.
* **===** operator is used to check for equality without type coersion, whereas **==** compares values with type coersion. Both yeild boolean value.

```js
let a = 10;
let b = "10";
console.log(a == b); //true
console.log(a === b); //false
```

## Functions

* A code block being executed when being called and as often being called helps in modularity decreases repetition.
* It can be created using the function keyword or the arrow function syntax, the arrow fucntion syntax being the more modern way to do it.
* The function must have a name, may have list of parameters that need to defined before being passed.
* Functions can also have default parameters that can be set using an equal sign in the function defintion. This is the value which will be used if no argument is passed for this parameter.
* Functions can return values, objects, arrays, etc. and are returned using the return keyword.
* Crucial React features include components that are basically arrow functions(can also be class based components but thats on  its way out).

Example of different functions with function keyword and arrow syntax.

app.js
```js
function func(a, b) {
  // do stuff
  return a * b;
}
function func1(a, b = 2) {
  // do stuff
  return a * b;
}
const func2 = (b, a = 1) => {
  // do stuff
  return a * b;
};
//We can omit the curly braces and return statement.
const func3 = (a = 1, b = 2) => a * b;

//If only one parameter is there we can omit the parantheses
// in the definition.
const func4 = (a) => a * 2;

//We must be careful while returning
// objects in the short return syntax.
//This throws an error
//const func5 = (a, b) => { name: a, age: b };

//This is the correct way to return objects
const func5 = (a, b) => ({ name: a, age: b });

console.log(func(1, 2)); //2
console.log(func1(2, 3)); //4
console.log(func2(4)); //6
console.log(func3()); //4
console.log(func4(53)); //106
console.log(func5("Hillary", 69)); //{name: 'Hillary', age: 69}
```

## Objects and Classes

* Objects are a collection that can contains value and functions. The values in the object are called as properties and the functions in the object is called as methods.
* The properties of the object can be accessed in the methods using the **this** keyword.
* Object can be created directly or from a blueprint.

Examples of objects are as follows

```js
//We can create objects directly as so
const obj = {
  name: "SleepyDev",
  age: 23,
  // we make methods as shown below
  greet() {
    console.log(this.name + " says Hi! ");
  },
  sayAge() {
    console.log("I am " + this.age + " years of age");
  },
};
obj.greet(); //SleepyDev says Hi!
obj.sayAge(); //I am 23 years of age

//Class blueprint can be defined as so
class Obj {
  //class needs a constructor to be instanciated
  constructor(name, age) {
    this.name = name;
    this.age = age;
  }
  greet() {
    console.log(this.name + " says Hi! ");
  }
  sayAge() {
    console.log("I am " + this.age + " years of age");
  }
}
// objects from blueprints
//can be instantiated using new keyword
const newDev = new Obj("AngryDev", 24);

newDev.greet(); //AngryDev says Hi!
newDev.sayAge(); //I am 24 years of age
```

## Arrays and Array methods

* Arrays are meant to store data(values, arrays, objects, etc) in a serialised format.
* We can access array element using indexing,slicing, etc.
* Some frequently used array methods in JavaScript are:
  1. `push()`: Adds one or more elements to the end of an array and returns the new length of the array.
  2. `pop()`: Removes the last element from an array and returns that element.
  3. `shift()`: Removes the first element from an array and returns that element.
  4. `unshift()`: Adds one or more elements to the beginning of an array and returns the new length of the array.
  5. `splice()`: Changes the contents of an array by removing or replacing existing elements and/or adding new elements in place.
  6. `slice()`: Returns a shallow copy of a portion of an array into a new array.
  7. `concat()`: Combines two or more arrays.
  8. `forEach()`: Executes a provided function once for each array element.
  9. `map()`: Creates a new array populated with the results of calling a provided function on every element in the calling array.
  10. `filter()`: Creates a new array with all elements that pass the test implemented by the provided function.
  11. `find()`: Returns the first element in the array that satisfies the provided testing function.
  12. `indexOf()`: Returns the first index at which a given element can be found in the array, or -1 if it is not present.
  13. `includes()`: Determines whether an array includes a certain value among its entries, returning true or false as appropriate.
  14. `some()`: Checks if at least one element in the array passes the test implemented by the provided function.
  15. `every()`: Checks if all elements in the array pass the test implemented by the provided function.

  These are just a few commonly used array methods in JavaScript.
  Descriptive information on each of the functions, their usage and other functions can be found [here](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array).
  Many of these functions take different values or anonymous functions as arguments to do opearations on the array.

## Destructuring and spreading

* We can destructure arrays and objects to pull values faster.
* Arrays are destructured by index and hence we can give any name to the destructured variables, but since objects are destructured by keys, we need to destructure using key names. We can assign aliases to them later tho.

```js
//Array destructuring
let [firstName, lastName] = ["Alex", "Reagan"];
console.log(firstName, lastName); //Alex Reagan

//Object destructuring
let { fName, lName } = { fName: "Richard", lName: "Strand" };
console.log(fName, lName); //Richard Strand

//Object destructuring with alias
let { fName: pfname, lName: plname } = {
  fName: "Paul",
  lName: "Montgomery",
};
console.log(pfname, plname); //Paul Montgomery

//We can also use destructuring in function parameters
const func = ({ name, age }) =>
  "Hi! My name is " + name + " and my ages is " + age + " years";
console.log(func({ name: "SleepyDev", age: 23 }));
//Hi! My name is SleepyDev and my age is 23 years
```

* We can spread array and object contents using the spread operator.
* A thing to note for the array spreading is that new array elements will follow the order in which they are spread.
* Also object spreading is that, if there is a conflict of key names, the key will have value based on the order in which the spread operation was done.

```js
let dune = ["Paul", "Chani", "Leto"];
let semetary = ["Gage", "Jud", "Louis"];
//Array elements follow order in which they are spread 
let mix = [...dune, ...semetary];
//["Paul", "Chani", "Leto", "Gage", "Jud", "Louis"]
console.log(mix);

let paul1 = { name: "Paul Atreides", title: "Kwisatz Haderach" };
let paul2 = { name: "Paul Atreides", title: "Lisan al Gaib" };

//Object keys being overwritten according to the order
//of spreading
let paula = { ...paul1, ...paul2 };
let paulb = { ...paul2, ...paul1 };
console.log(paula);
//{ name: "Paul Atreides", title: "Lisan al Gaib" }
console.log(paulb);
//{ name: "Paul Atreides", title: "Kwisatz Haderach" }
```



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

//We must be careful while returning objects in the short return syntax.
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


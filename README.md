# The never complete, always changing JavaScript Style Guide by Vermilion for Vermilion (and for others) – Draft!

This guide is for JavaScript only, and is intended to be a guide and not the bible. It is highly opinionated, and based on best practices. Because JavaScript is always changing/getting better (i.e. ES6–), this guide will always be a draft. 

##### Here is a break down of what this guide contains.

* whitespace and indentation
* quotes, semicolons, etc.
* comments
* file naming
* variables
* arrays
* objects
* functions
* namespaces
* methods
* working with classes and prototypes
* recursion

## Whitespace and Indentation
* **operators:** use a space between each, e.g. `var b = 4 + 4 / 2;`
* **braces:** on same line for all blocks and functions
* **indentation:** 2 spaces

##### Dos and dont's
 ```javascript
 // do not do this
function foo() 
{
}

// and none of this
for(var i = 0; i < 10; i++)
{
}

// correct
function foo(){ // whitespace after  "()" is permitted but easier to leave out
}
```
#### jQuery Specific
With jQuery, many methods can be chained. You should use hard returns and indent when method chaining is used. This keeps line lengths to a minumum making code easier to read.
```javascript
// bad
$('.my-module').css('color', 'red').height(200).width(200).show();

// good
$('.my-module')
    .css('color', 'red')
    .height(200)
    .width(200)
    .show();
```
## quotes, semicolons, etc.
Use single quotes for pretty much everything.
```javascript

// good
var foo = 'bar';

// bad
var foo = "bar";

// good
var $object = $('input[name="foo"]');

// bad
var $object = $("input[name=\"foo\"]");

// do not mix styles
var my_var = 'my';
var long_string = 'hello ' + my_var + " friend";

// be consistent
var my_var = 'my';
var long_string = 'hello ' + my_var + ' friend';
```
#### semicolons
 * `var foo = 'bar';` <--
 * `var foo = function() {};` <--
 * -->`;(function(){})();` before (optional)
 
Using a linter to find missing semicolons is recommended.


## Comments
* single: `// text here`
* multiline `/* text here.. */`
* DocBlock ↓
```javascript
/*
 * function description...
 *
 * @param {string} bar This param takes a string.
 * @return {string} This returns a string.
 */
function foo(bar) {...
```
##### Do not do this

```
// this is not
// a single line 
// comment
```
##### Do not add todos unless you get rid of them in production files
 
```javascsript
// todo: make this function work
function foo() {}...
```
## File naming
##### general script files
* **source:** myfile.js
* **minified:** myfile.min.js

##### plugin files
* **source:** name-x.x.plugin.js
* **minified:** name-x.x.plugin.min.js

##### class files
* **source:** MyClass.js
* **minified:** MyClass.min.js

## Variables
##### Assignment
* Always use `var` to avoid global assignment.
* Assign at the top of blocks if the variable(s) is used more than once throughout
```javascript
function foo(myvar) {
    // assign vars here
    var bar = null;
    if(myvar) {
        bar = myvar + ' test';
    }
    ...
}
```
##### Global variables
Do not use global variables unless absolutely necessary. Here are some occassions you might use them:
* You are using a 3rd party API that requires global variables to be defined as settings

###### An alternative to global variables
* Create a namespace
  * **Example:** `MyApp.foo = 'bar';` "foo" doesn't need to be global but is accessible through your global namespace of "MyApp".

##### Constants
* new way: `const foo = 'bar';`
* fallback: `var FOO = 'bar';` use caps to indicate this is a constant

##### Dos and dont's
```javascript
 // bad
 var b = 1, c = 2, d = 3;
 
 // also bad
 var b = 1,
 c = 2,
 d = 3;
 
 // good
 var b = 1;
 var c = 2;
 var d = 3;
```
##### Variable naming
Use snake case (e.g. `"my_var"`) to name variables that contain primitives. 

**The below are primitives:**
 * string 
 * number
 * boolean
 * null
 * undefined

**Functions, objects and classes should be treated differently.**

* be explicit about the variable by giving it a name that describes its purpose (e.g. `var is_resolved = null; var number_of_items = 5;`)
* use camel case for naming variables that reference objects: `var myVar = {};`
* same for functions: `var myFunc = function() {};`
* use upper camel case for class names: `var MyClass = function() {};`
* use "$" before variables that reference jQuery objects: `var $myFoo = $('.my-foo');`
* Class/object properties should reflect most of the latter but more about that in another section.

**Exceptions**

If your code works with an API or some 3rd party script, make sure to consult documentation on naming conventions for variable names. Same goes with properties.
```javascript
$.ajax({
    url: 'http://api.foo.com',
    data: { 
        my_object: { foo: 'bar'} 
        // the API expects "my_object" even though this style guide requires the format of "myObject".
    }
});
```

## Objects

##### Declaring objects
```javascript
// do not do this
var myObject = new Object();
myObject.foo = 'bar';

// declare objects this way
var myObject = {};
// it's much simpler
myObject.foo = 'bar';
```
##### Setting properties
For object properties, follow the same naming conventions of variables.
```javascript
// set initial values or defaults like this
var myObject.foo = {
    foo: null,
    myData: {},
    test: 1234
};
// set properties later on like this
myObject.foo = 'bar';
myObject.myData.foo2 = 'bar2';
```
## functions
Like variables, function and method names should be explicit about what they do and at the same time be simple enough where the name of the function/method does not take up a whole line.
Functions/methods should serve the purpose of accepting input, doing some work, and then outputting through a return statement. If it does not return, it should do some property manipulation on the object if it is a method. Lastly, it is acceptable to not return a value if it is asynchronous like timeouts, DOM events, or AJAX calls.

##### Defining functions
Do not define functions globally. This means you must use a namespace.
```javascript
// bad (becomes a global function)
var my_function = function(a) { 
    return a + ' bar'; 
};
// also bad (becomes a global function)
window.my_function = function(a) { 
    return a + ' bar'; 
};
// bad! it is stil global because there is no "var" before the function name.
$(function() {
  my_function = function(a) { 
    return a + ' bar'; 
  };
});

// better, but a mess because it lacks organization
$(function() {
 /* 
  The function is defined within this scope 
  and is not acessible by anything outside. 
  This is fine if you want this function to be private. 
  More on that later.
  */
  var my_function = function(a) { 
    return a + ' bar'; 
  };
});
```

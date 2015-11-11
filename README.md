# The never complete, always changing JavaScript Style Guide by Vermilion for Vermilion (and for others) – Draft!

This guide is for JavaScript only, and is intended to be a guide and not the bible. It is highly opinionated, and based on best practices. Because JavaScript is always changing/getting better (i.e. ES6–), this guide will always be a draft. 

##### Here is a break down of what this guide contains.

* indentation and whitespace
* comments
* file naming
* variables
* arrays
* objects
* declaring functions, methods 
* working with classes and prototypes
* recursion

## Indentation and Whitespace
* **Identation:** 2 spaces
* **braces:** on same line for all blocks and functions
 ```javascript
 // do not do this
function foo() 
{
}

// and none of this
for(var i=0; i < 10; i++)
{
}

// correct
function foo(){ // whitespace after  "()" is permitted but easier to leave out
}
```
### jQuery Specific
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

##### Class files
* **source:** MyClass.js
* **source:** MyClass.min.js


# The never complete, always changing JavaScript Style Guide by Vermilion for Vermilion (and for others)

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
## Comments
* single: `// text here`
* multiline `/* text here.. */`
* DocBlock ↓
```javascript
/*
 * function description...
 *
 * @param {string} this param takes a string
 * @return {string} this returns a string
 */
function foo(bar) {...
```

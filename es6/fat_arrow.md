# Fonctions flêchées

## Syntaxe raccourcie

```js
// ES5 lambdas-like
var numbers = [ 10, 20, 30, 50 ];
var multiplyBy10
            = numbers.map
             (
                 function( a )
                 {
                     return a * 10;
                 }
             );
console.log( multiplyBy10 );

// ...becomes in ES2015
const numbers      = [ 10, 20, 30, 50 ];
const multiplyBy10 = numbers.map( a => a * 10 );
console.log( multiplyBy10 );
```
```js
// With multiple arguments, add parenthesis
const numbers         = [ 10, 20, 30, 50 ];
const multiplyByIndex = numbers.map( ( a, i ) => a * i );
console.log( multiplyByIndex );
```

```js
// Beware if you need to return a structure, wrap it in parenthesis
const numbers      = [ 10, 20, 30, 50 ];
const multiplyBy10 = numbers.map( a => ({ res: a * 10 }) );
// not const multiplyBy10 = numbers.map( a => { res: a * 10 } );
console.log( multiplyBy10 );
```

## Portée du `this`

```js
// ES5 this
function Clock()
{
	this.currentTime = new Date();
};

Clock.prototype.start = function()
{
	var self = this;// Save scope in closure
	setInterval
	(
		function()
		{
			self.currentTime = new Date();
		}, 1000
	);
};

// ES6 with arrow functions,
// automatically scope this to its outer scope
// !! Beware !!
// Arrow function uses lexcial scope
Clock.prototype.start = function()
{
	setInterval
	(
		() =>
		{
			this.currentTime = new Date();
		}, 1000
	);
};
```
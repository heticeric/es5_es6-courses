# L'`Object` sous toutes les coutures

## Contruction
```js
// Object structure
const user =
{
  // No function anymore
  getName()
  {
      return 'Wowza !';
  }
};

console.log( user.getName() );
```

## Desconstruction
```js
// Object construction
const name = 'Arunoda';
const age  = 80;

const user = { name, age };

// Object destructuration
const user =
{
  name: 'Eric',
  age : 20,
  city: 'Montreuil'
};

const { name, age } = user;
console.log( name, age );


// Destructuring in functions
function printName( { name } )
{
	console.log( 'Name is: ' + name );
}

const user = 
{
	name: 'Eric',
	age : 20,
	city: 'Montreuil'
};

printName( user );

// or better
function printUser( { name, age = 20 /* default value */ } )
{
	console.log( 'Name is: ' + name + ' Age: ' + age );
}


// Destructuring works also with arrays
function printUser( [ name, age = 20 ] )
{
	console.log( 'Name is: ' + name + ' Age: ' + age );
}

printUser( [ "Eric", 40 ] );
```
## Spread
```js
function sum( a, b )
{
	return a + b;
}

// rest parameter is spreading
function sumAndLog( ...args )
{
	const result = sum( ...args );
	console.log( 'Result is: ' + result );
	return result;
}

sumAndLog( 10, 20 );
```
## Cloner et fusionner
```js
const user           = { name: "Eric" };
const newUser        = { ...user };
const withAge        = { ...user, age: 20 };
const newUserVersion = { age: 80, ...user };

console.log( newUser, withAge, newUserVersion );
```
## Mutabilité

```js
// Pure function for functional programming :
// Function without side effect

// Objects
function addMarks( user, marks )
{
	return {
		...user,
		marks
	};
}

const user          = { username: 'eric' };
const userWithMarks = addMarks( user, 20 );

console.log( user, userWithMarks );

// Arrays
function addUser( users, username )
{
	const user = { username };
	return [
		...users,
		user
	];
}

const user     = { username: 'eric' };
const users    = [ user ];
const newUsers = addUser( users, 'john' );

console.log( users, newUsers );
```
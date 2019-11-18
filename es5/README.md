# Bienvenue en ES5

## L'Array au milieu

### Vive les bouclettes

Avec l'avènement de la programmation fonctionnelle, une série de nouvelles fonctions sont apparues, permettant des itérations d'un nouveau genre…

```js
[ 1, 2, 3 ].forEach
(
	function( v )
	{
		console.log( v );
	}  
);
```

Exercice pour les imprudents, réalisez l'implémentation de la fonction `forEach` 

Petit _divulgachage_ ES6

```js
[ 1, 2, 3 ].forEach( v => console.log( v ) );
```
 
 
### Bouclettes focntionnelles

```js
[ 1, 2, 3 ].map(
	function( elem, index, arr )
	{
		return elem * elem;
	}
);
//returns [1, 4, 9]

[ 1, 2, 3, 4, 5 ].filter(
	function( elem, index, arr )
	{
		return elem % 2 === 0;
	}
);
//returns [2, 4]

[ 1, 2, 3, 4, 5 ].some(
	function( elem, index, arr )
	{
		return elem >= 3;
	}
);
//returns true

[ 1, 2, 3, 4, 5 ].every(
	function( elem, index, arr )
	{
		return elem >= 3;
	}
);
//returns false
```

Mais aussi :

```js
[ 1, 2, 3, 4, 5 ].reduce(
	function( sum, elem, index, arr )
	{
		return sum + elem;
	}
);
//returns 15

[ 1, 2, 3, 4, 5 ].reduceRight(
	function( sum, elem, index, arr )
	{
		return sum + elem;
	}, 10
);
//returns 25
```


## Cet obscur `Object`…

### Object.keys(obj)

```js
/**
 *  Returns an array of strings representing all the enumerable property names of the object.
 */

// Example
var obj = { name: "Eric", url: "http://ericpriou.net/" };

print( Object.keys(obj).join(", ") );
// name, url


// Shim
Object.keys = function( obj )
{
	var array = new Array();
	for( var prop in obj )
	{
		if( obj.hasOwnProperty( prop ) )
		{
			array.push( prop );
		}
	}
	return array;
};
```

### Mutabilité

Attention, sujet très sensible !

```js
var prof = 
{
	name : "Eric"
};
prof.teach = function()
{
	return this.name +" enseigne"; //SHAME !
}   
```

Pour prévénir ces effets de bords :

```js
/*
	Extension
 */
var obj = {};

obj.name = "John";
print( obj.name );
// John

print( Object.isExtensible( obj ) );
// true

Object.preventExtensions( obj );

obj.url = "http://ejohn.org/"; // Exception in strict mode

print( Object.isExtensible( obj ) );
// false


/*
	Sealing an object prevents other code from deleting, or changing the descriptors of, any of the object’s properties – and from adding new properties.
 */
Object.seal( obj );
Object.isSealed( obj );

/*
	Freezing an object is nearly identical to sealing it but with the addition of making the properties un-editable.
 */
Object.freeze( obj );
Object.isFrozen( obj );

```

### Object.create( obj )

```js
function User(){}
User.prototype.name = "Anonymous";
User.prototype.url  = "http://google.com/";

var john = Object.create(
	new User(),
	{
		name:
		{
			value: "Eric",
			writable: false
		},
		url : { value: "http://google.com/" }
	}
);

print( john.name );
// Eric

john.name = "Ted"; // Exception if in strict mode
```

### Object.defineProperty( obj, prop, desc )

```js
var obj = {};

/*
 {
	 value: "test",
	 get : callback,
	 set : callback,
	 writable: true,
	 enumerable: true,
	 configurable: true
 }
 */

Object.defineProperty(
	obj, "value", {
		value       : true,
		writable    : false,
		enumerable  : true,
		configurable: true
	}
);

(function()
{
	var name = "Eric";

	Object.defineProperty(
		obj, "name", {
			get: function()
			{
				return name;
			},
			set: function( value )
			{
				name = value;
			}
		}
	);
})();

print( obj.value )
// true

print( obj.name );
// Eric

obj.name = "Ted";
print( obj.name );
// Ted

for( var prop in obj )
{
	print( prop );
}
// value
// name

obj.value = false; // Exception if in strict mode

Object.defineProperty(
	obj, "value", {
		writable    : true,
		configurable: false
	}
);

obj.value = false;
print( obj.value );
// false

delete obj.value; // Exception


// To get property description
// Object.getOwnPropertyDescriptor( obj, "value" )

```

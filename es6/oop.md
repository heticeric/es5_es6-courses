# Orienté objet

## La classe 

```js
class Vehicle {
	constructor( type, number )
	{
		this.type   = type;
		this.number = number;
	}

	display()
	{
		return `Number: ${ this.number }`;
	}
}

const v1 = new Vehicle( 'Audi', 'GH-2343' );
console.log( v1.display() );
```

## Héritage

```js
// Inheritance
class Vehicle {
	constructor( type, number )
	{
		this.type   = type;
		this.number = number;
	}

	display()
	{
		return `Number: ${ this.number }`;
	}
}

class Car extends Vehicle {
	constructor( number )
	{
		super( 'Car', number );
	}

	display()
	{
		const value = super.display();
		return `Car ${value}`;
	}
}

const v1 = new Car( 'GH-2343' );
console.log( v1.display() );

```
# Warning ! Zone de turbulences

Les fonctions sont la clé de voute de vos programmes.
Mais attention, il y a certaines particularités à maîtriser.

##  `this` is a thing

Pour les gurus de l'orienté objet, `this` est une valeur essentielle. Elle faut référence à l'occurence de la classe. Elle permet entre autre d'appeler une méthode u sein de la classe.

```js
class Man
{
	constructor( name )
	{
		this.name = name;
	}
	
	eat()
	{
		console.log( this.name +" is eating, bro !" ); 
	}
}
```

Toutefois, son usage peut prêter à confusion :

```js
var f = function(){ console.log( this ) };

f();
var o = { f : f };
o.f(); 
new f(); // Ouch I'm an instance now
```

Pire ! Sa valeur peut être modifié à l'execution. 
**Attention, âmes sensibles d'abstenir **

```js
f.apply( { name : "sweat !" } );
```

## Portée lexicale

```js
var banque = function()
{
	var secret = 42;
	
	return function( pwd )
	{
		if( pwd === 42 ) return "OK";
		else return "KO";
	}
}

var moncompte = banque();
moncompte( 42 );
console.log( secret );// SyntaxTerror 
```

Les variables déclarées dans une fonction parente, sont accessibles à leurs fonctions enfant.


## Closure

Mieux encore, la portée lexicale est persistante :

```js
// On déclare une IIFE pour protéger l'accès à une portée lexicale privée
(
	function()
	{
		var iteration = 0;
		setInterval
		(
			function()
			{
				console.log( iteration ++ );
			}, 500
		)
	}
)();
```

![Mind blowing](../images/mindblowing.jpeg)

Petit exercice pour les plus kamikazes : comment faire en sorte de stopper cette fonction `setInterval()` à tout moment ?
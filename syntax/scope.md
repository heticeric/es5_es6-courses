# Valeurs inaccessibles

## solutions locales pour un problème global

Les variables se définissent avec le mot clé `var`

```javascript
var pouet;
```

Une variable définie au sein d'une fonction est dite locale

```javascript
function banque()
{
	var motdepasse = "pouet";
}

banque();
console.log( motdepasse );
```

**Attention**, sans le mot clé `var`, est devient globale

```javascript
function president()
{
	compagne = "julie";
}

president();
console.log( compagne );// C'est ballot
```

Pour finir, retenez ** GLOBAL C'EST MAL**


En `es6`, deux nouvelles déclarations voient le jour : `let`et `const`. Sachez pour le moment que la portée de ces déclarations appartient au bloc.

```
{
	// Déclaration d'un bloc
	const tada = "Surprise !";
}

console.log( tada );//SyntaxTerror
```
![Syntax terror](../images/google-glass-zombie.jpg)


## Passage par valeur ou par référence

Deux magnets à mettre sur votre frigo :

```javascript
var a = 10;
var a = b;
a += 1;
console.log( b );
```

```javascript
var a = [ 1, 2 ];
var a = b;
a.push( 3 );
console.log( b );
```

## Référence à une fonction

Fonctions anonymes

```javascript
var add = function( a, b )
{
	return a + b;
};

var ajoute = add;// !! Notez l'absence de parenthèses !!

ajoute( 1, 2 );
```

Inclusion dans une collection

```javascript
var courses =
[
	function(){ return "Pain" }
	,function(){ return "Vin" }
	,function(){ return "..." }
];

for( var i = 0, l = courses.length; i<l; i++ )
{
	console.log( "Achetez du "+ courses[ i ]() );
}
```

Passage par argument

```javascript
var courses =
[
	function(){ return "Pain" }
	,function(){ return "Vin" }
	,function(){ return "..." }
];

courses.forEach
(
	function( aliment )
	{
	    console.log( "Achetez du "+ aliment() );
	}
);
```

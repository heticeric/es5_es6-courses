# Drôle de types

- langage dynamique
- peut supporter des structures orientées objets, mais sans l'usage de classes (!?)
- les fonctions sont un type à part entière

Il faut distinguer les types primitifs, des complexes, car ils ne réagissent pas de la même façon.

### Types primitifs

### boolean

- `true`
- `false`
… voilà !

#### number

- Le type number ne distingue pas les entiers, des nombres à virgules.
- exprimé par une valeur à double-precision 64-bit format IEEE 754

```javascript
console.log( 0.1 + 0.2 ); // 0.30000000000000004
```

- Tous les opérateurs standards sont disponibles, plus le `%
- La conversion d'une chaine : `parseInt( "3zer" )` ou `parseFloat( "3.23ert" )`
- Pour certaines opérations, nous obtiendrons la valeur `NaN`
Cette valeur est de type number, mais attetion :

```javascript
console.log( NaN == NaN ); // false
console.log( isNaN( NaN ) );// true
```

#### string

Les string (j'en vois certains qui ricanent…) sont des séquences de caractères Unicode, représenté sur 16 bits.

```javascript
console.log( "ta mère en string".length );
```

#### `undefined`

Valeur par défaut des variables

```javascript
var pouet;
console.log( pouet );// undefined
```

### Types complexes

#### Object

- Collections de clé -> valeur.
- La clé est une `string`, la valeur n'importe qu'elle valeur
- Très utile pour sauvegarder des valeurs structururées

Initialisation :
```javascript
// Notation objet
var prof = new Object();
// Notation littérale
var prof = {};

// Ecriture
prof.nom = "Eric";
// Lecture
console.log( prof.nom );// "Eric"

// ou
// Ecriture
prof[ 'nom' ] = "Eric";
// Lecture
console.log( prof.nom );// "Eric"
```

#### Array

- Les `array` sont une forme hybride des `object`
- Leurs clés sont des index numériques
- Ils possèdent des méthodes propres et d'une propriété `length`

```javascript
// Notation objet
var cours = new Array();
// Notation littérale
var cours = [];

// Ecriture
cours[ 0 ] = "Passeport pour le Javascriptan";
// ou
cours.push( "node.js" );

// Lecture
console.log( cours[ 1 ] );
```

**Attention** : les `array` peuvent avoir des "trous"

```javascript
cours[ 999 ] = "0100101";
console.log( cours.length );
```

#### Functions

Les fonctions font parties des complexes en javascript

```javascript
// Déclaration
function hurle()
{
	return "HAAAAAAAAAA";
}

// Invocation
hurle();
```

Les fonctions prennent des arguments, tous optionnels

```javascript
// Déclaration
function add( a, b )
{
	return a + b;
}

// Invocation
add( 1, 2 );// 3
add( 1 );// 0
add()// 0
add( 1, 2, 3, 4 );// 3
```

Tous les arguments sont récupérables dynamiquement

```javascript
// Déclaration
function add( a, b )
{
	var o = 0;
	for( var i=0, l = arguments.length; i<l ; i++ )
	{
		o += arguments[ i ];
	}
	return 0;
}

// Invocation
add( 1, 2, 3, 4 );// 10
```
# La déclarations des droits ES6

## Parquer les variables

`let` et `const` définissent de variables réservées aux bloc : `{}`. Cette portée complète la portée lexicale des fonctions.

## Exemple de bloc

```js
if( true ){ let it = "be";  }
```

## Portée de bloc

```js
// Who need IIFE now ?
{
	let test = "test";
	const cantchange = 0;

	// TypeError: Assignment to constant variable.
	// cantchange = 1;
}
```

## L'inconstance des constantes
Les déveleioppeurs préfèrent souvent utiliser des `const`dans leur code.

```
const politicians = true;
politicians = false; // TypeError
```

Toutefois :

```js
{
	// Beware const don't forbid object's values change
	const prof = { name : "eric" };
	prof.name = "Eric";
}
```
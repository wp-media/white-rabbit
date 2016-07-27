# JavaScript



## Quels guillemets et quand ?

```js
var variable = 'Value';
```

> N'écrivez pas

```js
var variable = "Value";
```

Comme nous l'avons vu pour les [guillemets en HTML](#simple-ou-double), les **_double_** sont réservés aux attributs HTML. Nous gardons les **_simple_** pour JavaScript et ses valeurs.

L'idée de base est de conserver la syntaxe HTML quand on fait un lien entre JavaScript et HTML. Il est plus simple d'écrire une valeur sans devoir échaper son contenu et sans modifier la syntaxe du HTML.


> En effet il est plus simple d'écrire :

```js
var els = document.querySelectorAll('[data-lol="plop"]');
```

> que :

```js
var els = document.querySelectorAll("[data-lol=\"plop\"]");
```


## Concaténation

```js
var output =  '<div>'
				+ '<p>'
					+ '…'
				+ '</p>'
			+ '</div>';

```

> N'écrivez pas

```js
var output = '<div>';

output += '<p>';
output += '…';
output += '</p>';
output += '</div>';

```

L'idéal est de conserver l'indentation lorsque vous composez un balisage directement dans JS. Il est ainsi plus aisé de retrouver qui est le parent de qui, notamment dans un ensemble complexe.

## jQuery: Événements custom

```js
$( 'a' ).on( 'namespace:action', 'doSomething' );
```

> N'écrivez pas

```js
$( 'a' ).on( 'nawakAction', 'doSomething' );

```

L'idéal est de conserver l'indentation lorsque vous composez un balisage directement dans JS. Il est ainsi plus aisé de retrouver qui est le parent de qui, notamment dans un ensemble complexe.

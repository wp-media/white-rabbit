# CSS

Nous n'allons pas utiliser les termes CSS 2.1, ou CSS 3. Nous ne parlerons que de CSS.

Aujourd'hui il est rare d'utiliser CSS sans pré-processeur (ou post-processeur). Cette partie de la convention va donc mêler les deux usages.

Cette convention tente de fusionner les bonnes pratiques proposées par les méthodes [SMACSS](https://www.creativejuiz.fr/blog/css-css3/smacss-en-francais-organiser-css-efficacement), [OOCSS et BEM](http://www.alsacreations.com/article/lire/1641-bonnes-pratiques-en-css-bem-et-oocss.html).

<aside class="notice">Le nom des classes doit être en anglais</aside>

## Le sélecteur : espaces

```css
.element {}
.element > .children {}
.element + .siblings {}
```

> N'écrivez pas

```css
.element{}
.element>.children{}
.element+.siblings{}
```

Aérez ! Ne collez pas les éléments les uns aux autres, utilisez **une** espace pour les séparer, et pas davantage.



## Le sélecteur : multiple

```css
.element-1,
.element-2 {}
```

> N'écrivez pas

```css
.element-1, .element-2 {}
```

Lorsque vous concaténez plusieurs sélecteurs, sautez une ligne à chaque nouveaux sélecteur afin de les rendre plus lisibles. C'est plus facile ainsi que d'aller chercher un sélecteur dans une liste de 5 ou 6 éléments concaténés.



## Le sélecteur : d'attribut

```css
.element[attr="value"] {}
```

> N'écrivez pas

```css
.element[attr=value] {}
```

Les deux sont valides, mais s'il fallait en choisir un autant conserver la même syntaxe qu'en HTML. De plus il s'agit de celle recommandée par le W3C.



## Le sélecteur : indentation de parentée

```css
.element {}
.element .child {}
.element-child {}
```

> N'écrivez pas

```css
.element {}
	.element .child {}
	.element-child {}
```

Dans l'idéal, commencez par déclarer les styles des parents, puis des enfants, dans l'ordre de lecture, cela facilité la lecture de l'héritage propre à CSS.

Cependant, n'affichez pas le lien de parenté d'un élément à un autre en indentant l'élément enfant comme vous le feriez en HTML. Cette syntaxe apporte trop de confusion par rapport à celle proposée par les pré-processeurs.



## La propriété : les raccourcis

```css
.element {
	font: italic bold .8em/1.2 Arial, sans-serif;
}
```

> et 

```css
.element {
	font-style: italic;
	font-weight: bold;
	font-size: .8em;
	line-height: 1.2;
	font-family: Arial, sans-serif;
}
```

[Le raccourci des propriétés](https://developer.mozilla.org/fr/docs/Web/CSS/Propri%C3%A9t%C3%A9s_raccourcies) **est libre**.<br>
Si vous n'êtes pas familiers avec cette syntaxe, il vaut mieux expliciter les propriétés que de se planter sur le raccourci.

Les versions non raccourcies sont de toutes manières utiles lors de l'édition d'une seule des "sous-propriétés" dans le cadre d'un héritage et d'un besoin de modification.

__A PRECISER__


## La règle : présentation

```css
display: flex;
```

> N'écrivez pas

```css
display :flex
```

La composition d'une règle se forme toujours du nom de la propriété suivie d'un deux-points puis d'une espace, de la valeur de la propriété et d'un point-virgule.



## La règle : indentation

```css
.element {
	position: absolute;
	top: 40px;
	left: 0;
	right: 0;
}
```

> N'écrivez pas

```css
.element {
	position: absolute;
		top: 40px;
		left: 0; right: 0;

	-moz-transition: all .725s;
		 transition: all .725s;
}
```

Chaque règle est écrite sur une ligne différente et indentée sur le même niveau.

Les règles ne doivent pas être regroupées sur une seule ligne et ne doivent pas avoir une indentation supérieure à une unité. (tabulation, dans notre cas)



## La règle : ordre des propriétés

```css
.element::before {
	/* Generated content */
	content: "—";

	/* Box model */
	position: absolute;
	top: 0;
	z-index: 1337;
	overflow: hidden;

	/* Box dimensions */
	width: 300px;
	padding: 1.5rem;
	margin: 1rem;

	/* Inside the box */
	font-size: 1.2rem;
	line-height: 1.6;

	/* Decoration */
	color: #BADA55;
	text-shadow: 0 1px 0 rgba(0, 0, 0, .1);
	border-radius: 3px;
	box-shadow: 0 1px 6px rgba(0, 0, 0, .15);
}
```

Il existe 2 écoles principales : l'ordre alphabétique (nom des propriétés), et l'ordre sur les types de modifications effectuées par ces propriétés.

Nous avons opté pour un ordre logique de modification de la boîte :

1. Le contenu généré,
1. Les propriétés qui modifie le modèle de boîte,
1. Les propriétés qui influent sur les dimensions,
1. Les propriétés de texte (intérieur de la boîte),
1. La peinture… la décoration quoi.



## Les valeurs

```css
color: rgb(255, 245, 235);
background-image: url("/assets/images/logo.png");
padding: .75em 1em;
margin: 0 auto;
```

> N'écrivez pas

```css
color: #F1F2F3;
background-image: url(/assets/images/logo.png)
padding: 0.75em 1em;
margin: 0px auto;
```

Certaines valeurs de propriété ont des syntaxes alternatives.

* Les couleurs : l'utilisation de `rgb()` est à privilégié pour faciliter la transition vers `rgba()`,
* Les valeurs d'URL : démarquer la valeur avec des guillemets,
* Les zéros : 
 * utiliser la notation mathématique sans le `0` pour les valeurs décimales inférieures à 1.
 * ne pas préciser l'unité pour les valeurs de `0`.



## Convention de nommage

```css
.main-nav {
	display: flex;
}
.main-nav-link {
	color: #bada55;
}
.main-nav-link.current {
	text-decoration: underline;
}
```

Ce qui ressort le plus des solutions comme BEM ou SMACSS c'est le fonctionnement en module et l'idée de prévoir un code réutilisable et pas complètement dépendant du DOM (éléments utilisés ou position dans la structure globale).

Ici par exemple, rien ne me dit que `.main-nav` est un élément `ul` ou `nav`, ni où il se trouve dans le DOM. L'important dans mon code est de comprendre que le `-link` que je modifie appartient à `.main-nav`.

Des modifieurs peuvent venir s'appliquer mais ne doivent jamais être stylés indépendamment. Autrement dit, aucun style n'est appliqué à `.current`, `.active`, etc.


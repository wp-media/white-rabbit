# CSS

We will not use the terms CSS 2.1 or CSS 3. We will only talk about CSS.

Today, it's really rare coding CSS without using a pre-processor (or post-processor). This part of this convention will merge both usages: with and without pre-processor.

This convention try to merge good practices proposed by methodes like [SMACSS](https://smacss.com/), [OOCSS](http://oocss.org/) and [BEM](http://getbem.com/introduction/). Sometimes, we will introduce usual classes like [Atomic CSS](https://github.com/nemophrost/atomic-css) propose.

<aside class="notice"><strong>Important:</strong> Class name have to be in english</aside>

## Selector: spaces

```css
.element {}
.element > .children {}
.element + .siblings {}
```

> Don't write

```css
.element{}
.element>.children{}
.element+.siblings{}
```

Ventilate! Don't stick each elements to another, use **a** space to separate them, and no more than one space.



## Selector : multiple elements

```css
.element-1,
.element-2 {}
```

> Don't write

```css
.element-1, .element-2 {}
```

When you need to concatenate several selectors, put one selector by line to make them more readable. It's easier to do so than being looking for an item in a list of 6 ou 7 elements in the same line. Trust me.



## Selector : of attribute

```css
.element[attr="value"] {}
```

> Don't write

```css
.element[attr=value] {}
```

Both are valid, but if you'd have to chose only one, you'd better keep the same syntax as HTML syntax. Moreover, it's the one recommended by the W3C.



## Selector : indentation of kindred

```css
.element {}
.element .child {}
.element-child {}
```

> Don't write

```css
.element {}
	.element .child {}
	.element-child {}
```

The best way is to follow a logical order to declare your selector. Begin with the parents, then the children, in the same order of the DOM. It makes the thing easy when you read and look for heritage inside your own CSS document.

However, don't show the kindred link between elements by indenting child under the parent like you should do with you HTML code. This syntax brings to much confusion regarding the syntax proposed by and for the pre-processors.



## Property : the shorthand

```css
.element {
	font: italic bold .8em/1.2 Arial, sans-serif;
}
```

> and

```css
.element {
	font-style: italic;
	font-weight: bold;
	font-size: .8em;
	line-height: 1.2;
	font-family: Arial, sans-serif;
}
```

[Shorthand properties](https://developer.mozilla.org/en-US/docs/Web/CSS/Shorthand_properties) ** is up to you**.<br>
If you are not a friend of the short syntax, you'd better use complete and explicit properties instead of doing a wrong shorthand.

In anyway, the shorthand properties are useful when you need to re-declare one of the "sub-property", in a case of heritage. (e.i. a sprites and the `background`/`background-position` properties)

Think about that: you maybe not have to re-declare all the properties in a shorthand. Use the CSS heritage.

By default, try to be explicit as well as possible when you begin to have a complex property like multiple background to increase the readability of your code.


## Rule : presentation

```css
display: flex;
```

> Don't write

```css
display :flex
```

A rule is composed with the **property name**, then a **colon** (without space between), then a **white-space**, then the **property value**, and at the end a **semi-colon**.



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


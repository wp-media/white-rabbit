# CSS

We will not use the terms CSS 2.1 or CSS 3. We will only talk about CSS.

Today, it’s really rare coding CSS without using a pre-processor (or post-processor). This part of this convention will merge both usages: with and without pre-processor.

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

Ventilate! Don’t stick each elements to another, use **a** space to separate them, and no more than one space.



## Selector: multiple elements

```css
.element-1,
.element-2 {}
```

> Don’t write

```css
.element-1, .element-2 {}
```

When you need to concatenate several selectors, put one selector by line to make them more readable. It’s easier to do so than being looking for an item in a list of 6 ou 7 elements in the same line. Trust me.



## Selector: of attribute

```css
.element[attr="value"] {}
```

> Don’t write

```css
.element[attr=value] {}
```

Both are valid, but if you’d have to chose only one, you’d better keep the same syntax as HTML syntax. Moreover, it’s the one recommended by the W3C.



## Selector: indentation of kindred

```css
.element {}
.element .child {}
.element-child {}
```

> Don’t write

```css
.element {}
	.element .child {}
	.element-child {}
```

The best way is to follow a logical order to declare your selector. Begin with the parents, then the children, in the same order of the DOM. It makes the thing easy when you read and look for heritage inside your own CSS document.

However, don’t show the kindred link between elements by indenting child under the parent like you should do with you HTML code. This syntax brings to much confusion regarding the syntax proposed by and for the pre-processors.



## Property: the shorthand

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
If you are not a friend of the short syntax, you’d better use complete and explicit properties instead of doing a wrong shorthand.

In anyway, the shorthand properties are useful when you need to re-declare one of the "sub-property", in a case of heritage. (e.i. a sprites and the `background`/`background-position` properties)

Think about that: you maybe not have to re-declare all the properties in a shorthand. Use the CSS heritage.

By default, try to be explicit as well as possible when you begin to have a complex property like multiple background to increase the readability of your code.


## Rule: presentation

```css
display: flex;
```

> Don’t write

```css
display :flex
```

A rule is composed with the **property name**, then a **colon** (without space between), then a **white-space**, then the **property value**, and at the end a **semi-colon**.



## Rule: indentation

```css
.element {
	position: absolute;
	top: 40px;
	left: 0;
	right: 0;
}
```

> Don’t write

```css
.element {
	position: absolute;
		top: 40px;
		left: 0; right: 0;
}
```

Each rule is written on a new line and must be indented on the same level.

The rules should not be grouped together on one line and should not have more than one unit of indentation. (one tab in our case)



## Rule: properties order

```css
.element::before {
	/* Generated content */
	content: "—";

	/* Box model */
	box-sizing: content-box;
	position: absolute;
	top: 0;
	right: 0;
	bottom: 0;
	left: 0;
	z-index: 1337;
	overflow: hidden;

	/* Box dimensions */
	width: 300px;
	padding: 1.5rem;
	margin: 1rem;
	border: 1px solid rgb(0, 0, 0);

	/* Inside the box */
	font-size: 1.2rem;
	line-height: 1.6;
	letter-spacing: 0.125em;

	/* Decoration */
	text-decoration: underline;
	color: #BADA55;
	border-radius: 3px;
	background: rgba(255, 255, 255);
	text-shadow: 0 1px 0 rgba(0, 0, 0, .1);
	box-shadow: 0 1px 6px rgba(0, 0, 0, .15);
}
```

There are 2 main schools of thought: the alphabetic order (property names) and the type of property order. The type of property order classify the properties depending on the changes they do on the element styles.

We will use this second order: the type one. This is the order we will try to fit:

1. The generated content,
1. The properties that modify the box model,
1. The properties that change the dimensions of the box,
1. The properties about texts (inside the box),
1. The painting… the decoration. (colors, shadows, etc.)

Take a look at the non-explicit example beside.
Remember this convention is a recommandation, if you have doubt, don’t wast your time asking you where a property should go. Write it, we will see later ;p



## The values

```css
color: rgb(255, 245, 235);
background-image: url("/assets/images/logo.png");
padding: .75em 1em;
margin: 0 auto;
```

> Don’t write

```css
color: #F1F2F3;
background-image: url(/assets/images/logo.png)
padding: 0.75em 1em;
margin: 0px auto;
```

Some property values have alternative syntaxes:

* Colors: try to use `rgb()` if it’s possible, to make the transition to `rgba()` easier,
* URL values: wrap those URL with double-quotes,
* Zeros: 
 * use the mathematics notation without `0` unit for floating number smaller than 1.
 * do not precise unit for `0` values.



## Naming convention

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

BEM and SMACSS are bringing to us the idea to focus on reusable code thanks to modules. Your CSS code should not depend to the DOM. (elements used or position in the global structure).

For example, here, nothing is telling me that `.main-nav` is an `ul` or `nav` element, neither where it is situated in the DOM. The important thing is to understand that `-link` is a child of `.main-nav`, just thanks to its class name.

Modifiers can be applied, though they should not be styled apart. In other words, no style is applied to `.current`, `.active`, etc. But styles can be applied to `.main-nav-link.current` for example.


# HTML

Oui, nous allons parler de HTML5 (nom W3C) ou d'un truc nommé HTML Living Standards (WhatWG), mais sans parler de version, parce qu'en fait on s'en moque un peu (sauf sur un ou deux points peut-être). Le but est de proposer des règles qui pourront s'appliquer peu importe la version de HTML.



## Le Doctype

```html
<!doctype html>
```

> ou

```html
<!DOCTYPE html>
```

On ne le déclare généralement qu'une fois dans un projet, alors autant bien le faire.

Que l'on conserve une version  **en minuscules ou en majuscules**, ce n'est pas important, l'important est d'utiliser un `doctype` HTML5 qui est celui-ci.

<aside class="warning">
	Cet élément doit être le premier octet de votre document. Pas d'espace avant, pas de saut de ligne, rien… Pensez-y lors de l'utilisation de langages dynamiques.
</aside>



## L'élement `html` et l'attribut `lang`

```html
<html lang="en_US">
```

> ou

```html
<html lang="en">
```

Les deux sont à renseigner dans votre document, pas de `html` sans `lang`, jamais.

Cela permet d'éviter des comportements étranges comme la lecture de certains textes anglais en polonais par un lecteur d'écran chinois.

L'attribut `lang` peut être très précis ou plus générique, du moment qu'il est renseigné. (et dans la bonne langue, tant qu'à faire)



## `head` et `body` ton document contiendra

```html
<head>
	<!-- Your metas -->
</head>
<body>
	<!-- Your contents -->
</body>
```

Alors oui, HTML5 permet de s'en passer, mais dans un objectif de clarté et de lisibilité, leur utilisation doit être explicite.

Concernant leur [indentation](#indentation-et-imbrication) au sein de l'élément `html` lui-même, elle n'est pas obligatoire.



## `meta` cagoule

```html
<meta charset="UTF-8">
<meta name="viewport" content="initial-scale=1.0">
```

Les balises auto-fermantes de manière générale sont écrites sans le slash final, c'est également le cas des balises `meta`.

Concernant les nouveautés qu'il ne faut pas oublier : la `meta:charset` est raccourcie, c'est cette version que l'on utilise désormais, et plus l'ancienne.



## Indentation et imbrication

```html
<ul>
	<li>
		<a href="#">
			<span>Text node</span>
		</a>
	</li>
</ul>
```

> Ne faites pas

```html
<ul>
	<li><a href="#"><span>Text node</span></a></li>
</ul>
```

Chaque élément à l'intérieur d'un autre élément HTML doit être indenté à la ligne. Le but de cette présentation est de toujours bien voir la hiérarchie entre ces éléments, ou leur fratrie.

Nous ne cherchons pas à gagner de la place dans le code, ou à minifier manuellement. Cette dernière tâche est automatisée de toute manière.

Pensez-y également lorsque le code est généré dynamiquement en PHP ou Python (ce qui sera souvent notre cas). Les seules exceptions à la règle seront les sorties mal formattées de certaines fonctions de WordPress, ou d'une librairie PHP ou Python.

<aside class="notice">Les éléments <code>head</code> et <code>body</code> n'ont aucune obligation à être indentés.</aside>



## Fermeture de balise

```html
<ol>
	<li>First list item</li>
	<li>Second list item</li>
</ol>
```

> Ne faites pas

```html
<ol>
	<li>First list item
	<li>Second list item
</ol>
```

Différentes versions de HTML permettent l'absence des balises de fermeture pour certains éléments. Pour des raisons de lisibilité et pour expliciter la structure, toutes les balises nécessitant d'être fermées doivent l'être explicitement.

Cette manière d'écrire permet également de ne pas mélanger balise à fermer et balises auto-fermantes, puisque dans notre cas nous n'auto-fermons plus les balises d'un `/`.



## Simple ou double ?

```html
<a
	href="http://wp-media.me"
	title="WP Media's website"
	class="ghost"
>WP Media</a>
```

> N'écrivez pas

```html
<a
	href=http://wp-media.me
	title='WP Media's website'
	class='ghost'
>WP Media</a>
```

Les **_simple quotes_** et **_double quotes_** sont autorisées pour démarquer les valeurs d'attribut, d'ailleurs il est même autorisé de ne pas mettre de guillemets pour certains attributs.

Dans notre cas, nous utiliserons des **_double quotes_** et uniquement celles-ci. Pour les mêmes raisons que les **_double_** seront réservés aux attributs HTML, les **_simple_** le seront pour démarquer les chaînes en [JavaScript](#quels-guillemets-et-quand) ou PHP.



## Commentaires HTML

```html
<div class="second-section">
	<div class="container">
		
		<p>My dear Lorem…</p>

		<span class="js-fill"><!-- Will be JS-ified --></span>

	</div><!-- .container -->
</div><!-- .second-section -->
```

Dans la mesure du possible, passez les commentaires à destination de l'équipe de développement dans le langage dynamique afin qu'il ne soit pas _imprimé_ directement dans le code HTML.<br>
Certains commentaires ont cependant leur place dans le code :

* **Fin de grosse section** : rappeler ce que la balise fermante ferme.
* **Remplissage JS** : si JS intervient pour remplir un élément, le préciser.

Dans tous les cas, **nos commentaires sont en anglais**.



## Vide et `:empty`

```html
<div class="projets"></div>
```

> N'écrivez pas

```html
<div class="projets">
</div>
```

Les _white spaces_ ont leur importance. Si un élément est vide, il ne faut pas ajouter d'espace blanc (tabulation, saut de ligne, espace) à l'intérieur. L'intérêt est de permettre à la pseudo-classe `:empty` de faire son travail.<br>
En cas de présence d'espace blanc, cette pseudo-classe considère l'élément comme non-vide.

Pensez-y surtout lors des phases de développement impliquant des sorties HTML.



## `button` VS `input:submit`

> Préférez

```html
<button type="submit">Send</button>
```

> à

```html
<input type="submit" value="Send">
```

Avant le bras de fer entre ces deux protagonistes, sachez qu'un bouton `button` sans valeur explicite de l'attribut `type` est considéré comme un `type="submit"`. Ceci pouvant poser problème, **précisez tout le temps au moins une valeur neutre par défaut `type="button"`**.

L'utilisation de l'élément `button` est à préférer car il permet d'enrichir le label d'une icône, d'un saut de ligne, ou de tout type de structure qui pourrait être utile à un beau design de bouton.



## Où et quand utiliser `id` et `class`.


```html

<!-- Code sample 1 -->
<div class="flex"></div>


<!-- Code sample 2 -->
<a href="#about">About</a>
<div id="about" class="flex"></div>


<!-- Code sample 3 -->
<p id="ul-desc">Awesome list</p>
<ul aria-labelledby="ul-desc"></ul>
```

```css
/* Code sample 4 */
[id="about"] {
}
```

La règle de base est d'utiliser les classes pour styler les éléments (exemple de code 1), et les identifiants pour créer des ancres (exemple de code 2) ou définir l'identité d'une section ou d'un sous élément.

Dans d'autres besoins "externes", les identifiants peuvent être utiles pour coller avec les besoins de l'API ARIA (exemple de code 3) ou des besoins liés à JavaScript. Ce dernier cas doit rester rare et contrôlé, car dire qu'un ID est utile pour du JavaScript, c'est rendre dépendant le script à un DOM très particulier.

En effet, dans le fonctionnement modulaire, il vaut mieux éviter d'utiliser les identifiants qui risques d'être dupliqués à la réutilisation d'un module. (exemple : deux widgets identiques avec des contenus différents risquerait d'avoir des identifiants identiques)

Sauf cas très exceptionnel (non-maîtrise du DOM), CSS ne doit pas styler les éléments en incluant un sélecteur d'identifiant. Cependant, le problème de poids du sélecteur ID peut-être contourné en utilisant le sélecteur d'attribut. (exemple de code 4)

<aside class="notice">Certains lecteurs d'écran permettent l'enregistrement de l'identifiant d'une section afin d'y revenir plus tard plus rapidement, pour sauter vers cette section enregistrée.</aside>

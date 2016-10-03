# JavaScript



## Which quotes and when?

```js
var variable = 'Value';
```

> Don’t write

```js
var variable = "Value";
```

As we saw it before with the [Quotes in HTML](#simple-or-double), the **_double_**-quotes are reserved to HTML attributes. We keep the **_simple_**-quotes for JavaScript and its values.

The main idea in there is to always have the same HTML syntaxe, even if we are writing HTML inside JavaScript code. Writing a value with no need to escape its content and without editing HTML is much more easy.


> Indeed, easier to write:

```js
var els = document.querySelectorAll('[data-lol="plop"]');
```

> than:

```js
var els = document.querySelectorAll("[data-lol=\"plop\"]");
```


## Concatenation

```js
var output =  '<div>'
				+ '<p>'
					+ '…'
				+ '</p>'
			+ '</div>';

```

> Don’t write

```js
var output = '<div>';

output += '<p>';
output += '…';
output += '</p>';
output += '</div>';

```

The best would be to keep indentation when you write HTML directly in JavaScript. It’s easier to find who is who (parent, children, siblings), especially when the DOM is becoming intricate.

## jQuery: Namespaced Events

```js
$( 'a' ).on(  'click.secupress', 'doSomething' );
$( 'a' ).off( 'click.secupress', 'doSomething' );
```

> Don’t write

```js
$( 'a' ).on( 'click', 'doSomething' );

```

To avoid conflicts or overwritten actions in a context like plugin or theme developement, you should make a practice of adding a name space to all your generic events.
It’s not complicated, just compose your action with `action.slug` where slug is whatever you want, at least a reserved slug for our plugin or theme.

## jQuery: Custom Events

```js
$( 'a' ).on( 'namespace:action', 'doSomething' );
```

> Don't write

```js
$( 'a' ).on( 'nawakAction', 'doSomething' );

```

When you need to create a custom event, you can theorically use any word you want like `$.on('somethingStrange')`, or `$.on('yolo.code')`. Though, we will use the form proposed next to in order to avoid confusion with namespaced generic events `click.namespace`.
For example, in SecuPress project, a custom event could be `$.on('secupress:scan')`.

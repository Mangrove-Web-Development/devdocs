# JavaScript Coding Standards

## Blocks and Curly Braces
`if`, `else`, `for`, `while`, and `try` blocks should always use braces, and always go on multiple lines. The opening brace should be on the same line as the function definition, the conditional, or the loop. The closing brace should be on the line directly following the last statement of the block.

```javascript
var a, b, c;
if ( myFunction() ) {
  // Expressions
} else if ( ( a && b ) || c ) {
  // Expressions
} else {
  // Expressions
}
```
## Enqueueing Scripts
All scripts should be registered using [wp_register_script()](https://developer.wordpress.org/reference/functions/wp_register_script/) in the wp_enqueue_scripts action. Scripts should be enqueued only if they are required on the loaded page. [See Template Specific Scripts](#markdown-header-template-specific-scripts) below.

Dependencies ( ex: jQuery, Modernizr ) should not be enqueued directly - they should be added to the dependency array of the dependent script.

## Template Specific Scripts
Scripts that need to be to be available on the whole website should be enqueued in functions.php, but scripts specific to a template should be enqueued in that template.

For example, you might need flexbox on the home page and a few other templates, but not every page of the website.  In this case, flexbox should be registered in functions.php, but only enqueued in the template files.

```php
<?php // page-with-slideshow.php

add_action( 'wp_enqueue_scripts', function(){
	wp_enqueue_script( 'flexbox' );
});

get_header();

... loop and stuff...
```

Just make sure your `add_action()` call is before `wp_head()` if the script should be loaded in the header.  Usually this is in header.php, so your add_action() should be before `get_header()` in your template file.

In early versions of WP, scripts could not be enqueued after wp_head().  Since version 3.3, scripts can be loaded after wp_head(), as long as they are registered to be enqueued in wp_footer().

## Inline Scripts
See https://developer.wordpress.org/reference/functions/wp_add_inline_script/

## Bootstrap
If the Bootstrap data attribute API is used, bootstrap.js should be enqueued directly.

If a script uses Bootstrap functions, bootstrap.js should be added as a dependency

## Modernizr
[WIP] This section may be outdated.

If you need to use modernizr, add modernizr as a dependency to the script using it.

Gulp is setup to detect what modernizr tests are being used by files in /library/js/src and to compile a minified modernizr.js that includes only what is necessary.  If you need the optional Modernizr API methods, you will need to add those to the options array in gulpfile.js.


## IIFE
NOTE: This does not apply to ES6, as the module structure provides encapsulation.

JavaScript scripts should be wrapped in an immediately invoked function expression, like this:

```js
;(function ( $, window, document, undefined ) {
	// your code here
	// you can use $ instead of jQuery
})( jQuery, window, document );
```
There’s a [good article](IIFE) about what these are by Ben Alman.


[IIFE]: http://benalman.com/news/2010/11/immediately-invoked-function-expression/

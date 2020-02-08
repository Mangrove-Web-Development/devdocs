---
parent: Coding Standards
---

# PHP Coding Standards

## Avoid Code Noise
[WIP] This section needs some explanation. The concept is covered well somewhere
in [this video](https://www.youtube.com/watch?v=ZsHMHukIlJY), but it's far from
succinct.
[WIP] This section should probably be moved to the general standards doc.

**Bad**
```php
<?php if( $case ){ ?>
  <?php while( $thing ){ ?>
    <div class="content">
      <?php the_content() ?>
    </div>
  <?php } ?>
<?php } ?>
```

**Good**
```php
<?php
if( $case ):
  while( $thing ): ?>
    <div class="content" ><?php
      the_content() ?>
    </div><?php
  endwhile;
endif; ?>
```


## Indentation
[WIP] This section should probably be moved to the general standards doc.

Indentation should reflect logical structure. If you have a block of code
that would be more readable if things are aligned, use spaces for alignment.

For associative arrays, values should start on a new line. Note the comma after the last array item: this is recommended because it makes it easier to change the order of the array, and makes for cleaner diffs when new items are added.

```
$my_array = array(
  'foo'   => 'somevalue',
  'foo2'  => 'somevalue2',
  'foo3'  => 'somevalue3',
  'foo34' => 'somevalue3',
);
```

### Don't Indent for `<?php` Tags
`<?php` tags are not part of logical structure; do not indent just for `<?php`
tags.

**Bad**
```php
<div>
  <?php
    echo 'somethingsomething';
  ?>
</div>
```

[WIP] These "Good" examples need team review. I generally prefer (#1). -- Jonathan

**Good**
```php
// Good (#1)
<div><?php
  echo 'somethingsomething'; ?>
</div>

// Good (#2)
<div>
  <?php
  echo 'somethingsomething';
  ?>
</div>
```

### Brace Style and Alternate Syntax
Logical block opening and closing tokens should always be at the start of the line.
Alternate syntax is preferred over brace syntax.

**Bad**
```php
<?php if( $condition ): ?>
  <p>Lorem ipsum...</p>
<?php endif; ?>
```

**Good**
```php
<?php
if( $condition ): ?>
  <p>Lorem ipsum</p><?php
endif; ?>
```

## Namespaces
WordPress core does not use namespaces, as WordPress predates the namespace feature added in PHP 5.3, and still supports older PHP versions.

WPE and most servers use at least PHP 5.3, so the starter theme and some newer projects make use of namespacing.

Some especially relevant points are included below. Of course, you can also read the [PHP docs](http://php.net/manual/en/language.namespaces.php), or a friendly article like [this one](https://torquemag.io/2015/01/using-namespaces-wordpress-development/) ( note: the author mistakenly identifies backslashes as forward slashes ).

### Using Namespaces
A namespaced file will start with the namespace declaration.

```php
<?php
namespace Mangrove;
```

This must be the first statement in the PHP file, and all code within the file will be working within that namespace.  Any code not within a namespace is within the global namespace.


### Functions in Namespaces
When calling a function within a namespace, PHP will use the function of that name with the current namespace.  If it does not exist within the current namespace, it will use the function defined in the global namespace.

```php
// global-namespace.php
<?php

function foo(){
echo 'foo';
}

function bar(){
	echo 'bar';
}
```

```php
// mangrove-namespace.php
<?php namespace Mangrove;

require( 'global-namespace.php');

foo();  // outputs ‘mangrove foo’
bar();  // outputs ‘bar’

function foo(){
	echo 'mangrove foo';
}
```

If you are within a namespace, but you specifically want to use a function from a different namespace, you need to use the function’s fully qualified name; i.e. the namespace path.  This is similar to a directory path, using the backslash as a separator.  To access the global, or root, namespace, just use a single backslash before the function name.

```php
// mangrove-namespace.php
<?php namespace Mangrove;
require( 'global-namespace.php');

\foo(); // outputs 'foo'
foo();  // outputs 'mangrove foo'

function foo(){
	echo 'mangrove foo';
}
```
### Classes in Namespaces
Classes in namespaces do not default to the global namespace if it is not defined in the current namespace.  You must always use the fully qualified class name if you are not within the namespace it was defined.

```php
<?php
Namespace Mangrove;

new WP_Query( … );  // error, class does not exist

new \WP_Query( … ); // this works
```

### Callable
Some functions, like add_action() take a callable argument.  This is usually the string name of the function you want called.

```php
// gloabl-namespace.php
<?
add_action( 'wp_enqueue_scripts', 'register_styles' );

function register_styles(){
	wp_register_style( … );
	wp_register_style( … );
}
```

For functions defined within a namespace, you must always include the fully qualified name.

```php
// mangrove-namespace.php
<?php namespace Mangrove;
add_action( 'wp_enqueue_scripts', 'Mangrove\register_styles' );

function register_styles(){
	wp_register_style( … );
	wp_register_style( … );
}
```

## Images
[WIP] This, or parts of this, section should probably be moved.

### File Format
Generally, JPEG format images are the smallest and should be used in most cases. PNG and GIF should only be used when transparency is required, or when the graphic has a very limited color palette which results in smaller file size in this format.

### Source
Do not use the ‘full’ image size. This will return the original file uploaded, which may be extremely large and result in poor page load performance.

### Responsive
There are new HTML5 attributes on the <img> tag for loading appropriately sized image files.

The srcset attribute gives the browser varying image sources to choose from.  Use the wp_get_attachment_image_srcset() function to get the URLs to all available image sizes.

```php
<?php
$src = wp_get_attachment_image_src( $attachment_id, $size );
$srcset = wp_get_attachment_image_srcset( $attachment_id, $size ); ?>
<img
	alt="My Example Image"
	src="<?php echo $src[0] ?>"<?php
	if( $srcset ): ?>
		srcset="<?php echo $srcset ?>"<?php
	endif; ?>
/>
```

If the image is to be displayed at 100vw, that’s all you need.  However, if the image will display as less than 100vw on any device, you also need to include the sizes attribute.  This takes a comma separated list of display sizes, and can include media queries.

```php
<?php
$src = wp_get_attachment_image_src( $attachment_id, $size );
$srcset = wp_get_attachment_image_srcset( $attachment_id, $size );
?>
<img
	alt="My Example Image"
	src="<?php echo $src[0] ?>"<?php
	if( $srcset ): ?>
		srcset="<?php echo $srcset ?>"
		sizes="(min-width: 40em) 40em, 100vw"<?php
	endif; ?>
/>
```

If you want to know more about these attributes and the new <picture> element used for more advanced responsiveness, see [A List Apart: Responsive Images In Practice].

You can also see this [WordPress announcement] about the related WordPress functions.

[A List Apart: Responsive Images In Practice]: http://alistapart.com/article/responsive-images-in-practice
[WordPress announcement]: https://make.wordpress.org/core/2015/11/10/responsive-images-in-wordpress-4-4/]


## The Loop
### If ( have_posts() ) Not Required for Single
The if( have_posts() ): check is not necessary on pages that display a single post: e.g. single.php or page.php.  If a query for a single post results in no post, the 404 template is loaded instead of the single template.

See [Stack Exchange discussion](https://wordpress.stackexchange.com/questions/117219/why-should-i-put-ifhave-posts-is-whilehave-posts-not-enough)

### While( have_posts() ) Always Required
Even if there is only a single post to display, as on single.php or page.php, calling the_post() by itself is not enough, because have_posts() does some cleanup after the last post is displayed.

Technically, simply calling have_posts() after you’re done with the_post() is probably enough, but it’s probably better to conform to the standard practice of using while( have_posts() ).

See [ThemeShaper article](https://themeshaper.com/2013/09/03/a-proper-loop/)
See $this->in_the_loop in have_posts() [WP_Query source](https://developer.wordpress.org/reference/classes/wp_query/#source-code)

Note to self: Consider adding this information to WP Codex / Theme developer docs.

## ACF Image Field
always output image id or object, not URL, so WordPress functions can be used to get correct image size.

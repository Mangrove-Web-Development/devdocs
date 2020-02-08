---
nav_order: 2
title: Coding Standards
---
# Mangrove Coding Standards

The purpose of the Mangrove Coding Standards is to create a baseline for
collaboration and review within various aspects of Mangrove Web Development,
from core code to themes to plugins.

Coding standards help avoid common coding errors, improve the readability of
code, and simplify modification.

Following the standards means anyone will be able to understand a section of
code and modify it, if needed, without regard to when it was written or by whom.


## Readable Code
The code itself should be easy to read and understand, generally rendering
comments unnecessary. If a block of code is not easy to understand, naming may
need to be improved, or it may need to be better abstracted into separate functions.

There are rare cases in which code can not be made more clear. In these
instances, write comments and keep them up to date with the code.

## Avoid Extra Comments
Unnecessary comments make the code harder to understand and maintain. Only use
comments if the code cannot be made self-explanatory.

[Suggested Reading: Thoughts on Self-Documenting CSS](http://keithjgrant.com/posts/2017/06/self-documenting-css/)

```php
<?php
// bad
if ( have_posts() ) :
  /* Start the Loop */
  while ( have_posts() ) : the_post();
    /*
     * Include the Post-Format-specific template for the content.
     */
    get_template_part( 'components/post/content', get_post_format() );
  endwhile;

  the_posts_pagination();
else : ...
```

```php
<?php
// good
if ( have_posts() ) :
  while ( have_posts() ) : the_post();
    get_template_part( 'components/post/content', get_post_format() );
  endwhile;

  the_posts_pagination();
else : ...
```

## Spacing
* Install [EditorConfig](http://editorconfig.org) in your text editor to help
maintain project consistency.
* Use __2 spaces__ for indentation in all languages **except markdown**
    * Two-space indentation is not consistently recognized in all markdown rendering engines, so use 4 spaces instead.
* Use spaces for alignment.
* [WIP] from [AirBNB](https://github.com/airbnb/javascript#whitespace--after-blocks)
Leave a blank line after blocks and before the next statement.
* [WIP] from [AirBNB](https://github.com/airbnb/javascript#whitespace--padded-blocks)
Do not pad your blocks with blank lines.

```javascript
// bad
function bar() {

  console.log(foo);

}

// also bad
if (baz) {

  console.log(qux);
} else {
  console.log(foo);

}

// good
function bar() {
  console.log(foo);
}

// good
if (baz) {
  console.log(qux);
} else {
  console.log(foo);
}
```

### When to Indent
Code within logical blocks should be indented by one level more than the opening token, and the closing token should match the indent level of the opening token.

The open and closing tokens should be the first non-indent characters on their respective lines.
PHP opening tags do not start logical blocks, so they should not start indents.

```php
<div>
  <?php
  if( condition ):
    the stuff;
  else:
    the other stuff;
  endif; ?>
</div>
```

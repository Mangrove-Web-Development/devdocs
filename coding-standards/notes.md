---
title: WIP Notes
nav_order: -1
---

# Note for Future Content
Notes for future content of this document

Switch vs If..Elseif

See code in function the_masthead() SNP commit from 22 Feb 2016
Optimizing SVG
- https://web-design-weekly.com/2014/10/22/optimizing-svg-web/
- https://sarasoueidan.com/blog/svg-coordinate-systems/
- https://css-tricks.com/svg-use-with-external-reference-take-2/

### DRY Coding ( Don’t Repeat Yourself )
Large blocks of repeating code are difficult to read and maintain.  Any time you’re copy-pasting code to repeat something, you’d probably be better off using some kind of loop.

For example, the following is the code for a set of filter buttons.  Because it’s such a large block of code, it’s hard to be sure whether every iteration is the same, and making an adjustment would require editing each element individually.

```php
// template-team.php from SNP 25 Feb 2016
<section>
	<h5 class="team-location">
		<a class="filter" data-filter="all">
			<svg version="1.1" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" x="0px" y="0px" width="15px" height="14px" viewBox="0 0 15 14" enable-background="new 0 0 15 14" xml:space="preserve"><polygon fill="#DADADA" points="5.795,12.843 0.28,6.897 1.747,5.537 5.801,9.909 13.256,1.94 14.717,3.307"/></svg>
			All Locations
		</a>
		<a class="filter" data-filter=".sf">
			<svg version="1.1" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" x="0px" y="0px" width="15px" height="14px" viewBox="0 0 15 14" enable-background="new 0 0 15 14" xml:space="preserve"><polygon fill="#DADADA" points="5.795,12.843 0.28,6.897 1.747,5.537 5.801,9.909 13.256,1.94 14.717,3.307"/></svg>
			San Francisco
		</a>
		<a class="filter" data-filter=".nyc">
			<svg version="1.1" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" x="0px" y="0px" width="15px" height="14px" viewBox="0 0 15 14" enable-background="new 0 0 15 14" xml:space="preserve"><polygon fill="#DADADA" points="5.795,12.843 0.28,6.897 1.747,5.537 5.801,9.909 13.256,1.94 14.717,3.307"/></svg>
			New York
		</a>
		<a class="filter" data-filter=".dub">
			<svg version="1.1" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" x="0px" y="0px" width="15px" height="14px" viewBox="0 0 15 14" enable-background="new 0 0 15 14" xml:space="preserve"><polygon fill="#DADADA" points="5.795,12.843 0.28,6.897 1.747,5.537 5.801,9.909 13.256,1.94 14.717,3.307"/></svg>
			Dublin
		</a>
		<br class="hidden-xs"/>
		<a class="filter" data-filter=".midwest">
			<svg version="1.1" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" x="0px" y="0px" width="15px" height="14px" viewBox="0 0 15 14" enable-background="new 0 0 15 14" xml:space="preserve"><polygon fill="#DADADA" points="5.795,12.843 0.28,6.897 1.747,5.537 5.801,9.909 13.256,1.94 14.717,3.307"/></svg>
			Midwest
		</a>

		<a class="filter" data-filter=".portland">
			<svg version="1.1" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" x="0px" y="0px" width="15px" height="14px" viewBox="0 0 15 14" enable-background="new 0 0 15 14" xml:space="preserve"><polygon fill="#DADADA" points="5.795,12.843 0.28,6.897 1.747,5.537 5.801,9.909 13.256,1.94 14.717,3.307"/></svg>
			Portland
		</a>

		<a class="filter" data-filter=".denver">
			<svg version="1.1" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" x="0px" y="0px" width="15px" height="14px" viewBox="0 0 15 14" enable-background="new 0 0 15 14" xml:space="preserve"><polygon fill="#DADADA" points="5.795,12.843 0.28,6.897 1.747,5.537 5.801,9.909 13.256,1.94 14.717,3.307"/></svg>
			Denver
		</a>
	</h5>
</section>
```

This can be refactored to:
```php
<section class="team-location-container">
	<h5 class="team-location">
		<?php
		$location_filters = array(
			'all'  => 'All Locations',
			'.sf'  => 'San Francisco',
			'.nyc' => 'New York',
			'.dub' => 'Dublin',
			'.midwest' => 'Midwest',
			'.portland' => 'Portland',
			'.denver'   => 'Denver',
		);
		foreach( $location_filters as $class => $location ): ?>
			<a class="filter" data-filter="<?php echo $class ?>">
				<svg> …</svg>
				<?php echo $location ?>
			</a><?php
		endforeach;
?>
	</h5>
</section>
```

This is much easier to understand and update.

## Naming / Self Documenting Code / Writing for Readability / Code Organization
page-team.js in SNP Feb 26 commit $(window).load()

high level ( abstract, human readable ) overview at top of file
functions.php in mgtemplate
javascript
php template file
page structure, functions for components
the_ function prefix

## Separation of Concerns
JavaScript libraries that hook directly into markup are difficult to debug. It’s much easier to tell what’s going on when javaScript functions are explicitly called in the javaScript file.  Similarly, elements with many style classes can be hard to work with.

HTML classes should be used to identify the type of element, not the style of an element.
For example:
```html
<a
class="navbar-brand <?php if (is_front_page()) {?>animated wow fadeIn<?php } ?>"
title="<?php echo get_bloginfo('description'); ?>"
href="<?php echo home_url(); ?>"
>
<h1><?php bloginfo('name');?></h1>
</a>
```
Should instead be

```html
<a
class="navbar-brand"
title="<?php echo get_bloginfo('description'); ?>"
href="<?php echo home_url(); ?>"
>
<h1><?php bloginfo('name');?></h1>
</a>
```
```scss
// nav.scss
.front-page .navbar-brand {
	@extend .animated
	@extend .wpw
	@extend .fadeIn
}
```


### Code Example
```php
<div class="wrapper">
<?php if ( is_home() && ! is_front_page() ) : ?>
  <header class="page-header">
    <h1 class="page-title"><?php single_post_title(); ?></h1>
  </header>
<?php else : ?>
  <header class="page-header">
    <h2 class="page-title"><?php _e( 'Posts' ); ?></h2>
  </header>
<?php endif; ?>
  <main role="main">
  <?php
  if ( have_posts() ) :
    while ( have_posts() ) : the_post();
      get_component('post/content');
    endwhile;
    the_posts_pagination();
  else :
    get_component('post/content-none');
  endif;
  ?>
  </main>
</div>
```

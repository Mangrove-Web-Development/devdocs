---
title: Images
parent: Coding Standards
---
# Images

## File Format
Generally, JPEG format images are the smallest and should be used in most cases. PNG and GIF should only be used when transparency is required, or when the graphic has a very limited color palette which results in smaller file size in this format.

## Source
Do not use the ‘full’ image size. This will return the original file uploaded, which may be extremely large and result in poor page load performance.

## Responsive
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

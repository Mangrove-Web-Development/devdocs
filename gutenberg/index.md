---
nav_order: 7
title: Gutenberg
has_children: true
---
# Gutenberg

To take advantage of JavaScript developer tools, make sure to set `SCRIPT_DEBUG` in `wp-config.php`.

```php
<?php
define('SCRIPT_DEBUG', true );
```

## Attributes

Gutenberg blocks use _attributes_ to save data.

### Declaring
Attributes must be declared in the `registerBlockType` function call.

```js
// src/index.js
registerBlockType( 'mangrove/example', {
  title: 'Basic Example',
  attributes: {
    renderCount: {
      type: 'number',
    },
  },
  ...
} );
```

The attribute type must be declared. Valid types[^1] are:
* null
* boolean
* object
* array
* number
* string
* integer

[^1]: https://developer.wordpress.org/block-editor/developers/block-api/block-attributes/#attribute-type-validation


### Accessing
The block component will receive an attributes object as one of the props.

```js
// src/example/index.js
export default function Example( props ){
  const { attributes: { renderCount } } = props
  return( <p>`This component has rendered ${renderCount} times!`</p> )
}
```

### Saving
Use setAttributes to update attributes. This will save the changes when the post is saved.
Make sure you use the attribute name exactly as declared in `registerBlockType`, or it won't save.

```js
// src/example/index.js
export default function Example( props ){
  const {
    attributes: { renderCount },
    setAttributes,
  } = props
  setAttributes( { renderCount: renderCount + 1 } )
  return( <p>`This component has rendered ${renderCount} times!`</p> )
}
```

### Editing UI
With the `setAttributes` function, you can create any kind of UI within the block itself to
update the attributes.
However, that could be cumbersome and a lot of work.
See the next page about the Inspector Controls for an alternative.

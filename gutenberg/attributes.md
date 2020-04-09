---
parent: Gutenberg
title: Attributes
nav_order: 1
---

# Attributes

Gutenberg blocks use _attributes_ to save data.

## Declaring
Attributes must be declared in the `registerBlockType` function call.

```jsx
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

The attribute type must be declared. [Valid types](https://developer.wordpress.org/block-editor/developers/block-api/block-attributes/#attribute-type-validation) are:
* null
* boolean
* object
* array
* number
* string
* integer


## Accessing
The block component will receive an attributes object as one of the props.

```jsx
// src/example/index.js
export default function Example( props ){
  const { attributes: { renderCount } } = props
  return( <p>`This component has rendered ${renderCount} times!`</p> )
}
```

## Saving
Use setAttributes to update attributes. This will save the changes when the post is saved.
Make sure you use the attribute name exactly as declared in `registerBlockType`, or it won't save.

```jsx
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

## Editing UI
With the `setAttributes` function, you can create any kind of UI within the block itself to
update the attributes.
However, that could be cumbersome and a lot of work.
See the next page about the [Inspector Controls](/gutenberg/inspector-controls) for an alternative.

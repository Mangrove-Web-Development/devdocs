---
parent: Gutenberg
title: Media
nav_order: 3
---

# Media
Use the `MediaUploadCheck` and `MediaUpload` components for handling attached media in custom blocks.

`MediaUploadCheck` checks whether the logged in user has permission to upload media.
If so, the component children are rendered.
Otherwise, the `fallback` is rendered.
This can be placed inside both the block component and/or within the InspectorControls.

`MediaUpload` uses a `render` property instead of rendering its children.
This provides the `open` function, which opens the media library modal.
Again you can use this anywhere in your block component - in or outside the InspectorControls.
When the media is selected, `onSelect` will be called, passing an object with all the media details.
I recommend you save just the ID of your media file as an attribute.

```js
// src/example/index.js
import {
  InspectorControls,
  MediaUploadCheck,
  MediaUpload,
} from '@wordpress/block-editor'
import {
  Button,
  PanelBody,
  PanelRow
} from '@wordpress/components'

export default function Example( props ){
  const {
    attributes,
    setAttributes
  } = props
  const saveImage = ({ id }) => {
    setAttributes( { image: id } )
  }
  // This was getting unwieldy, so I split the editor block and the inspector controls into
  // separate components.
  return (
    <>
      <EditorBlock {...attributes} />
      <Inspector saveImage={ saveImage } />
    </>
  )
}

function EditorBlock( { image } ){
  return(
    <p>{`The image ID is ${image}`}</p>
  )
}

function Inspector( { saveImage } ){
  const mediaFallback = <p>To edit the image, you need permission to upload media.</p>
  return (
    <InspectorControls>
      <PanelBody title="Example Image">
        <MediaUploadCheck fallback={ mediaFallback }>
          <PanelRow>
            <p>
              Any content here only displays if the user has permission to upload media.
              Otherwise, the content in the fallback property will be displayed.
            </p>
          </PanelRow>
          <PanelRow>
            <MediaUpload
              title="Title for the media library modal."
              allowedTypes={['image']}
              onSelect={ saveImage }
              render={
                ({open}) => (
                  <Button isDefault onClick={open} >Select Image File</Button>
                )
              }
            />
          </PanelRow>
        </MediaUploadCheck>
      </PanelBody>
    </InspectorControls>
  )
}
```

You may have noticed that the above code saves and displays the image ID,
but it doesn't actually display the image!
Since you only save the ID,
you have to fetch the rest of the image data when you render the component with `apiFetch`.
This is an AJAX call to the WP JSON API, which means you're going to have to use the `useEffect`
React hook to deal with the asynchronous data fetching.

I will show you how to do this. Better yet, I might make a reusable component that handles this for you; we'll see. But not now. I need to get away from the computer now.

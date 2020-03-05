---
nav_order: 6
title: MGTemplate
---
# MGTemplate

[WIP] This section is a work in progress. These are just some notes about what should be added.

- This is the standard framework for all Mangrove sites.
- Older sites may have an older setup that isn't up-to-date.
- New sites will be setup by cloning this WPEngine install.
- Includes Docker local development setup.
- Tracks theme, mangrove plugin.
- Doesn't track WordPress files.
- How to edit CSS/JS

## Animations

Our theme utilizes [sal.js](https://github.com/mciastek/sal) as a lightweight scroll animation library. Using this, you can easily add various on-scroll animations with options for type, duration, delay, and easing. For example, the title, text, and button elements within our hero building block (seen in action [here](http://mgtemplate.wpengine.com/)) use these shared settings: `data-sal="slide-up" data-sal-duration="400" data-sal-easing="ease-out"`, while each subsequent element uses a slighly larger `data-sal-delay` (between 300-700) to create a staggered slide-up effect. Please refer to the [documentation](https://github.com/mciastek/sal) for full usage options.

We also utilize [lazysizes](https://github.com/aFarkas/lazysizes) to lazyload both images and background images. This can be enabled by adding the class `.lazyload` to the desired element, and then setting a `data-src` rather than a `src` attribute for `<img>` elements, and `data-bg` rather than `style="background: url();"` for background images. For example: `<img class="lazyload" data-src="URLHERE" alt="Alt Text" />` or `<div class="lazyload" data-bg="URLHERE"></div>`. Elements using lazysizes will fade-in using an animation set in `/sass/vendor/lazyload/_lazyload.scss`. 

The background image in our hero building block uses a progressive loading effect to initially load a low resolution version and then fade-in the higher resolution version for better on-load experience. When building hero elements that do not use the hero building block (custom templates, etc.) please try and replicate this functionality.

## Grid System

Our grid system is a 12 column maximum system that utilizes two main elements: the `.grid` and the `.grid__column`. `.grid` is the wrapper element, with `.grid__column` elements nested directly inside. Varying widths and/or offests of the grid columns can be set using size and offset utility classes (`.u-size-XofY` and `.u-offset-XofY`). You can enable different widths and offsets at various breakpoints (set in `/sass/settings/_variables.scss`) using size class modifiers that match the breakpoint names set in the variables. 

For example from a mobile-first perspective `.grid__column .u-size-1of2--md .u-size-1of3--lg`  would create a column that is 100% width until it hits the 'md' breakpoint, then 50% width until it hits the 'lg' breakpoint, and then 33.33% width on any screen widths larger than that. Default grid padding can be set in the same `variables.scss` file mentioned above. If grids with multiple padding sizes are required for your site design, you can add additional size modifiers in `/sass/components/_grid.scss`, for example `.grid--lg` within that file. as You can see this in action on our [styleguide](http://mgtemplate.wpengine.com/styleguide/).

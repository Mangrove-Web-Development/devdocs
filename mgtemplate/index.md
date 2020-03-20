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


## Theme Scripts
All `*.js` files in the `js` directory of themes based on _mgstarter will have a corresponding output file in the `dist` directory. To use these scripts in WordPress, they must be registered, and then enqueued.

Note: only scripts in the `js` directory will be output separately. Files in subdirectories of `js` will not be output.

E.g.:
```sh
js/global.js                       # Outputs to dist/global.hash.js.
js/example.js                      # Outputs to dist/example.hash.js.
js/example-helpers/first-helper.js # Does not output to dist.
```

### Register Scripts

Register scripts in the `js` directory in the `register_scripts` function in `functions.php`.
Use the `register` method of the `Script_Registry` abstract class[^1].

```php
<?php
function register_scripts() {
    ...
    Script_Registry::register( $handle, $dependencies, $options );
    ...
}
?>
```

`Script_Registry::register` takes three arguments:
* `$handle` - `(string)` Handle for script.
    Must match the filename of the source file, excluding the `.js` file extension.
    Used to enqueue or add script as dependency.
* `$dependencies` - `(array)` Optional. Array script handles this script depends on.
    Defaults to empty array.
* `$options` - `(array)` Optional. Allows overriding arguments sent to [wp_register_script](https://developer.wordpress.org/reference/functions/wp_register_script/).
    * `src` - `(string|bool)` Defaults to compiled JS file in `dist` directory corresponding to `$handle`.
    * `version` - `(string|bool|null)` Version number is not needed for cache-busting due to hashed file names.
         Default `null`.
    * `in_footer` - `(bool)` Whenever possible, scripts should be enqueued in the footer.
         Default `true`.

[^1]: [WIP] Link to PHP abstract class explanation. [PHP Docs](https://www.php.net/manual/en/language.oop5.abstract.php)

### Webpack External Scripts
Most dependency scripts will either be node modules managed with npm,
or custom scripts within the theme `js` directory.
These can simply be included by using the `import` syntax in the main JavaScript files, and
they will be included the the output bundles in `dist`.
This is the preferred method to include dependencies, however,
there are instances when a dependency can or should not be bundled.
For example, many plugins rely on jQuery, and attempting to bundle jQuery can cause issues.

In this case, the script must be added to the [`externals`](https://webpack.js.org/configuration/externals/) object in `webpack.config.js`.
Then, the script must be registered with WordPress.
If it's included in WordPress by default, it is already registered.
Otherwise, use `Script_Registry::register` or `wp_register_script`.
Then, you can add it to the `$dependencies` array of the dependent scripts and
`import` it as if it was a node module.

E.g. jQuery [^1]
```js
// webpack.config.js
externals: {
  jquery: "jQuery",
},
```
```php
<?php // functions.php
Script_Registry::register( 'jquery', [], ['src'=>''] );
Script_Registry::register( 'global' );
```
```js
// global.js
import $ from 'jquery'

```
[^1]: This is a somewhat contrived example. jQuery is already 

## Animations

Our theme utilizes [sal.js](https://github.com/mciastek/sal) as a lightweight scroll animation library. Using this, you can easily add various on-scroll animations with options for type, duration, delay, and easing. For example, the title, text, and button elements within our hero building block (seen in action [here](http://mgtemplate.wpengine.com/)) use these shared settings: `data-sal="slide-up" data-sal-duration="400" data-sal-easing="ease-out"`, while each subsequent element uses a slighly larger `data-sal-delay` (between 300-700) to create a staggered slide-up effect. Please refer to the [documentation](https://github.com/mciastek/sal) for full usage options.

We also utilize [lazysizes](https://github.com/aFarkas/lazysizes) to lazyload both images and background images. This can be enabled by adding the class `.lazyload` to the desired element, and then setting a `data-src` rather than a `src` attribute for `<img>` elements, and `data-bg` rather than `style="background: url();"` for background images. For example: `<img class="lazyload" data-src="URLHERE" alt="Alt Text" />` or `<div class="lazyload" data-bg="URLHERE"></div>`. Elements using lazysizes will fade-in using an animation set in `/sass/vendor/lazyload/_lazyload.scss`. 

The background image in our hero building block uses a progressive loading effect to initially load a low resolution version and then fade-in the higher resolution version for better on-load experience. When building hero elements that do not use the hero building block (custom templates, etc.) please try and replicate this functionality.

## Grid System

Our grid system is a 12 column maximum system that utilizes two main elements: the `.grid` and the `.grid__column`. `.grid` is the wrapper element, with `.grid__column` elements nested directly inside. Varying widths and/or offests of the grid columns can be set using size and offset utility classes (`.u-size-XofY` and `.u-offset-XofY`). You can enable different widths and offsets at various breakpoints (set in `/sass/settings/_variables.scss`) using size class modifiers that match the breakpoint names set in the variables. 

For example from a mobile-first perspective `.grid__column .u-size-1of2--md .u-size-1of3--lg`  would create a column that is 100% width until it hits the 'md' breakpoint, then 50% width until it hits the 'lg' breakpoint, and then 33.33% width on any screen widths larger than that. Default grid padding can be set in the same `variables.scss` file mentioned above. If grids with multiple padding sizes are required for your site design, you can add additional size modifiers in `/sass/components/_grid.scss`, for example `.grid--lg` within that file. as You can see this in action on our [styleguide](http://mgtemplate.wpengine.com/styleguide/).

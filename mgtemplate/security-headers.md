---
title: Security Headers
parent: MGTemplate
nav_order: 10
---
# Security Headers

Security headers not set by WPEngine are added by the theme.
Find these in the `add_security_headers` function in `functions.php`.
These headers are restrictive, so you may need to adjust them for your project.

## Strict-Transport-Security
The HTTP Strict-Transport-Security (HSTS) header enforces the use of HTTPS.
**If your project domain or any subdomains require access via HTTP,
read the [MDN docs][MDN HSTS] to understand this header.**

A `preload` directive can be added to this header for better, more reliable security.
However, this has long-term effects that are difficult to reverse,
so it is not included by default,
and should only be used after reading the documentation at [hstspreload.org][] and
discussing this with the project manager and/or client.


[MDN HSTS]: https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Strict-Transport-Security
[hstspreload.org]: https://hstspreload.org/

## Content-Security-Policy
The Content-Security-Policy header controls what types of resources may be loaded on the page,
and where they can be loaded from.
This applies to all types of resources, from scripts and stylesheets to images and other media.

Each resource type can be individually specified,
but the default template uses `default-src` to apply to all resource types.

`self` allows loading resources from the same origin.

`unsafe-inline` allows the use of inline scripts, styles, etc.
This is considered unsafe and not recommended,
but is currently required for the theme and plugins to work.

Additional allowed origins are specified in the `$allowed_src_origins` array
and added to the security header.
You will likely need to edit this list for your project.

```php
$allowed_src_origins = implode( ' ', [
  '*.typekit.net',
  '*.googletagmanager.com',
  '*.googleapis.com',
  '*.google-analytics.com',
]);
header("Content-Security-Policy: default-src 'self' 'unsafe-inline' $allowed_src_origins;");
```

Additionally, the `X-Content-Security-Policy` is set to `'self'`.
This is a deprecated version of the Content-Security-Policy header that is only used by
Internet Explorer.
This setting breaks the site on IE, but this browser is no longer supported.
If IE support is required, you will need to adjust this header.

For more information, see [MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/CSP)
and [content-security-policy.com](https://content-security-policy.com/)

## Feature-Policy
The Feature-Policy header controls which browser features are allowed by which origins.
By default, the MGTemplate theme completely disables a few features.
If any of these features are needed, they should be removed from the `$disabled_features` list
and a specific header for that feature added.

For example, you may want to allow geolocation for Google Maps:
```php
// This is not a real example, Maps may require different header settings.
header( "Feature-Policy: geolocation 'self' maps.google.com", false );
```
Make sure to set the `$replace` parameter of
[the `header` function](https://www.php.net/manual/en/function.header.php)
to `false` so you don't overwrite the other Feature-Policy headers.

---
title: WordPress: How to Add a Trailing Slash to the Homepage's Canonical URL
date: 2019-07-18 12:03
category: WordPress
tags: SEO
author: Josh
path: "/blog/wordpress-canonical-url-homepage/"
---

If you're using the [Yoast SEO plugin](https://wordpress.org/plugins/wordpress-seo/) for WordPress, it will add [canonical URL metatags](https://moz.com/learn/seo/canonicalization) on your WordPress pages. The problem is that, if you WordPress site is in a subdirectory, the plugin might use the wrong canonical URL for the homepage.

## Explanation

In most cases, for WordPress to be served from a subdirectory (like `example.com/blog/`), it has to sit in a physical subdirectory. The slash on the end of a URL indicates that it's a physical directory. If you try to leave the trailing slash off, the server will `301` redirect you to the URL with a trailing slash.

The Yoast SEO plugin leaves off the trailing slash on the home page canonical URL if your WP site sits in a directory and has certain permalink settings (which are unrelated to the root URL of the site). That means search engines will list the wrong URL in the <abbr title="Search Engine Results Pages">SERPs</abbr>.

## How to Fix It

If your WordPress' site's homepage canonical URL does <em>not</em> have a trailing slash, this code in the [theme's `functions.php` file](https://codex.wordpress.org/Functions_File_Explained) should fix it:

```php
function wpseo_canonical_home_url_fix( $canonical_url ) {
      // Add a trailing slash if it's missing in front page
     if ( is_front_page() ){
         return trailingslashit( $canonical_url );
     }
     return $canonical_url;
}
add_filter( 'wpseo_canonical', 'wpseo_canonical_home_url_fix' );
```

There is almost never a case where the home page URL of your WordPress site <em>won't</em> have a trailing slash on it. Sometimes browsers will hide the trailing slash, but it's still there. If you can't see it in the browser's address bar, copy the URL from the browser and paste it in a text editor to see the real URL. Or open the browser console (right-click and "Inspect Element" in Firefox), click on the "console" tab, and type this code to see the page's real URL:

```text
window.location.href
```

![`window.location.href` in Firefox](/files/window-location-href.png)

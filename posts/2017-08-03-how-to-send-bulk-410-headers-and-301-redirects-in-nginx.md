---
title: How to Send Bulk 410 Headers and 301 Redirects in Nginx
date: 2017-08-03
author: Josh
path: "/blog/how-to-send-bulk-410-headers-and-301-redirects-in-nginx/"
---

<a href="https://www.google.com/webmasters/">Google's Webmaster Tools</a> warns you when there are a lot of <em>404 Not Found</em> pages found on your website. If you've just deleted a lot of spam from a site, Google might keep recrawling those URLs as long as they send 404 headers.

A 404 header means <em>Not Found</em>.
A 410 header means <em>Gone</em>.

If you want to stop Google from adding those removed pages back to Google Webmaster Tools, you can send 410 headers for the removed URLs.

It took me a while to figure out how to do this with nginx, but I finally came up with this solution:

Create a new file called `/etc/nginx/header-maps.conf`. In that file map each <em>gone</em> URL to a variable, in this case the number 1 (chosen arbitrarily).

```nginx
map $request_uri $gone_var {
	/path-one		1;
	/path-two		1;
	/path-three		1;
	/path-four		1;
}
```

Then in your main conf file for your domain, like `/etc/nginx/sites-available/example.com` (replacing `example.com` with your domain):

```nginx
include header-include.conf;
server {
	# other things here...

	if ($gone_var) {
		return 410 $gone_var;
	}

	# other things here...
}
```

You can also map redirects in the same file, for example:

```nginx
# header-include.conf
map $request_uri $gone_var {
	/path-one		1;
	/path-two		1;
	/path-three		1;
	/path-four		1;
}

map $request_uri $redirect_uri {
	/path-five		/path-five.html;
	/path-six		/path-six.html;
	/path-seven		/path-seven.html;
}
```

```nginx
# Your domain's conf file
include header-include.conf;
server {
	# other things here...

	# if there is a mapped $gone_var set for the current path
	if ($gone_var) {
		return 410 $gone_var;
	}

	# if there is a $redirect_uri set for the current URI:
	if ($redirect_uri) {
		return 301 $redirect_uri;
	}

	# other things here...
}
```

If you get an error about `map_hash_bucket_size` being to small, open the `/etc/nginx/nginx.conf` file (or wherever the `http` block lives) and increase it something like this: `map_hash_bucket_size 256`

<img src="/files/map_hash_bucket_size-nginx.png" alt="map_hash_bucket_size nginx" />

More information:

<ul>
  <li><a href="http://nginx.org/en/docs/http/ngx_http_map_module.html">Module ngx_http_map_module</a></li>
  <li><a href="http://nginx.org/en/docs/http/ngx_http_rewrite_module.html">Module ngx_http_rewrite_module</a></li>
  <li><a href="https://www.bjornjohansen.no/nginx-redirect">Nginx redirects</a></li>
  <li><a href="https://www.digitalocean.com/community/tutorials/how-to-use-nginx-s-map-module-on-ubuntu-16-04">How to Use Nginx's map Module on Ubuntu 16.04</a></li>
</ul>

I don't know yet how this affects performance, but it solved my current problem of sending 410 headers on a couple of hundred URLs.

If it doesn't work for you or if you have any suggestions for improving this idea, please comment below.

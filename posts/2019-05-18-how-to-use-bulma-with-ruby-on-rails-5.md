---
title: How to use Bulma with Rails 5
date: 2019-05-18 20:29
category: Ruby
author: Josh
path: "/blog/bulma-rails-5/"
---

Using [Bulma CSS framework](https://bulma.io/) in Rails is pretty easy.

Add `bulma-rails` to your `Gemfile`. If you want to use [Bulma extensions](https://wikiki.github.io/), also add that gem.

```ruby
# check rubygems to see what the latest version is
gem 'bulma-rails', '~> 0.7.4'

# optional
gem 'bulma-extensions-rails'
```

Install the gems.

```text
$ bundle install
```

Then, after restarting the Rails server, import Bulma in your `application.scss`:

```scss
// import bulma and optionally the extensions
@import "bulma";
@import "bulma-extensions";
```

To override variables, check the [Bulma docs](https://bulma.io/documentation/customize/variables/). Each page there lists relevant variables at the bottom.

```scss
@import url('https://fonts.googleapis.com/css?family=Source+Code+Pro|Roboto+Slab|Open+Sans');

// override the Bulma variables here
$subtitle-line-height: 1.5;
$family-sans-serif: 'Open Sans', Helvetica, Arial, sans-serif;
$family-monospace: 'Source Code Pro', monospace;

// import bulma and optionally the extensions
@import "bulma";
@import "bulma-extensions";

// custom scss works here or in the relevant files
```

If it doesn't work for you, leave a comment in the [Code Self Study Forum](https://community.codeselfstudy.com/).

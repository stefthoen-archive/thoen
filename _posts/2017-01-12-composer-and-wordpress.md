---
layout: post
title:  "Composer and WordPress"
date:   2017-01-12 00:51:00 +0100
categories: php composer wordpress
---
I had some problems with recursively using Composer. I was trying to include one
of my own packages (a WordPress plugin) in a Composer project (a WordPress
website) and I got some errors. 

I forgot what kind of errors I got, because it has been a while ago since I
last tried to get it to work, but I had a [twitter
conversation](https://twitter.com/baardbaard/status/819119819614289920) this
morning and it turns out that I [shouldn't have been using a repository for my
plugin](https://getcomposer.org/doc/faqs/why-can't-composer-load-repositories-recursively.md).
By adding my plugin to <http://www.packagist.org> I no longer got any errors.

Last thing I needed to fix was the `autoload.php` that I was requiring when I
was working on the plugin independently.  I just needed to make sure to only
include the `autoload.php` if the file exists, like this:

``` php
<?php 
if ( file_exists( __DIR__ .  '/vendor/autoload.php' ) ) { 
    require __DIR__ . '/vendor/autoload.php'; 
} 
```

If you use a dependency in a project, you should require the Composer generated
`autoload.php` somewhere. [Rarst
suggests](http://composer.rarst.net/recipe/site-stack) doing that in
`wp-config.php` and [Bedrock also seems to do it this
way](https://github.com/roots/bedrock/blob/master/web/wp-config.php#L7). Once
you've required the `autoload.php` somewhere it will autoload the classes of
your dependencies. 

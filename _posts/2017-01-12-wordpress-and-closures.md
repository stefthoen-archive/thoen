---
layout: post
title:  "WordPress and Closures"
date:   2017-01-12 22:12:00 +0100
categories: wordpress
---
Closures are anonymous functions that you can save to a variable if you're so
inclined. Here we're saving a anonymous function to `$example` and we're using
`$message` that we defined earlier:

``` php
<?php
$message = 'world';

$example = function ($arg) use ($message) {
    var_dump($arg . ' ' . $message);
};

$example('hello');
// Output: string(11) "hello world"
```

I've been using closures in Laravel and higher-order functions and I've just
recently started using WordPress again. Turns out that there are lots of
opportunities to use closures where I wasn't using them before. 

You can use a closure when you're adding an action for example:

``` php
<?php
add_action( 'init', function() {
    load_plugin_textdomain( 'your_text_domain', false, plugin_basename( PLUGIN_PATH
    ) . '/languages/' );
}
```

Or you might use it directly when you need a callback:

``` php
<?php
wp_add_dashboard_widget(
    'dashboard_widget',
    'Example Dashboard Widget',
    function() {
        echo "Hello World, I'm a great Dashboard Widget.";
    }
);
```

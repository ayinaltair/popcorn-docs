---
title: Popcorn.plugin.debug
---
# Popcorn.plugin.debug #

## Purpose ##

Popcorn.plugin.debug is a boolean flag that toggles error suppression on Popcorn plugin functions (start, end, etc.).
When it is set to false, errors are caught and stored inside Popcorn.plugin.errors, and an "error" event is triggered on the instance.
When set to true, errors will not be suppressed.

## Options ##

* **Popcorn.plugin.debug** \[Boolean\] - Toggle debug mode on or off

## Use Case ##

* During plugin development, debug mode may be turned on to have Popcorn suppress errors thrown inside of plugins.
* In production environments, debug mode should be set to false, allowing error handling to be performed by listening to the "error" event on the Popcorn instance.

## Examples ##

{% highlight js linenos %}
    // Turn on debug mode
    Popcorn.plugin.debug = true;

    // Create a plugin that will throw an error when it's start function runs
    pop.plugin( "foo", {
      start: function() {
        throw new Error();
      }
    });

    // Create Popcorn instance
    var pop = Popcorn( "#video-element-id" );

    // set up "foo" event
    pop.foo({ start: 1 });

    // The error will not be caught by Popcorn
    pop.play();

{% endhighlight %}

{% highlight js linenos %}
    // Debug mode is off by default

    // Create a plugin that will throw an error when it's start function runs
    Popcorn.plugin( "foo", {
      start: function() {
        throw new Error();
      }
    });

    // Create Popcorn instance
    var pop = Popcorn( "#video-element-id" );

    // set up "foo" event
    pop.foo({ start: 1 });

    // The error will be caught by Popcorn.plugin.errors
    pop.listen( "error", function( e ) {
      // 'e' is Popcorn.plugin.errors, which can be accessed outside the "error" event callback.
      console.log( e );
    });

    pop.play();

{% endhighlight %}

* [Live Demo of using Popcorn.plugin.debug (disabled)](http://jsfiddle.net/popcornjs/eV2c4/)
* [Live Demo of using Popcorn.plugin.debug (enabled)](http://jsfiddle.net/popcornjs/ssRLb/2/)

## Related ##

* [Popcorn.plugin.errors](#Popcorn.plugin.errors)
* [on](/popcorn-docs/media-methods/#on)
* [Popcorn.plugin](#Popcorn.plugin)

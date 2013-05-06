# ![LOGO](http://upload.wikimedia.org/wikipedia/en/9/9e/JQuery_logo.svg)
---

## Event Basics

- The ```on``` method is useful for binding the same handler function to multiple events
  - ```$.fn.click```, ```$.fn.focus```, ```$.fn.blur```, ```$.fn.change```
  - shorthand for jQuery's ```$.fn.on``` method

``` js
// Event setup using a convenience method
$( "p" ).click(function() {
    console.log( "You clicked a paragraph!" );
});
```

``` js
// Equivalent event setup using the `$.fn.on` method
$( "p" ).on( "click", function() {
    console.log( "click" );
});
```


Preventing a link from being followed with ```.preventDefault()```
``` js
$( "a" ).click(function( eventObject ) {
    var $this = $( this );
    if ( $this.attr( "href" ).match( /evil/ ) ) {
        eventObject.preventDefault();
        $this.addClass( "evil" );
    }
});
```


Binding multiple events with different handlers
``` js
$( "p" ).on({
    "click": function() { console.log( "clicked!" ); },
    "mouseover": function() { console.log( "hovered!" ); }
});
```

Tearing down all click handlers on a selection
``` js
$( "p" ).off( "click" );
```


Tearing down a particular click handler, using a reference to the function
``` js
var foo = function() { console.log( "foo" ); };
var bar = function() { console.log( "bar" ); };
 
$( "p" ).on( "click", foo ).on( "click", bar );
$( "p" ).off( "click", bar ); // foo is still bound to the click e
```

Setting up events to run only once
``` js
// Switching handlers using the `$.fn.one` method
$( "p" ).one( "click", firstClick );
 
function firstClick() {
    console.log( "You just clicked this for the first time!" );
    // Now set up the new handler for subsequent clicks;
    // omit this step if no further click responses are needed
    $( this ).click( function() { console.log( "You have clicked this before!" ); } );
}
```

Using $.fn.one to bind several events
``` js
$( "input[id]" ).one( "focus mouseover keydown", firstEvent);
 
function firstEvent( eventObject ) {
    console.log( "A " + eventObject.type + " event occurred for the first time on the input with id " + this.id );
}
```

## Handling Events

simple event binding
``` js
// When any <p> tag is clicked, we expect to see '<p> was clicked' in the console.
$( "p" ).on( "click", function() {
    console.log( "<p> was clicked" );
});
```

many events, one event handler
``` js
// When a user focuses on or changes any input element, we expect a console message
// bind to multiple events
$( "div" ).on( "mouseenter mouseleave", function() {
    console.log( "mouse hovered over or left a div" );
});
```

many events, many events/handlers
``` js
$( "div" ).on({
    mouseenter: function() {
        console.log( "hovered over a div" );
    },
    mouseleave: function() {
        console.log( "mouse left a div" );
    },
    click: function() {
        console.log( "clicked on a div" );
    }
});
```

event object
``` js
$( "div" ).on( "click", function( event ) {
    console.log( "event object:" );
    console.dir( event );
});
```

passing data to the event handler
``` js
$( "p" ).on( "click", {
    foo: "bar"
}, function( event ) {
    console.log( "event data: " + event.data.foo + " (should be 'bar')" );
});
```

binding events to elements that don't yet exist
``` js
$( "ul" ).on( "click", "li", function() {
    console.log( "Something in a <ul> was clicked, and we detected that it was an <li> element." );
});
```

Connecting Events to Run Only Once
``` js
// Switching handlers using the `.one()` method
$( "p" ).one( "click", function() {
    console.log( "You just clicked this for the first time!" );
    $( this ).click(function() {
        console.log( "You have clicked this before!" );
    });
});
```

Disconnecting Events

``` js
// Unbinding all click handlers on a selection
$( "p" ).off( "click" );
```

``` js
// Unbinding a particular click handler, using a reference to the function
var foo = function() {
    console.log( "foo" );
};
 
var bar = function() {
    console.log( "bar" );
};
 
$( "p" ).on( "click", foo ).on( "click", bar );
 
// foo will stay bound to the click event
$( "p" ).off( "click", bar );
```



## Namespacing

``` js
var TRKR = {};
TRKR.exclaim = function () {...};
```


## References

- [jQuery Event Basics](http://learn.jquery.com/events/event-basics/)
- [jQuery Selectors](http://www.w3schools.com/jquery/jquery_ref_selectors.asp)
- [Handling Events](http://learn.jquery.com/events/handling-events/)
- [RegExp & JS](https://developer.mozilla.org/en-US/docs/JavaScript/Reference/Global_Objects/RegExp)
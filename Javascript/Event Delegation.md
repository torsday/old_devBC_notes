# Event Delegation in js

---

---

## [Event Delegation 101](http://webcache.googleusercontent.com/search?q=cache:fw789WR1K2MJ:brandonaaron.net/blog/2010/03/4/event-delegation-with-jquery+&cd=3&hl=en&ct=clnk&gl=us) by Brandon Aaron

At its core event delegation is all about letting events bubble up the DOM tree to a parent element. This provides several advantages such as only binding one event handler instead of potentially 100s and it works with elements currently in the DOM at runtime and those which are injected after runtime.

Imagine you have a large table of data and you want to do something when the user clicks on a row. You might first start out by binding a click event to each <tr> which would look like this.

```js
$('tr').bind('click', function(event) {
    // this == tr element
});
```
If you have lots and lots of table rows it could take a while to bind all those events. Not to mention the browser now needs to keep track of all those event handlers. Instead, we can use event delegation by binding the click event to the table (or any parent element, maybe even the body) and letting the event bubble up to the table. Then we can inspect the event to see which element was actually clicked on. jQuery either does this for you or makes this part easy and we’ll look at how to do this in just a moment.

The second reason you might want to use event delegation is for automatically handling dynamic data. Lets say you needed to dynamically add rows to your table. Well, then you’d have to also bind the click event to those new rows. With event delegation the event is actually bound to the table element and any new rows do not need a new event bound. Awesome!

---


## Definitions

#### Events

Actions that can be detected by your Web Application

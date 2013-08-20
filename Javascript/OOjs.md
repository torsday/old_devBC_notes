# Object Oriented JavaScript
---

## Constructor & Prototypes

### Constructor

Used to make a class from which to build instances.

```js
function Animal (name, length) {
  this.name = name;
  this.length = length;
}
```

another way to write this:

```js
var Animal = function (name, length) {
  this.name = name;
  this.length = length;
}
```

[Neither are deprecated, and both will work. The difference here is that one is a named function ( ```function f()``` ) while the other is a variable equal to a function ( ```var f = function()``` ).](http://stackoverflow.com/questions/9423693/javascript-function-definition-syntax)

#### Example Code
```js
var animals = [
  new Animal("Human", 2),
  new Animal("Monkey", 2),
  new Animal("Kangaroo", 2),
  new Animal("Horse", 4),
  new Animal("Cow", 4),
  new Animal("Centipede", 100)
];

animals[2].name // "Kangaroo"
```

### Prototype

Creates a class-like method.

 ```
Animal.prototype.identify = function() {
  return "I am a " + this.name + " with " + this.length + " legs."
}
```

> [The prototype object is meant to be used on constructor functions, basically functions that will be called using the new operator to create new object instances. Functions in JavaScript are first-class objects, which means you can add members to them and treat them just like ordinary objects:](http://stackoverflow.com/questions/1592384/adding-prototype-to-object-literal)

#### Example Code
```js
animals[0].identify() // "I am a Human with 2 legs."
animals[0].identify === animals[5].identify // true, only one implementation of the identify() function should exist
```

## Object Literal

Creates a class object which can never create instances.

``` js
var Zoo = {
  collection : [],
  init : function(arr_of_animals) { this.collection = arr_of_animals },
  bipeds : function () {
    collect = []
    for(var i = 0; i < this.collection.length; i++) {
      if(this.collection[i].length == 2) {
        collect.push(this.collection[i]);
      }
    }
    return collect;
  },
  quadrupeds : function () {
    collect = []
    for(var i = 0; i < this.collection.length; i++) {
      if(this.collection[i].length == 4) {
        collect.push(this.collection[i]);
      }
    }
    return collect;
  }
}
```

#### Example Code
```js
Zoo.init(animals);

Zoo.bipeds().length // 3
Zoo.quadrupeds().length // 2
```

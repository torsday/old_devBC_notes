# Object Oriented JavaScript
---

## Constructor & Prototypes
``` js
function Animal (name, length) {
  this.name = name;
  this.length = length;
}
 
Animal.prototype.identify = function() {
  return "I am a " + this.name + " with " + this.length + " legs."
}
```
 
## Object Literal
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

## Driver Code
``` js 
function assert(test, message) {  
  if (!test) {
    throw "ERROR: " + message;
  }
  return true;
}
 
var animals = [
new Animal("Human", 2),
new Animal("Monkey", 2),
new Animal("Kangaroo", 2),
new Animal("Horse", 4),
new Animal("Cow", 4),
new Animal("Centipede", 100)
];
 
Zoo.init(animals);
 
assert(
  Zoo.bipeds().length === 3, "the Zoo should have 3 bipeds"
  );
assert(
  Zoo.quadrupeds().length === 2, "the Zoo should have 2 bipeds"
  );
assert(
  animals[0].identify() === "I am a Human with 2 legs.", "humans have 2 legs"
  );
assert(
  animals[2].name === "Kangaroo", "expected 'Kangaroo'"
  );
assert(
  animals[0].identify === animals[5].identify, "only one implementation of the identify() function should exist"
  );
```
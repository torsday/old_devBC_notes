

# Rule of Composition

Developers should write programs that can communicate easily with other programs. This rule aims to allow developers to break down projects into small, simple programs rather than overly complex monolithic programs.

---

Easy to compose:

* Pure functions  - e.g. sort(pluck(people,'name'))
* Method chaining - e.g. people.map(&:name).sort
* Music (if you understand the fundementals)
* Leggo (except new leggos)

* Some well built REST APIs

Hard to compose:

* Methods that take as arguments objects with complex interfaces and then pass them to other methods

---

* Removing explicit names often makes composition easier



# Rule of Separation

Developers should separate the mechanisms of the programs from the policies of the programs; one method is to divide a program into a front-end interface and back-end engine that interface communicates with. This rule aims to let policies be changed without destabilizing mechanisms and consequently reducing the number of bugs.

---

policies vs mechasims = what vs how

Where mechanism leaks:

* SQL in ActiveRecord

Revealed Policy, Hidden Mechanisms:

* Most unix commands
* Ruby enumerable method
* Good HTTP APIs (or any API really)

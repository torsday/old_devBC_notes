

# Rule of Modularity

Developers should build a program out of simple parts connected by well defined interfaces, so problems are local, and parts of the program can be replaced in future versions to support new features.

This rule aims to save time on debugging complex code that is complex, long, and unreadable.

---

* Simple parts (one thing)
  * uuid
  * ls - just lists contents of current directory (or directory in argv)
  * puts - writes arg to stdout then writes newline
  * p - puts and also returns arg (slightly more complex)
  * URI gem
  * Nokigiri
  * Faker
  * Secure Random - just gives you a random number

* Complex parts (more than one thing)
  * Ruby interpreter
  * ActiveRecord (OMG)
  * Browser
  * Node
  * jQuery

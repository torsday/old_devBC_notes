# Modules
---

> I think of a module as a degenerate abstract class. A module can’t be instantiated and no class can directly extend it but a module can fully implement methods. A class can leverage the implementation of a module by including the module’s methods. A module can define methods that can be shared in different and separate classes either at the class or instance level.

#### Benefits

- provide a *namespace*, preventing name clashes
- implement the *mixin* facility

## Syntax

```ruby
module Identifier
  statement1
  statement2
end
```

### Example

```ruby
#!/usr/bin/ruby

# Module defined in trig.rb file

module Trig
   PI = 3.141592654
   def Trig.sin(x)
   # ..
   end
   def Trig.cos(x)
   # ..
   end
end
```

```ruby
#!/usr/bin/ruby

# Module defined in moral.rb file

module Moral
   VERY_BAD = 0
   BAD = 1
   def Moral.sin(badness)
   # ...
   end
end
```

```ruby
Example:

require 'trig.rb'
require 'moral'

y = Trig.sin(Trig::PI/4)
wrongdoing = Moral.sin(Moral::VERY_BAD)
```

### You can embed a module in a class. To embed a module in a class, you use the include statement in the class:

```ruby
module Week
   FIRST_DAY = "Sunday"
   def Week.weeks_in_month
      puts "You have four weeks in a month"
   end
   def Week.weeks_in_year
      puts "You have 52 weeks in a year"
   end
end
```

```ruby
#!/usr/bin/ruby
require "Week"

class Decade
include Week
   no_of_yrs=10
   def no_of_months
      puts Week::FIRST_DAY
      number=10*12
      puts number
   end
end
d1=Decade.new
puts Week::FIRST_DAY
Week.weeks_in_month
Week.weeks_in_year
d1.no_of_months
```

result

```
Sunday
You have four weeks in a month
You have 52 weeks in a year
Sunday
120
```

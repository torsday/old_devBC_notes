# Interview Review

## OOP

### decoupling, examples of

### POODR

### Law of demeter, encapsulation

## Ruby

```ruby
class person
  attr_reader :name
  attr_writer :password
  attr_accessor :location, :height

  def initialize(name, location)
    @name = name
    @location = location
    @password = ""
    @height = ""
  end
end
```

## RegEx

TODO

## HTML

TODO

## CSS

TODO

## jQuery

### AJAX

TODO

### [Manipulation](http://api.jquery.com/category/manipulation/)

#### .addClass()

TODO

#### .append()

TODO

#### .clone()

TODO

#### .css()

TODO

#### .empty()

TODO

#### .html()

TODO

#### .text()

TODO

#### .val()

TODO

### [Events](http://api.jquery.com/category/events/)

#### .click()

TODO

#### event.data

TODO

#### event.pageX

TODO

#### event.pageY

TODO

#### event.preventDefault()

TODO

#### event.stopPropagation()

TODO

#### .off()

TODO

#### .on()

TODO

#### .one()

TODO

#### .ready()

TODO

#### .toggle()

TODO

### [jQuery UI](http://api.jqueryui.com/)

#### [Draggable](http://jqueryui.com/draggable/)

TODO

#### Droppable

TODO

#### Selectable

TODO

#### Sortable

TODO

## Rails

### Classes

#### [ActionController::Base](http://api.rubyonrails.org/classes/ActionController/Base.html)

##### ```application_controller.rb```

```ruby
class ApplicationController < ActionController::Base
end
```

##### ```users_controller.rb```

```ruby
class UsersController < ApplicationController
end
```


#### [ActiveModel::Validator](http://api.rubyonrails.org/classes/ActiveModel/Validator.html)

Custom validators are classes that extend ActiveModel::Validator. These classes must implement a validate method which takes a record as an argument and performs the validation on it. The custom validator is called using the validates_with method.

```ruby
class MyValidator < ActiveModel::Validator
  def validate(record)
    unless record.name.starts_with? 'X'
      record.errors[:name] << 'Need a name starting with X please!'
    end
  end
end
 
class Person
  include ActiveModel::Validations
  validates_with MyValidator
end
```

#### [ActiveRecord::Base](http://api.rubyonrails.org/classes/ActiveRecord/Base.html)

```ruby
class User < ActiveRecord::Base
  attr_accessible :name
  validates :email,  :presence => true, :uniqueness => true, :length => { :minimum => 6 }, :format { :with => /^([^@\s]+)@((gmail.)+[a-z]{2,})$/i }
end
```

#### [ActiveRecord::Calculations.pluck](http://apidock.com/rails/ActiveRecord/Calculations/pluck)

This method is designed to perform select by a single column as direct SQL query Returns Array with values of the specified column name The values has same data type as column.

```ruby
erson.pluck(:id) # SELECT people.id FROM people
erson.uniq.pluck(:role) # SELECT DISTINCT role FROM people
Person.where(:confirmed => true).limit(5).pluck(:id)
```

#### [ActiveRecord::Migration](http://api.rubyonrails.org/classes/ActiveRecord/Migration.html)

```ruby
class CreateUsers < ActiveRecord::Migration
  def change
    create_table :users do |t|
      t.string  :name, :null => false
    end
  end
end
```

### Associations

TODO

#### Polymorphic

e.g. users have posts, posts have posts

TODO

### attribute accessors

DEFINE

### difference betwen sinatra & rails

EXPLAIN

### rails helpers, the ones given to us

- form helpers
- inheritence
- extend
- module

TODO

## SQL (Structured Query Language)

### Pros

- flexible
- universal
- few commands to learn

### Cons

- requires detailed knowledge of db
- can provide misleading results

### Basic Components

#### Required

```sql
SELECT column
FROM table
```

#### With Optional

```sql
SELECT schema.table.column
FROM table alias
WHERE [conditions]
ORDER BY [columns]
;
```

#### Basic Structural Elements

##### SELECT

defines what is to be returned

- columns
- contant text values
- formulas
- pre-defined functions
- Group Functions: COUNT, SUM, MAX, MIN, AVG

##### FROM

defines the table(s) or view(s) used by SELEC or WHERE

##### Examples

```sql
SELECT state_name, state_abbr
FROM states
```

```sql
SELECT *
FROM agencies
```

##### WHERE

- defines what records are to be included in the query
- uses conditional operators (e.g. =, >=, != ...)
- link multiple conditions with AND & OR statements
- strings contained within **single quotes**


##### Examples

```sql
SELECT state_name, state_population
FROM states
WHERE state_name LIKE '%NORTH%'
```

```sql
SELECT *
FROM annual_summaries
WHERE sd_duration_code IN ('1', 'W', 'X')
  AND annual_summary_year = 2000
```

```sql
SELECT mo_mo_id, sd_duration_code
FROM annual_summaries
WHERE annual_summary_year = 2003
  AND values_gt_pri_std > 0
  OR values_gt_sec_std > 0
```

```sql
SELECT mo_mo_id, sd_duration_code
FROM annual_summaries
WHERE annual_summary_year = 2003
AND (values_gt_pri_std > 0
OR values_gt_sec_std > 0)
```

##### ORDER BY

- defines how the records are to be sorted
- must be in the ```SELECT``` statement to be ```ORDER BY```

```sql
SELECT * 
FROM agencies 
ORDER BY agency_desc
```

```sql
SELECT cc_cn_stt_state_code, site_id
FROM sites
WHERE lut_land_use_type = ‘MOBILE’
ORDER BY cc_cn_stt_state_code DESC
```

##### GROUP BY

- Performs common mathematical operations on a group of records
- defines what constitues a group with ```GROUP BY```
- all non-group elements in the ```SELECT``` statement must be in the ```GROUP BY``` clause (additional columns are optional)

```sql
SELECT si_si_id, COUNT(mo_id) 
FROM monitors 
GROUP BY si_si_id
```

```sql
SELECT AVG(max_sample_value)
FROM summary_maximums
WHERE max_level <= 3
  AND max_ind = ‘REG’
GROUP BY ans_ans_id
```

#### Selecting from Multiple Tables

##### Joining Tables with Primary & Foreign Keys

cartesion join / simple join

```sql
SELECT mo_id, poc, parameter_desc
FROM monitors, parameters
```

joining tables

```sql
SELECT mo_id, poc, parameter_desc
FROM monitors, parameters
WHERE pa_parameter_code = parameter_code
```

##### Aliases

Why

- saves typing
- good internal documentation
- better headers

```sql
SELECT mo.mo_id, mo.poc, pa.parameter_desc parameter
FROM monitors mo, parameters pa
WHERE mo.pa_parameter_code = pa.parameter_code
```

## RSpec

TODO


## Whiteboarding

1. Be able to create from scratch any of the above code.

## Books

### [POODR: Practical Object-Oriented Design in Ruby](https://github.com/skmetz/poodr)
### ReWork
### Professional JavaScript for Web Developers
### Thinking in Systems
### Zen Mind, Beginners Mind
### Design Patterns
### The Pragmatic Programmer
### Code Complete


## Passion


## Lower water line (i.e. iceberg)



## References

- [epa.gov: SQL Basics](http://www.epa.gov/ttn/airs/airsaqs/training/SQL%20Basics.pdf)



## INBOX

form_for
fields_for
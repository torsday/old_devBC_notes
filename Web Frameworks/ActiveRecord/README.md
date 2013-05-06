# ActiveRecord
---

## Types of Associations

``` ruby
belongs_to
has_one
has_many
has_many :through
has_one :through
has_and_belongs_to_many
```

## Methods for migrations

``` ruby
add_column
add_index
change_column
change_table
create_table
drop_table
remove_column
remove_index
rename_column
```

## Supported Types

``` ruby
:binary
:boolean
:date
:datetime
:decimal
:float
:integer
:primary_key
:string
:text
:time
:timestamp
```

## Methods for retrieving objects from the database

``` ruby
where
select
group
order
reorder
reverse_order
limit
offset
joins
includes
lock
readonly
from
having
```

## Methods & Validations

### These methods trigger validations, & will save the object to the database **only if the object is valid**

``` ruby
create
create!
save
save!
update
update_attributes
update_attributes!
```

### These methods skip validations, & will save the object to the database **regardless** of its validity.

``` ruby
decrement!
decrement_counter
increment!
increment_counter
toggle!
touch
update_all
update_attribute
update_column
update_counters
```

## Tables

### Creation

``` ruby
class CreateUsers < ActiveRecord::Migration
  def change
    create_table :users do |t|
      t.string :name
      t.string :email
      t.string :password

      t.timestamps
    end
  end
end
```

### Addition

``` ruby
class AddUserNameToUsers < ActiveRecord::Migration
  def change
    add_column :users, :user_name, :string
  end
end
```


## References
- Active Record Guide
  - [Associations](http://guides.rubyonrails.org/association_basics.html)
  - [Migrations](http://guides.rubyonrails.org/migrations.html)
  - [Query Interface](http://guides.rubyonrails.org/active_record_querying.html)
  - [Validations & Callbacks](http://guides.rubyonrails.org/active_record_validations_callbacks.html)

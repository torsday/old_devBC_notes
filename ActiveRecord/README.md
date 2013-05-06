# ActiveRecord

## Creating a migration

## Creating a table

## Adding to a table

``` ruby
class AddNewColumnToTable < ActiveRecord::Migration
  def change
    add_column :<table>, :<column>, :<type>
  end
end
```
# ActiveRecord
---

## Rake Commands

- ```$ rake console```
- ```$ rake db:drop```
- ```$ rake db:create```
- ```$ rake db:migrate```
- ```$ rake db:seed```
- ```$ rake db:drop && rake db:create && rake db:migrate && rake db:seed

## Rake Generations

- ```$ rake generate:migration NAME=create_users```
- ```$ rake generate:model NAME=user```

## Creating a table

``` ruby
class CreateUsers < ActiveRecord::Migration
  def change
    create_table :users do |t|
      t.string :first_name
      t.string :last_name
      t.string :email
      t.string :password

      t.timestamps
    end
  end
end
```

## Adding to a table

``` ruby
class AddNewColumnToTable < ActiveRecord::Migration
  def change
    add_column :<table>, :<column>, :<type>
  end
end
```

# ActiveRecord

## Creating a migration

```rake generate:migration NAME=the_name_of_your_migration```

## Creating a table

``` ruby
class CreateUsers < ActiveRecord::Migration
  def change
    create_table :users do |t|
      t.string :first_name
      t.string :last_name
      t.string :user_name
      t.string :email
      t.string :password_hash
      t.string :perishable_token

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
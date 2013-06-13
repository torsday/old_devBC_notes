

# Factory Girl

## Why Factory Girl?
Factory Girl solves the worst problem of fixtures: **maintenance**. 

Tests become much easier to maintain when you can request a model instance that is always **current**. Using Factory Girl, *a model is never bound to a particular phase of your application’s development*. They are *dynamically loaded from the current state of your application*. Were there new Customer attributes introduced in that last merge? No problem, Factory Girl already sees them. Not so the case with a directory of fixtures.

Factory Girl was created to create templates for valid and re-usable objects.  They allow more customization when you instantiate the objects and they aim to ensure that you have a valid object to work with. They can be used anywhere in your tests and in your before and after test hooks.

Factories are aimed at creating valid Ruby objects and records, so that you can keep your object creation flexible and DRY. 

#### /test/factories
``` ruby 
FactoryGirl.define do

  factory :site do
    name      'test site'
    subdomain { "#{name}".gsub(/ /,'-') }
  end
  
  factory :company do
    site
    name 'Spatula City, Inc.'
    site_url 'test'
    pitch "We sell spatulas.. and that's all!"
    city 'Spatville'
    state 'OR'
    country 'United States'
    status 'active'
  end

  factory :customer do
    company
    payment_plan 'basic'  
    engagement 'monthly'
    subscription true
  end
  
  sequence :product_name do |n|
    "The Zoom Spat #{n}"
  end
  
  factory :product do
    company
    name  { generate(:product_name) }
    price 11.0
    inventory 20
  end
  
  factory :line_item do
    product
    quantity 1
  end
  
  factory :order do
    customer

    ignore do
      total_items 1
    end

    after(:create) do |order, evaluator|
       FactoryGirl.create_list(:line_item, evaluator.total_items, order: order)
    end
  end
  
end
```

Examples of what you can do with these factories
``` ruby
# return a user instance that's not saved
user = FactoryGirl.build(:user)

# returns a saved User instance
user = FactoryGirl.create(:user)

# return a hash of attributes that can be used to build a User instance
attr = FactoryGirl.attributes_for(:user)

# return an object with all defined attributes stubbed out
stub = FactoryGirl.build_stubbed(:user)

# pass a block to any of the methods above will yield the return object
FactoryGirl.create(:user) do |user|
  user.posts.create(attributes_for(:post))
end
```

Example Test
``` ruby
def test_customer_refund
    # this not only returns a new order but it also creates 5 line items
    @order = FactoryGirl.create(:order, :total_items => 5)
    
    # total charge simply tallies the sum of the line_items + shipping, etc.
    order_total = @order.total_charge

    # charge the customer
    @order.take_their_money!
    
    # reverse the charge, passing an amount to refund
    @order.refund_the_money!(order_total)
    refund_amount = @order.total_refund
      
    assert_equal(order_total, refund_amount, "We should have refunded the full amount of the order")      
  end

  ... lots more tests ...

end
```

### Other things to check out
- Traits
- Lazy attributes
- Sequences
- Create multiple records at once
- You can change existing factories that you inherited from a gem
- You can utilize callbacks


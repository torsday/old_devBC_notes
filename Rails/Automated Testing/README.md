# Automated Testing
---

## Tutorial
- Show test examples, contrasting good tests from bad tests
- Illustrate the different kind of tests
- Record a screencast illustrating your points
- Curate outside resources

## FAQ
- How do I use rspec instead of the default testing framework that comes with Rails?
- How do I test common features of ActiveRecord models? Validations? Associations? Callbacks?
- How do I populate my test database with dummy data?
- How do I run my test suite? How do I interpret the output?
- What makes a good test? What makes a bad test?
- What is the difference between a unit test and an integration test?

#### Tests should be:
- Reliable
- Easy to write
- Easy to understand

#### Tradeoff
- We’re not focusing on speed
- We’re not focusing on overly DRY code in our tests



## Fixtures


Fixtures provide a means of loading serialized data from YAML files for testing purposes. Tests frequently involve creating instances of various objects, making assertions about their state, and drawing conclusions from there. With fixtures you don’t have to manually create a new object instance for each test. You can simply load a fixture and refer to its value like so:


What they are:
Fast to load
Easy to generate from live data for later re-use
Easy to read
What they are not:
Dynamic – you get the same values every time for better or worse
Aware of change – if your model’s change your fixtures may become outdated and require manual updates before your tests will pass
Why use fixtures when I can use seeds.rb?
Using seeds.rb to accomplish the work of fixtures (or vice versa) would be a mistake as seeds.rb is designed for one purpose: to populate an empty database with essential data. To belabor the point, seeds.rb should be responsible for data so critical to your application that would be inoperable without it. For many applications it is likely you will need seeds.rb to setup your test database via rake db:test:prepare.
What about using a factory?
Don’t fret. We’ll talk about factories (or more specifically, FactoryGirl) and how they can provide much needed functionality in a coming post.


## Unit Tests

Unit tests are the bread and butter of testing. These little guys tell us that our code is operating as expected no matter what we throw at it. They are often closely paired to a model and follow a pattern like so:

- /app/models/user.rb contains methods like:
    - def first_name
    - def last_name
    - def email
    - def password

- /test/unit/user_test.rb tests those methods: 
    - def test_first_name
    - def test_last_name
    - def test_login
    - def test_password_reset

Unit tests make assertions that validate data going into a method and data coming out. They validate success as well as failure conditions.


## Integration Tests
Integration tests take functional tests one step further by examining behavior across multiple controller actions.

## Functional Tests
Functional tests are written to validate the content returned by individual actions within your controllers and mailers. Let’s look at some code.

## Factory
a factory is an object whose sole job is to create other objects.

## Why Factory Girl?
The first (and possibly best) reason to use Factory Girl is because it solves the single worst problem of fixtures: maintenance. Tests become much easier to maintain when you can request a model instance that is always current. Using Factory Girl, a model is never bound to a particular phase of your application’s development. They are dynamically loaded from the current state of your application. Were there new Customer attributes introduced in that last merge? No problem, Factory Girl already sees them. Not so the case with a directory of fixtures.



Test-Unit has a large list of assertion matchers to help validate the behavior of a method. Tests providing coverage for crucial models (user.rb, for example) may have multiple (def test_xyz_fails_if_nil, def test_xyz_resets_some_value) methods target a single model attribute (def xyz).



## Factory Girl

### Why Factory Girl?
Before Factory Girl there were *fixtures*, which are fixed records loaded into the database. Factory Girl was created to create templates for valid and re-usable objects.  They allow more customization when you instantiate the objects and they aim to ensure that you have a valid object to work with. They can be used anywhere in your tests and in your before and after test hooks.

Factories are aimed at creating valid Ruby objects and records, so that you can keep your object creation flexible and DRY. 

##### /test/factories
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
    pitch 'We sell spatulas.. and that's all!'
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

# Returns a saved User instance
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

##### Other things to check out
- Traits
- Lazy attributes
- Sequences
- Create multiple records at once
- You can change existing factories that you inherited from a gem
- You can utilize callbacks




## Shoulda

add ```rspec-rails``` and ```shoulda-matchers``` to the ```Gemfile```.
``` ruby
group :test do
  gem 'rspec-rails'
  gem 'shoulda-matchers'
end
```

``` ruby
describe Post do
  it { should belong_to(:user) }
  it { should validate_presence_of(:title) }
end
```


## Factory Girl





## References
- Github
    - [thoughtbot / shoulda](https://github.com/thoughtbot/shoulda)
    - [thoughtbot / factory_girl](https://github.com/thoughtbot/factory_girl)
    - [thoughtbot / factory_girl_rails](https://github.com/thoughtbot/factory_girl_rails)
- [rspec.info](http://rspec.info/)
- [How I learned to test my Rails applications](http://everydayrails.com/2012/03/12/testing-series-intro.html)
- [RailsGuides: A Guide to Testing Rails Applications](http://guides.rubyonrails.org/testing.html)
- [Rails Testing — Demystifying Test-Unit](http://www.hiringthing.com/2012/08/02/rails-testing-demystifying-test-unit.html)
- [Rails Testing — Factory Girl](http://www.hiringthing.com/2012/08/17/rails-testing-factory-girl.html)
- StackOverflow
    - [Factory Girl = What's the purpose?](http://stackoverflow.com/questions/5183975/factory-girl-whats-the-purpose)
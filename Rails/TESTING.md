# Automated Testing with Rails
---

## Index
- [Factory Girl](https://github.com/ctorstens/dev_bootcamp_notes/blob/master/Rails/Testing/Factory%20Girl.md)
- [RSpec](https://github.com/ctorstens/dev_bootcamp_notes/blob/master/Rails/Testing/RSpec.md)

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



## Unit Tests

Unit tests make assertions that validate data going into a method and data coming out. They validate success as well as failure conditions. Essentially, they tell us that our code is operating as expected no matter what we throw at it. They are often closely paired to a model and follow a pattern like so:

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





## Fixtures
Fixtures provide a means of loading serialized data from YAML files for testing purposes. Tests frequently involve creating instances of various objects, making assertions about their state, and drawing conclusions from there. With fixtures you don’t have to manually create a new object instance for each test. You can simply load a fixture and refer to its value like so:


##### What they are:
- Fast to load
- Easy to generate from live data for later re-use
- Easy to read

##### What they are not:
- Dynamic – you get the same values every time for better or worse
- Aware of change – if your model’s change your fixtures may become outdated and require manual updates before your tests will pass

##### Why use fixtures when I can use seeds.rb?
Using seeds.rb to accomplish the work of fixtures (or vice versa) would be a mistake as seeds.rb is designed for one purpose: to populate an empty database with essential data. To belabor the point, seeds.rb should be responsible for data so critical to your application that would be inoperable without it. For many applications it is likely you will need seeds.rb to setup your test database via rake db:test:prepare.





## Shoulda

Shoulda allows you to create unit tests and matchers in a light-weight, readable format. 

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


 
Matchers
 
Matchers for Active Record test associations.
 
Active Record matchers
 
``` ruby
describe Post do 
  it {should belong_to(:user)}
  it {should have_many(:tags).through(:taggings)}
end
```
 
Matchers for Active Model tests valiations.
Active Model matchers

``` ruby
describe Post do 
  it {should validate_uniqueness of(:title)}
end
 
describe User do
  it {should_not allow_value("blah").for(:email)}
end
```
 
Unit Testing
 
``` ruby
class CalculatorTest < Test::Unit::TestCase
  context "a calculator" do
    setup do
      @calculator = Calculator.new
    end
 
    should "add two numbers for the sum" do
      assert_equal 4, @calculator.sum(2, 2)
    end
 
    should "multiply two numbers for the product" do
      assert_equal 10, @calculator.product(2, 5)
    end
  end
end
```


## [Testing Tips & Tricks](https://gist.github.com/ndelage/5585671)

* This is a copy of ndelage's 'Testing Tips & Tricks' gist *

### Run a single test
In a large application, running all the tests at once using `rake spec` can make it difficult to check the output of the test you're working on. Especially if you have many failing or pending tests. Run a single test by running rspec:

`rspec spec/models/account.rb`
  
You can be even more specific and run a specific example from a test file. For example, given the following tests:
```ruby
11: describe "#deposit!" do
12:  it "adds value to the balance" do
13:     expect{account.deposit!(10)}.to change{account.balance}.by(10)
14:   end
15:   it "returns the balance" do
16:     account.deposit!(10).should == account.balance
17:   end
18: end
```

`rspec account_spect.rb:15` will only run the test `it "returns the balance"`

### Run all the tests frequently and always before making any commits
Running a specfic example file or test helps you focus, but don't forget to run the entire test suite with `rake spec` before making any commits. While the test you're might be passing, it's very possible your changes might have broken another test. __Better to get that feedback immediately__, rather than later.

### Consult the log

When you run any rails application (the webserver, tests or rake tasks) ouput from the running code is saved to a log file. There are log files per environment: `log/development.log`, `log/test.log` and `log/production.log`

Take a moment to open up one of these log files in your editor and take a look at its contents. To keep an eye on what's new in your log files, use the *nix tool `tail`. Try running the following on your terminal:

```
tail -f log/test.log
```
The option -f (follow)  allows a file to be monitored. Instead of just displaying the last few lines and exiting, tail displays the lines and then monitors the file. As new lines are added to the file by another process, tail updates the display. This is particularly useful for monitoring log files.





## References
- Github
    - [ndelage / testing tips.md](https://gist.github.com/ndelage/5585671)
    - [jnicklas / capybara](https://github.com/jnicklas/capybara)
    - [thoughtbot / shoulda](https://github.com/thoughtbot/shoulda)
    - [thoughtbot / factory_girl](https://github.com/thoughtbot/factory_girl)
    - [thoughtbot / factory_girl_rails](https://github.com/thoughtbot/factory_girl_rails)
- [rspec.info](http://rspec.info/)
- [How I learned to test my Rails applications](http://everydayrails.com/2012/03/12/testing-series-intro.html)
- [RailsGuides: A Guide to Testing Rails Applications](http://guides.rubyonrails.org/testing.html)
- [Rails Testing — Demystifying Test-Unit](http://www.hiringthing.com/2012/08/02/rails-testing-demystifying-test-unit.html)
- [Rails Testing — Factory Girl](http://www.hiringthing.com/2012/08/17/rails-testing-factory-girl.html)
- StackOverflow
    - [Factory Girl - What's the purpose?](http://stackoverflow.com/questions/5183975/factory-girl-whats-the-purpose)






## Inbox

##### after any time you do ```rake db:migrate```, perform the following
```
$ rake db:test:prepare
```
What this does is tells the testing gods the database has a new design when they create a new database during their tests

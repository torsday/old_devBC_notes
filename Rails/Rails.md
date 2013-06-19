# Rails






## Setup (Manual)

#### Create Rails app (use *postgres* instead of sqlite) without tests
```
rails new <app_name> -d postgresql -T
```

#### Setup git repo

```
git init
git add .
git commit...
```

#### Rename/create README && Commit

#### Setup GEMFILE

##### To allow rspec generation
``` ruby
group :test, :development do
  gem 'rspec-rails'
end
```

##### may include such files as below

``` ruby
gem 'activesupport'
gem 'activerecord'
gem 'bcrypt-ruby'
gem 'pg' # unnecessary if you initialized with pg
```

##### Create database

```
rake db:create
```

#### add RSpec

```
rails generate rspec:install
```



#### Create Home Controller elements

##### app/controllers/home_controller.rb

```
$ touch app/controllers/home_controller.rb
```

###### ```app/controllers/home_controller.rb```

```ruby
class HomeController < ApplicationController
  def index
  end
end
```

```
$ mkdir app/views/home && touch app/views/home/index.html.erb
```

###### ```app/views/home/index.html.erb```
```HTML+ERB
<p>Anything, or nothing. It's only important to have the </p>
```

#### Delete ```public/index.html```

```
$ rm public/index.html
```

#### create route for home

##### ```config/routes.rb```

```ruby
WeddingRsvp::Application.routes.draw do
  root :to => 'home#index'
end
```





## Setup (With Scaffolding)

### Create Rails app (use *postgres* instead of sqlite) without tests
```
rails new <app_name> --database=postresql -T
```

### Edit config/routes.rb

``` ruby
root :to => 'home#index'
```

### add rspec to the app
```
$ rails generate rspec:install

  create  .rspec
   exist  spec
  create  spec/spec_helper.rb
```

### create home controller with index router
```
$ rails generate controller home index

  create  app/controllers/home_controller.rb
   route  get "home/index"
  invoke  erb
  create    app/views/home
  create    app/views/home/index.html.erb
  invoke  rspec
  create    spec/controllers/home_controller_spec.rb
  create    spec/views/home
  create    spec/views/home/index.html.erb_spec.rb
  invoke  helper
  create    app/helpers/home_helper.rb
  invoke    rspec
  create      spec/helpers/home_helper_spec.rb
  invoke  assets
  invoke    coffee
  create      app/assets/javascripts/home.js.coffee
  invoke    scss
```

### Remove native index file

```
$ rm public/index.html
```

### Create a resource using scaffolding

The scaffold generator will build several files in your application, along with some folders, and edit config/routes.rb

```
$ rails generate scaffold User name:string email:string password_hash:string

  invoke  active_record
  create    db/migrate/20130514014401_create_users.rb
  create    app/models/user.rb
  invoke    rspec
  create      spec/models/user_spec.rb
  invoke  resource_route
   route    resources :users
  invoke  scaffold_controller
  create    app/controllers/users_controller.rb
  invoke    erb
  create      app/views/users
  create      app/views/users/index.html.erb
  create      app/views/users/edit.html.erb
  create      app/views/users/show.html.erb
  create      app/views/users/new.html.erb
  create      app/views/users/_form.html.erb
  invoke    rspec
  create      spec/controllers/users_controller_spec.rb
  create      spec/views/users/edit.html.erb_spec.rb
  create      spec/views/users/index.html.erb_spec.rb
  create      spec/views/users/new.html.erb_spec.rb
  create      spec/views/users/show.html.erb_spec.rb
  create      spec/routing/users_routing_spec.rb
  invoke      rspec
  create        spec/requests/users_spec.rb
  invoke    helper
  create      app/helpers/users_helper.rb
  invoke      rspec
  create        spec/helpers/users_helper_spec.rb
  invoke  assets
  invoke    coffee
  create      app/assets/javascripts/users.js.coffee
  invoke    scss
  create      app/assets/stylesheets/users.css.scss
  invoke  scss
  create    app/assets/stylesheets/scaffolds.css.scss
```


### Add a link using 'link_to'

#### app/views/home/index.html.erb

``` HTML+ERB
<h1>Hello, Rails!</h1>
<%= link_to "My Blog", posts_path %>
```





## Rails, the DBC Way


### 1.  Create the skeleton
```
$ rails new app_name --database=postgresql
```

### 2.  Configure database

  - sqlite by default, for postgres:

#### config/database.yml
``` ruby
development:
  adapter: postgresql
  database: app_name_dev
  pool: 5
  timeout: 5000

test:
  adapter: postgresql
  database: app_name_dev
  pool: 5
  timeout: 5000

production:
  adapter: postgresql
  database: app_name #convention is to use actual name of app (no dev)
  pool: 5
  timeout: 5000
```

### 3.  Config gems, add:

``` ruby
gem 'pg'
group :development, :test do
    gem 'rspec-rails'
end
```


### 4. Initialize Spec
```
$ rails generate rspec:install
```

###  5. Create Migrations
```
$ rails generate migration CreateUsersTable
```

##### 20130514001059_create_users_table.rb
``` ruby
class CreateUsersTable < ActiveRecord::Migration
  def change
    create_table :users do |t|
      t.string :name
      t.string :email
      t.string :password_hash
    end
  end
end
```

##### To delete a migration, model...
```
$ rails d model User
```

### 6. Create Models

##### app/models/user.rb
``` ruby
class User < ActiveRecord::Base
  validates :email, :confirmation => true
  validates :email, :uniqueness => true
  validates :password_hash, :presence => true
  has_many  :urls
end
```

### 7. Delete the smoketest default index
```
public/index.html
```

### 8. Uncomment line 51 in config/routes.rb
``` ruby
root :to => 'home#index' # was originally 'welcome#index'
```

### 9. Create Controller(s)

##### app/controllers/home_controller.rb
``` ruby
class HomeController < ApplicationController
  def index
  end
end
```

### 10. Create View(s)

##### app/views/home/index.html.erb
```HTML+ERB
<p>hello there</p>
```

### 11. Start Server
i. ```$ rails s```
ii. [http://localhost:3000](http://localhost:3000)

### 12. Write the rest of the app...



















## Important Commands

#### Create a new app
``` rails new <name_of_project>```

#### Launch server
```
rails server
rails s
```

## Generation

### Migration
#### ```Add<Anything>To<Table Name> [OPTIONS]```
```
$ rails generate:migration AddEmailToUsers email:string
```

### Model
```
$ rails generate model User name:string email:string password_hash:string
```


### Scaffold
```
$ rails generate scaffold <name> <attribute>:<type>
$ rails g scaffold <name> <attribute>:<type>
```
>The scaffold command magically generates all the common things needed for a new resource for you! This includes controllers, models and views. It also creates the following basic actions: create a new resource, edit a resource, show a resource, and delete a resource.


---


### Link within template
``` html+erb
<a href='/demo/index'>index page</a>
<%= link_to(text, target) %>
<%= link_to('My link', '/demo/index') %>
<%= link_to('My link', {:controller => 'demo', :action => 'index'}) %>
<%= link_to('My link', {:action => 'index'}) %> <!-- don't need to include controller if you're staying in the current controller -->
```

## Controllers

#### Redirect
``` ruby
def index
  redirect_to({:action => 'index'})
end
```

#### Render Template Syntax
``` render

# Default: template matching the action name

def index
  render(:action => 'hello') # deprecated
end

def index
  render(:template => 'demo/hello') # explicit, but long
end

def index
  render('demo/hello') # common
end

def index
  render('hello') # makes the assumption of the controller
end
```

















## Useful Github Repos
- [Discourse](https://github.com/discourse/discourse)

## Useful Gems
- [Better Errors](https://github.com/charliesome/better_errors)
- [Devise](https://github.com/plataformatec/devise)
- [Sextant](https://github.com/schneems/sextant)
- [xray-rails](https://github.com/brentd/xray-rails)

## References
- Github
    - [rspec-rails](https://github.com/rspec/rspec-rails)
- [Lynda: Rails 3 Essential Training](https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=1&cad=rja&ved=0CD8QFjAA&url=http%3A%2F%2Fwww.lynda.com%2FRuby-on-Rails-3-tutorials%2Fessential-training%2F55960-2.html&ei=Bn2QUeNsgeGIAvOngKgB&usg=AFQjCNEdUAKfOjMrhD2ATGXSrhy4uAoY9w&bvm=bv.46340616,d.cGE)
- [RailsGuides: Rails Form helpers](http://guides.rubyonrails.org/form_helpers.html)

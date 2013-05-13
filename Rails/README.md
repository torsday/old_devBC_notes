# Rails


## Important Commands

#### Create a new app
``` rails new <name_of_project>```

##### The created directory tree 

```
.
├── app
│   ├── assets
│   │   ├── images
│   │   ├── javascripts
│   │   └── stylesheets
│   ├── controllers
│   ├── helpers
│   ├── mailers
│   ├── models
│   └── views
│       └── layouts
├── config
│   ├── environments
│   ├── initializers
│   └── locales
├── db
├── doc
├── lib
│   ├── assets
│   └── tasks
├── log
├── public
├── script
├── test
│   ├── fixtures
│   ├── functional
│   ├── integration
│   ├── performance
│   └── unit
├── tmp
│   ├── cache
│   │   └── assets
│   │       ├── CF0
│   │       │   └── DA0
│   │       └── E25
│   │           └── 4C0
│   ├── pids
│   ├── sessions
│   └── sockets
└── vendor
    ├── assets
    │   ├── javascripts
    │   └── stylesheets
    └── plugins
```

#### Launch server
```
rails server
rails s
```

#### generate scaffolding
```rails generate scaffold <name> <attribute>:<type>```
>The scaffold command magically generates all the common things needed for a new resource for you! This includes controllers, models and views. It also creates the following basic actions: create a new resource, edit a resource, show a resource, and delete a resource.



#### Link within template
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
- [Lynda: Rails 3 Essential Training](https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=1&cad=rja&ved=0CD8QFjAA&url=http%3A%2F%2Fwww.lynda.com%2FRuby-on-Rails-3-tutorials%2Fessential-training%2F55960-2.html&ei=Bn2QUeNsgeGIAvOngKgB&usg=AFQjCNEdUAKfOjMrhD2ATGXSrhy4uAoY9w&bvm=bv.46340616,d.cGE)
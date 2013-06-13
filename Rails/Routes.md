# Rails Routing
---

Routes are stored in config/routes.rb.
The priority of the routing is based on the order of creation (first created -> highest priority).

#### Routing and controller actions are decoupled in rails.
```ruby
AppName::Application.routes.draw do
end
```

#### Regular route
```ruby
# directs to the view method within the catalog_controller
match 'products/:id' => 'catalog#view'
```


#### Rails Resources
```ruby
resources :post
```
#### The resources method in the routes.rb file will create seven default RESTful routes, which include:
- http://guides.rubyonrails.org/routing.html#paths-and-urls

#### URL Helper
```HTML+ERB
<%= link_to "show all posts", posts_path %>
```
>posts_path returns /posts
new_post_path returns /posts/new
edit_post_path(:id) returns /posts/:id/edit
post_path(:id) returns /post/:id 

## INBOX

##### see what routes are available
```
rake routes
```

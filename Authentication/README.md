# Authentication
===================

## Sinatra

#### app/models/user.rb

``` ruby
class User < ActiveRecord::Base
  attr_reader :entered_password

  validates :name, :length => { :minimum => 3, :message => "must be at least 3 characters, fool!" }
  validates :entered_password, :length => { :minimum => 6 }
  validates :email, :uniqueness => true, :format => /.+@.+\..+/ # imperfect, but okay

  include BCrypt

  def password
    @password ||= Password.new(password_hash)
  end

  def password=(pass)
    @entered_password = pass
    @password = Password.create(pass)
    self.password_hash = @password
  end

  def self.authenticate(email, password)
    user = User.find_by_email(email)
    return user if user && (user.password == password)
    nil # either invalid email or wrong password
  end

end
```

#### Gemfile

``` ruby
gem 'bcrypt-ruby'
```

#### config/environment.rb

``` ruby
require 'bcrypt'
```

#### app/controllers/<controller>.rb

``` ruby
  get '/' do
    # render home page
    @users = User.all
    erb :index
  end

  #----------- SESSIONS -----------

  get '/sessions/new' do
    # render sign-in page
    @email = nil
    erb :sign_in
  end

  post '/sessions' do
    # sign-in
    @email = params[:email]
    user = User.authenticate(@email, params[:password])
    if user
      # successfully authenticated; set up session and redirect
      session[:user_id] = user.id
      redirect '/'
    else
      # an error occurred, re-render the sign-in form, displaying an error
      @error = "Invalid email or password."
      erb :sign_in
    end
  end

  delete '/sessions/:id' do
    # sign-out -- invoked via AJAX
    return 401 unless params[:id].to_i == session[:user_id].to_i
    session.clear
    200
  end


  #----------- USERS -----------

  get '/users/new' do
    # render sign-up page
    @user = User.new
    erb :sign_up
  end

  post '/users' do
    # sign-up
    @user = User.new params[:user]
    if @user.save
      # successfully created new account; set up the session and redirect
      session[:user_id] = @user.id
      redirect '/'
    else
      # an error occurred, re-render the sign-up form, displaying errors
      erb :sign_up
    end
  end
```

#### app/views/sign_in.erb

``` ruby
<div class="container">
  <h1>Sign In</h1>

  <% if @error %>
    <div class="errors"><%= @error %></div>
  <% end %>

  <form id="sign-in" method="post" action="/sessions">
    <label class="label" for="email">Email</label>
    <input type="email" name="email" placeholder="e.g., me@example.com" value="<%= @email %>"><br>
    <label class="label" for="password">Password</label>
    <input type="password" name="password" placeholder="6 or more characters">
    <br>
    <div class="submit"><input type="submit" value="Sign In"></div>
  </form>

</div>
```

#### app/views/sign_up.erb

``` ruby
<div class="container">
  <h1>Sign Up</h1>

  <div id="errors"><%= erb :_model_errors, :layout => false, :locals => { :model => @user } %></div>

  <form id="sign-up" method="post" action="/users">
    <label class="label" for="name">Name</label>
    <input type="text" name="user[name]" placeholder="e.g., joe" value="<%= @user.name %>">
    <span id="name-errors" class="errors"></span>
    <br>

    <label class="label" for="email">Email</label>
    <input type="email" name="user[email]" placeholder="e.g., me@example.com" value="<%= @user.email %>">
    <span id="email-errors" class="errors"></span>
    <br>

    <label class="label" for="password">Password</label>
    <input type="password" name="user[password]" placeholder="6 or more characters">
    <span id="entered_password-errors" class="errors"></span>    
    <br>

    <div class="submit"><input type="submit" value="Sign Up"></div>
  </form>

</div>
```


#### app/views/layout.erb

``` ruby
<!DOCTYPE html>
<html lang="en">
<head>
  <link rel="stylesheet" href="/css/normalize.css">
  <link rel="stylesheet" href="/css/application.css">

  <script src="//ajax.googleapis.com/ajax/libs/jquery/1.9.1/jquery.min.js"></script>
  <script src="/js/application.js"></script>

  <title></title>
</head>
<body>

  <nav>

    <div class="brand"><a href="/">Skills</a></div>

    <ul>
      <% if current_user %>
        <li><a id="sign-out" href="/sessions/<%= current_user.id %>">Sign Out</a></li>
      <% else %>
        <li><a href="/sessions/new">Sign In</a></li>
        <li><a href="/users/new">Sign Up</a></li>
      <% end %>
    </ul>

  </nav>

  <%= yield %>
</body>
</html>
```

#### app/helpers/sessions.rb

``` ruby
helpers do
  
  def current_user
    @user ||= User.find(session[:user_id]) if session[:user_id]
  end

end
```

#### public/js/application.js

``` js
$(document).ready(function () {

  // send an HTTP DELETE request for the sign-out link
  $('a#sign-out').on("click", function (e) {
    e.preventDefault();
    var request = $.ajax({ url: $(this).attr('href'), type: 'delete' });
    request.done(function () { window.location = "/"; });
  });

});
```


## References
-[phase_2_assessment_pt1](https://github.com/ctorstens/phase_2_assessment_pt1)
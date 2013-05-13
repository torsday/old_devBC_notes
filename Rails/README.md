# Rails

``` html+erb
< a href='/demo/index' >index page</a>
<%= link_to(text, target) %>
<%= link_to('My link', '/demo/index') %>
<%= link_to('My link', {:controller => 'demo', :action => 'index'}) %>
<%= link_to('My link', {:action => 'index'}) %> <!-- don't need to include controller if you're staying in the current controller -->
```

``` ruby
redirect_to({:action => 'index'})
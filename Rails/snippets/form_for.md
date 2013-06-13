# form_for

``` HTML+ERB
<%= form_for(:subject, :url => {:action => 'create'}) do |f| %>

<table summary='subject form fields'>
    <tr>
        <th>Name</th>
        <td><%= f.text_field(:name) %></td>
    </tr>
    ...
</table>
```
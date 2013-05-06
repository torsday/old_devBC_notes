# HTML
==========


## Passing in data
---

#### HTML
``` html
<form method="post" id="user-results" action="/results">
<ul>
<%@survey.questions.each do |question|%>
  <li><%=question.description%></li>
    <ol>
      <input type="hidden" name="results[<%= question.id %>][respondent_id]" value="<%= current_user.id %>" >
      <input type="hidden" name="results[<%= question.id %>][survey_id]" value="<%=@survey.id%>" >
      <input type="hidden" name="results[<%= question.id %>][question_id]" value="<%=question.id%>" >
      <%question.answers.each do |answer| %>
      <li> <input type="radio" name="results[<%= question.id %>][answer_id]" value="<%=answer.id%>"> <%= answer.description %> </li>
      <% end %>
    </ol>
<% end %>
</ul>
<input type="submit" value="FINISH THIS">
</form>
```

#### Javascript catches the submit
``` js
  // SUBMIT ANSWERS TO QUESTIONS 
  $('#user-results').submit(function(data){
    data.preventDefault();
    $.post('/results', $('#user-results').serialize(), function(data){
    }).done(function(data){
      $("#survey-box").html(data);
    });
  })
```

#### and AJAX's it to the controller
``` ruby
post "/results" do
  content_type :json
  params[:results].each do |key, value|
    Result.create(params[:results][key])
  end
  
  @user = User.find(session[:user_id])
  (erb :completed_survey, :layout =>false).to_json
end
```



## References
- [MDN: HTML Elements](https://developer.mozilla.org/en-US/docs/HTML/Element)
  - [MDN: input](https://developer.mozilla.org/en-US/docs/HTML/Element/input)
  - [MDN: form](https://developer.mozilla.org/en-US/docs/HTML/Element/form)
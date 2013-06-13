# AJAX
======

## Examples

#### example.js
---

``` js
$(document).ready(function(){

  $('#get_color').on("click", function (e) {
    e.preventDefault

    $.ajax({
      type: 'post',
      url: '/colors'
    }).done(function (data) {
      console.log("Cell: " + data.cell);
      console.log("Color: " + data.color);
      // debugger
      $('#color_me li:nth-child(' + data.cell + ')').css('background-color', data.color);
    });

  });

});
```


#### example.rb (controller)
---

``` ruby
post '/colors' do

  #Create and return a JSON object with the random cell and color given below.
  content_type :json

  cell = rand(1..9)
  color = "#" + "%06x" % (rand * 0xffffff)
  return {:cell => cell, :color => color}.to_json
end
```

## References
---
- [Phase 2 Assessment Part 3](https://github.com/ctorstens/phase_2_assessment_pt3.git)
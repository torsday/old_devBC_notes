# [The CoMPuTaH Web App Architecture](https://gist.github.com/quackingduck/a2d7c25baabe8d6fffd7)

*The original repo of this can be found* **[here](https://gist.github.com/quackingduck/a2d7c25baabe8d6fffd7)**

When working on a web app using a framework like Rails or Backbone I split the kind of components I write into five broad groups:

* Controllers
* Models
* Presenters
* Templates
* Helpers

## Controllers

Modules with methods that receive information from the user interface layer, do something with that information and then render an updated user interface.

    MainScreen.render() # screen shown to user
    MainScreen.removeTodoList(id) # list removed then screen shown to user

Updating a user interface is an irreversible side-effect.

## Models

Modules with methods that take a query as input (or build one with some DSL) and return pure data (or objects that wrap data plus and have some methods that lazily load more data) as output.

    data = Todos.where(:user => myles).incomplete.all()
    data #=> [ { :id => 1, :title => 'Book flights to Chicago' ... } ... ]

## Presenters

Modules that take data as input and return interface descriptions as output. HTML is an interface description because it is data encoded in such a way that another program (the browser) can turn it into a interface.

    CompletedTodoList.render(todoListData) #=> '<div class="todo-list" ...'

Rendering an interface description (like HTML) is not an irreversible side-effect.

## Templates

A template is just a string with special syntax that says "this part of the string should be replaced with something else". A _compiled template_ is a template that has been turned into a function that takes a presenter object as input and returns a string with all the appropriate subsitutions made as output.

    template = "Hello {{name}}"
    compiledTemplate = TemplateSystem.compile(template)
    compiledTemplate(personPresenter(personModelData)) # => "Hello Myles"

Templates should have no logic in them. Use [mustache](http://mustache.github.io/).

## Helpers

A logical grouping of functions that may have begun life as part of a specific presenter, model or controller but was extracted out so it could be tested in isolation and shared amongst different modules in the system.

    # Helpers used by a View
    domQuery = CreateDOMQuery().class('todo-list').attr('data-id',1)
    // => ".todo-list[data-id='1']"

    QueryDOM(element, domQuery) // => < Element div, class='todo-list' ... >

    # Helper used by a Presenter
    RelativeDateFormatter.timeAgoInWords(time) // => "4 days ago"
    RelativeDateFormatter.timeAgoInWords(Time.now()) // => "just now"

    # Helper used by a Model
    SQLQueryBuilder
      .relation(person.collection)
      .filter('name': "Myles")
      .fields('name')
      // => "SELECT name FROM people WHERE name = 'Myles'"

Helpers also go by "libraries". Most of your code should be in helpers.

 * * *

# Relationships Between Components

The diagram of "who knows about who" look something like:

    Controllers
      Helpers
      Models
        Helpers
      Presenters
        Helpers
        Templates

To do its job, a controller may use one or more helpers, models and presenters. A model may use one or more helpers (in this case the "help" would be things like formatting an SQL query). A presenter uses one or more helpers or templates. Note that templates do _not_ use helpers. Helpers can also use other helpers.

# CoMPuTaH Architecture as Mapped to Rails and Backbone

Rails:

* Controllers - ActionPack Controllers
* Models - ActiveRecord Models
* Presenters - no direct mapping, this job ends up getting performed by all the other modules
* Templates - ERB templates (that are extra complicated because they must act as presenters)
* Helpers - any ruby module or class can implement a helper and can be used at any layer, rails emphasises helpers in template rendering contexts and test contexts but they are useful everywhere

Backbone:

* Controllers - Views
* Models - Models and Collections
* Presenters - no direct mapping, this job ends up getting performed by all the other modules
* Templates - Underscore templates, Mustache etc
* Helpers - any javascript object can implement a helper

* * *

# FAQ

> What happened to MVC? MVC sounds way better

Agreed.

> Why does the C come first?

Because you can implement a (poorly architected) app with just the Controller. That's not true of the other components. Therefore it gets to headline the acronym.

> So Backbone models are pretty much like Rails models?

Not really. The biggest difference is that BB models are asyncronous.

    # Rails
    myModel.save()
    log(myModel) # if myModel is valid then by this line it's been saved

    # BB
    myModel.save()
    log(myModel) # myModel will *not* have been saved to the backend yet

The upshot of this is that rendering in Backbone can appear to happen "backwards". For example some function may be running in the background polling a backend for changes to a model, when the backend sends back changed attributes the `model.save` will cause the model to trigger a `change` event, then some view that is subscribed to this event may decide to render itself. This isn't the kind of thing that happens with Rails models.

> So Views/Controllers make user interfaces and so do presenters? What's the difference again?

The main difference is this: controller methods have irreversible side-effects.

For example a rails controller method could update the value on some model. Then another another applicaiton connected to the same database could show the user that new value. That can't be undone.

When a rails controller writes an HTTP response, that's an irreversible side-effect.

When a BB view renders the presenter html to the dom or toggles on a class on some element, that's an irreversible side-effect.

> Okay, so what's the difference between a presenter and a compiled template again? Aren't they both just functions that take data and return HTML?

They are both functions that take data and return HTML. However a presenter can run the data through helpers (to reformat it) before passing it to the template (to put it in the right spot). Pieces of a presenter can be tested in isolation but a template must be tested as a whole.

> I've heard some Rails people say "skinny controllers, fat models" so most of my code should be in the models right?

No. In a large well-factored application, most of your code should be in helpers and pretty much all of your value should be in the data.

Think of controllers, models, and presenters as glue (or duct tape). Many great things are built _with_ glue but no great things are build _from_ glue.

Even if it's really really awesome glue and every year there's an awesome conference about it and all the cool companies only want to hire people who are expert users of this amazing glue. Even then.

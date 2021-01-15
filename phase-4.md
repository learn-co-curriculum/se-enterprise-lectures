### Phase 4

- [Rails Intro](#intro)
- [Rails Associations](#associations)
- [Rails Forms REST](#forms-rest)
- [Rails Forms Advanced](#forms-advanced)
- [Rails Forms Associations](#forms-associations)
- [Rails Forms Validations](#forms-validations)
- [Rails Review](#rails-revew)
- [Rails Sessions and Cookies](#sessions)
- [Rails Authorization](#authentication)
- [React JWT Auth 1](#jwt1)
- [React JWT Auth 2](#jwt2)

## Lecture Notes

---
title: Rails Intro
layout: post
---

# <a id="intro">rails-intro</a>

> TODO: Incorporate these notes

* Intro to Rails [Notes](https://github.com/learn-co-curriculum/web-051517/blob/master/Module-2/Intro-Rails.md)

## SWBATs

* Create a new Rails application
* Describe similarities between Sinatra routing & Rails routing
* Generate a controller
* Create actions/methods for a RESTful controller
* Create views
* Generate a model
* Create routes

## Resources

* [Example Video](https://youtu.be/1CD5iniV_00)
* [Starter Code](https://github.com/learn-co-curriculum/lectures-starter-code/tree/master/rails/rails-intro)

## Outline

```text
10m What is Rails (10 mins)
10m A blog in 10 mins (10 mins)
10m Codealong: Installing Rails (5 mins)
 5m Create a rails app
 5m Generate a controller
 5m Create Views
 5m Generate a model
 5m Generate a migration
 5m Conclusion
===
60m Total
```

### What is Rails

Instructors like to show [this video](https://www.youtube.com/watch?v=9ML8PrP3A8E) as a way to introduce rails. You see all of the pain that goes into a Sinatra application, and then show `rails new` and `rails g` and everything becomes easier!

Rails was created in 2003 by David Heinemeier Hansson, while working on the code base for Basecamp, a project management tool by 37signals. David extracted Ruby on Rails and officially released it as open source code in July of 2004. Despite rapid iteration of the Rails code base throughout the years, it has stuck to three basic principles:

* Ruby Programming Language
* Model-View-Controller Architecture
* Programmer Happiness

Rails was created with the goal of increasing programmers' happiness and productivity levels. In short, with Rails you can get started with a full-stack web application by quickly creating pages, templates and even query functions.

Rails heavily emphasizes _**"Convention over Configuration."**_ This means that a programmer only needs to specify and code out the non-standard parts of a program. Even though Rails comes with its own set of tools and settings, you're certainly not limited to library of rails commands and configurations. Developers are free to configure their applications however they wish, though adopting conventions is certainly recommended.

![](https://s3-us-west-2.amazonaws.com/student-resources/uploads/lecture/Screen+Shot+2017-06-09+at+10.04.20+AM.png)

#### A Look Back

As we look back at the history of Rails, let's review some of the more significant releases over the years.

* Rails 1.0 \(Dec 2005\) - Mostly polishing up and closing pending tickets from the first release along with the inclusion of Scriptaculous 1.5 and Prototype 1.4.
* Rails 1.2 \(Jan 2007\) - REST and generation HTTP appreciation
* Rails 2.0 \(Dec 2007\) - Better routing resources, multi-view, HTTP basic authentication, cookie store sessions
* Rails 2.0 \(Nov 2008\) - i18n, thread safe, connection pool, Ruby 1.9, JRuby
* Rails 2.3 \(Mar 2009\) - Templates, Engines, Rack
* Rails 3.0 \(Aug 2010\) - New query engine, new router for controller, mailer controller, CRSF protection
* Rails 3.1 \(Aug 2011\) - jQuery, SASS, CoffeeScript, Sprockets with Assets Pipeline
* Rails 3.2 \(Jan 2012\) - Journey routing engine, faster development mode, automatic query explains, tagged loggin for multi-user application
* Rails 4.0 \(June 2013\) - Rails 4.2: Active Job, Asynchronous Mails, Adequate Record, Web Console, Foreign Keys.
* Rails 5.0 \(June 2016\) - Notable additions in Rails 5.0 include an option for an API-only application suitable for use as a backend to JavaScript or mobile applications. Also Action Cable for live features such as chat and notifications.

Over the years, Rails has indeed made it easier for beginners to dive into web development and build large complex applications. Some popular websites built on Rails include Twitter \(at one point\), GitHub and, of course, 37signals' very own Basecamp. Although it has often been criticized for performance and bloat, Rails continues its iterations with an ever-growing developer community and a vibrant ecosystem.

[Built With Rails](https://skillcrush.com/2015/02/02/37-rails-sites/)

### A blog in 10 mins

The goal of the next few minutes is to show the power that Rails gives us – it's actually possible to create a website with a lot of the functionality you've seen in our Sinatra app – forms, links, database, and MVC structure – in less than 5 minutes. We will not detail each step for this app, but we will create a dynamic website in 5 mins by typing the following commands.

I'll talk through this as I demo, and we'll come back and talk about what each of these steps are doing afterwards.

```ruby
rails new blog_app
cd blog_app
rails generate scaffold Post title:string content:text author:string
rake db:migrate
rails server
```

Now we'll head over to `localhost:3000/posts`. All of our REST actions are live!

### Codealong: Installing Rails

#### Let's install rails

```bash
  gem install rails
```

Versions of Rails change quite rapidly, and if you leave off the "-v", you'll just get the latest version. Be specific if you want a specific version.

```bash
  gem install rails -v=INSERT_RAILS_VERSION_HERE
```

### Create a rails app

For this introduction, we want to create a simple app: a petstore! The specs for this app are as follows:

* Display a list of all pets
* Create new pets and edit existing pets
* Delete pets

Rails follow a pattern called **"convention over configuration"** - this means that by default, a Rails app expects you to follow specific patterns and folder structures. This means you need to learn these conventions, but also means that once you learn them, you save time by not having to setup a lot of the configuration you'd otherwise need to set up manually.

This structure may look a bit complex – there a lot of files, specific naming conventions, and some nested files and folders. We generally don't create this structure manually, but instead use the Rails command line tool, which initializes the app for us:

```bash
  rails new petstore
```

> **Note:** By default, if you _do not_ add any option for the database, Rails will create the app with SQLite3. While you are working in a local development environment \(localhost\), you won't notice much of a difference between SQLite3 and PostgreSQL.
>
> Once your app is in production on a remote server, you will _not_ use SQLite, and they will often use PostgreSQL. A best practice in web development is to keep development and production environments as similar as possible, so we recommend using PostgreSQL from the start.

Now, let's go into the petstore folder:

```bash
  cd petstore
```

Let's look at the contents of this folder \(using `ls`\), and take a look at the files and folders that were magically created by the `rails new` command:

```text
├── app
├── bin
├── config
├── db
├── lib
├── log
├── public
├── test
├── tmp
└── vendor
```

Some details about this structure:

* 90% of the web app code will be inside the folder `app`, including all of our model, view, and controller logic.
* `config` contains all the credentials for the DB and other 3rd party services, all the deployment settings, and the specs about how to serve this app over HTTP.
* `db` will contain all of your migrations

We will describe the other folders in later lessons, and for the next couple of weeks, you will primarily write code inside the folders described above.

#### Rails Routing vs. Sinatra Routing

As you know, a "route" is a combination of **the path** that was requested and **the HTTP verb** that was used to request that path.

```text
                                          -----> Model <----> DB
                                         |         |
            response        request      |         |
   Browser <-------- router -------> controller <--
                             GET         ^
                             PUT         |
                             POST         -----> view <----> html/images/css/js
                             DELETE
```

When we've used Sinatra, we were managing the routes and the code executed for a specific route in the same place:

```ruby
    get "/pets" do
        # Here is the code that will be executed when the client requests /books
    end
```

This is handy for us as developers, because it allows us to keep everything in the same place - routing and controller logic - but if the app grows it can get unreadable. Imagine, for example, an app that has 20 or 30 different routes... your main routes file could contain a lot of complex code.

Rails has a "routing engine" that separates the routing logic from the controller logic \(what we want to happen when routes are requested\). The configuration for this routing engine is in the file `config/routes.rb`.

```ruby
Rails.application.routes.draw do

end
```

Everything between the `do` and the `end` will be code related to handling routes for the current application.

Later on in this lesson, we will add some content in this file, and in a later lesson, we will go into detail about handling routes inside a Rails application.

### Generate a controller

As Rails is an MVC framework, we will need to have controllers to handle requests and call the database through models.

In Rails, the controllers are files inside the folder `app/controllers`. If you open this folder, you will see that one controller is already here: the file `application_controller.rb`. This controller does not directly handle HTTP requests, but rather serves as a link between all the controllers we will create, `application_controller.rb` will be the parent of all the controllers in our app.

There is 3 different ways for creating a controller in Rails:

1. We can manually create a file and write the ruby code inside it.
2. We can use a generator called `controller`, using `rails g controller CONTROLLER_NAME [ACTIONS]`. For instance, if we want to create a controller for the resource `pets` with an action and a view for `index` and `show`, we would type in the console `rails g controller pets index show`. This command would create a bunch of files and modify some others:
   * The controller itself, `pets_controller.rb` inside `app/controllers`
   * The views for each method , in this case
     * `app/views/index.html.erb`
     * `app/views/show.html.erb`
   * The routes handlers for these two actions will also be added to config/routes.rb :
     * `get '/pets/index', to: 'pets#index'`
     * `get '/pets/show', to: 'pets#show'`
3. We can use the `scaffold_controller` generator. This generator will create the same files as the previous generator but with a REST logic for views, controller and views.

#### Create methods for a RESTful controller

We've already defined what a RESTful resource is, let's see how to implement it in a rails app.

As a reminder, a RESTful resource will include 7 methods:

* Index
* Show
* New
* Create
* Edit
* Update
* Delete

Rails has a generator called `scaffold` that will create the whole MVC structure for a resource, let's say that inside the petstore app, we want the `Pet` resource to have a title and a content field, we would type:

```ruby
rails g scaffold Pet name:string animal:string
```

Running this command will generate a lot of files, including the controller, the views, the model, and the migration. It will also update the routes file.

Take a look at the controller, it has all the RESTful methods, and these methods already contain the code to query the database through the model `Pet`.

We don't want all the files created with the scaffold and in practice you won't actually use it so let's delete it

```ruby
rails d scaffold Pet
```

Let's go ahead and generate a new Pets controller.

### Create views

There is no specific generator that will create only a view file, but you can add them manually into the appropriate folder inside views.

For instance, if we want to add a view file `about` for the resource `Pet`, we can create a file `about.html.erb` in `app/views/pets`.

If a view is "static" - as in, it doesn't use any instance variables created in the controller - you can just create a route for this view and rails will render it in the browser even if there is no method in the controller:

In config/routes.rb

```ruby
get "/pets/about", to: 'pets#about'
```

If there is a file `about.html.erb` in `app/views/pets`, this file will be automatically rendered when you call `localhost:3000/pets/about`

#### Implicit vs Explicit Rendering

Thanks to Rails conventions, we do not need to specify the view file to render in our controller. This is known as implicit rendering

In app/controllers/pets

```ruby
  def index
  end
```

However, if we wanted to be more explicit or if we wanted to rendr a view template that does not correspond with the action name we could do the following:

```ruby
  def index
    render 'cats'
    # This will render cats.html.erb
  end
```

### Generate a model

Sometimes, you will need a model but not the related controller, in this case, you will use the model generator:

```text
rails g model MODEL_NAME [fields]
```

This will generate the model by itself along with the migration containing all the fields and the data types if you wrote them when you typed the console.

### Generate a migration

In Sinatra you had to create your migrations by hand. As with most things in Rails, theres an generator for that.

```ruby
rails g migration AddAgeToPets age:integer
```

By following certain conventions like the one above, rails will generate a migration that specifically adds the age column to your existing pets column.

```ruby
class AddAgeToPet < ActiveRecord::Migration[5.1]
  def change
    add_column :pets, :age, :integer
  end
end
```

### Conclusion

Rome wasn't built in a day and neither can someone learn Rails in a day. Keep coding and it will all come together.

[Rails Guides](http://guides.rubyonrails.org/index.html)

---
title: Rails Associations
layout: post
---

# <a id="associations">Rails Associations</a>

## SWBATs

## Resources

* [Example Video](https://youtu.be/FrXjK9M9FfM)
* [Starter Code]()

## Outline

---
title: Rails Forms
layout: post
---

# ActiveRecord Validations

## Objectives


By the end of this lecture students should feel more comfortable with working with forms. This is a good opportunity to go over the creation of forms using `form_for`

Why do we use Validations? Because users suck

![](https://media.giphy.com/media/ZfU11ODanloCA/giphy.gif)

## Resources
Starter Code: https://github.com/learn-co-students/web-103017/tree/master/13_rails_forms/docoffice
Video: https://youtu.be/73fjjOpH6uM

## Steps


### Introduction (20 mins)

Set up a project with full built out CRUD/Restful actions. `index`, `show` actions can be covered very quickly. Spend time working through `new` and `create`. Illustrate the problem of bad input. We want a student to see that if we do not fill out information it is easy to create a form. Additionally if you build out `edit` and `update` they will see how easy it is to change the data.

*Note* This is a good oppurtunity to talk about the various levels of validation. Frontend Validation i.e Forms themselves, Validation in code, Database Contraint.


### Validations (25 mins)

Spend the rest of the time showing students how they can write validations in their models which will prevent the creation of a project without the validations passing.

For example

```

# dog.rb

class Dog
  validates :breed, presence: true
end


# dogs_controller.rb


def create

  @dog = Dog.new(name: params[:name], breed: params[:breed])
  if @dog.valid?
    @dog.save
    redirect_to dog_path(@dog)
  else
    # Flash allows you to display errors on the page
    # It persists from one request to the next

    flash[:errors] = @dog.errors.full_messages # gives you an array of error messages corresponding to the validations 9

  end

end


# OR


def create

  @dog = Dog.new(name: params[:name], breed: params[:breed])
  if @dog.save
    @dog.save
  else

    flash[:errors] = @dog.errors.full_messages
  end

end
```

*Note* Walk students through a couple of the validations on the Rails Guides documentation and show them how to try new ones. It is helpful for them to see how easy this is. Reiterate that this not something you simply memorize but something you work on and get practice with.


### Strong params

This lecture is also a good opportunity to dive into strong params. Because of issues with mass assignment Rails does not allow you to initialize with params therefore you must use strong params


```
  def create
    # Include validation...
    @dog = Dog.create(dog_params)
  end

private
  def dog_params
    params.require(:dog).permit(:name, :breed)
  end

```
It could also be cool to show students how the return of `dog_params`. Rails changes the params to `permitted:true`

## References
 * [Railsguides - AR Validations](http://guides.rubyonrails.org/active_record_validations.html)

 ---
title: Rails Forms Rest
layout: post
---

# <a id="forms-rest">rails-forms-rest</a>

## SWBATs

* Discuss and Review Forms
* form_for, form_tag, link_to, button_tag, submit_tag
* Strong params
* Checking information before creating

## Resources

* [Example Video](https://www.youtube.com/watch?v=h4aJ3OFnNDk)
* [Starter Code](https://github.com/learn-co-curriculum/lectures-starter-code/tree/master/rails/rails-forms-rest)
* [Security](http://guides.rubyonrails.org/v3.2.8/security.html)
* [Rails Guides](http://edgeguides.rubyonrails.org/active_record_validations.html)
* [Form For](https://guides.rubyonrails.org/form_helpers.html#binding-a-form-to-an-object)
* [Rails Strong Params](https://edgeguides.rubyonrails.org/action_controller_overview.html#strong-parameters)

## Outline

```text
15m Create a new application
20m Build CRUD using REST
15m Mass Assignment
10m Refactor with before_action
===
60m Total
```


# Private Keyword

[Read this (very short) article](http://ruby-for-beginners.rubymonstas.org/advanced/private_methods.html)

### Create a new application

`rails new docoffice`

Create a new model Doctor `rails g model Doctor name speciality`

Create a new model Patient `rails g model Patient name condition`

Create the routes for both

> You may use the `resources` keyword but use the `only` keyword to define only the actions you will be using

Create your controllers

```ruby
class DoctorController < ApplicationController
  def index
    @doctors = Doctor.all
  end


  def show
    @doctor = Doctor.find(params[:id]
  end


  def new
    @doctor = Doctor.new
  end


  def create
    @doctor = Doctor.create(name: params[:doctor][:name], speciality: params[:doctor][:speciality])
  end

  def edit
    @doctor = Doctor.find(params[:id])
  end


  def update
    @doctor = Doctor.find(params[:id])
    @doctor.update(name: params[:doctor][:name], speciality: params[:doctor][:speciality])
  end
end
```

Create your corresponding views

```text
# new.html.erb
  <%= form_for @doctor do |f| %>
    <%= f.label :name %>
    <%= f.text_field :name %>


    <%= f.label :speciality %>
    <%= f.text_field :speciality %>

    <%= f.submit %>
  <% end %>
```


## Mass Assignment & Strong Params

This lecture is also a good opportunity to dive into strong params. Because of issues with mass assignment Rails does not allow you to initialize with params therefore you must use strong params

```ruby
# doctors_controller.rb

  #...

  def create
    @doctor = Doctor.new(doctor_params)
    if @doctor.valid?
      @doctor.save
    else
      render 'new'
    end
  end

  # ...

  private

  def doctor_params
    params.require(:doctor).permit(:name, :speciality)
  end

end
```

It could also be cool to show students how the return of `dog_params`. Rails changes the params to `permitted:true`

### Refactor with before_action

Refactor your controllers
 Notice the number of times `Doctor.find(params[:id])` is used

We can make sure that block of code is executed before each of the controller#actions that need it like :show,:edit,:update,:destroy
```ruby
class DoctorController < ApplicationController

  def index
    @doctors = Doctor.all
  end

  def show
    find_doctor
  end

  def new
    @doctor = Doctor.new
  end

  def create
    @doctor = Doctor.create(name: params[:doctor][:name], speciality: params[:doctor][:speciality])
  end

  def edit
    find_doctor
  end

  def update
    find_doctor
    @doctor.update(name: params[:doctor][:name], speciality: params[:doctor][:speciality])
  end

  def destroy
    find_doctor
    @doctor.destroy
    redirect_to doctors_path
  end

  private

  def find_doctor
    @doctor = Doctor.find(params[:id]
  end
end
```
* [Chapter 8 Filters](https://guides.rubyonrails.org/action_controller_overview.html)
Or you can refactor into the
`before_action :find_doctor`

```ruby
class DoctorController < ApplicationController
  before_action :find_doctor

  def index
    @doctors = Doctor.all
  end

  def show
  end

  def new
    @doctor = Doctor.new
  end

  def create
    @doctor = Doctor.create(name: params[:doctor][:name], speciality: params[:doctor][:speciality])
  end

  def edit
  end

  def update
    @doctor.update(name: params[:doctor][:name], speciality: params[:doctor][:speciality])
  end

  def destroy
    @doctor.destroy
    redirect_to doctors_path
  end

  private

  def find_doctor
    @doctor = Doctor.find(params[:id]
  end
end
```


---
title: Rails Review
layout: post
---

# <a id="rails-review">rails-review</a>

## SWBATs

* Create Full CRUD application
* Utilize Rails Generators properly
* Establish appropriate relationships between models
* Build forms using rails helpers (form_for, form_tag)
* Refactor - before_action and `_form` partial
* Explain RESTful routing outside of just using `resources :model_name`


## Resources

* [Example Video](https://youtu.be/15UDFMwWHU8)
* [Starter Code](https://github.com/learn-co-curriculum/lectures-starter-code/tree/master/rails/rails-review)

## Outline

#### Build a Full Crud Application

---
title: Rails Sessions And Cookies
layout: post
---

---
title: Rails Forms Validations
layout: post
---

---
title: Rails Forms Advanced
layout: post
---

# Further Forms & Validations

## Objectives

1. Discuss and Review Forms
2. Strong params
3. Checking information before creating

## Prerequisites

A student should be able to:

1. Set up their own routes
2. Create a form using form_for
3. Create their own models

# Instructions

1. Create a new appication
   `rails new docoffice`
2. Create a new model Doctor
   `rails g model Doctor name speciality`
3. Create a new model Patient
   `rails g model Patient name condition`
4. Create the routes for both
   * You may use the `resources` keyword but use the `only` keyword to define only the actions you will be using
5. Create your controllers

```
class DoctorController < ApplicationController
  def index
    @doctors = Doctor.all
  end


  def show
    @doctor = Doctor.find(params[:id]
  end


  def new
    @doctor = Doctor.new
  end


  def create
    @doctor = Doctor.create(name: params[:doctor][:name], speciality: params[:doctor][:speciality])
  end

  def edit
    @doctor = Doctor.find(params[:id])
  end


  def update
    @doctor = Doctor.find(params[:id])
    @doctor.update(name: params[:doctor][:name], speciality: params[:doctor][:speciality])
  end
end
```

6. Create your corresponding views

`new.html.erb`

```
  <%= form_for @doctor do |f| %>
    <%= f.label :name %>
    <%= f.text_field :name %>


    <%= f.label :speciality %>
    <%= f.text_field :speciality %>

    <%= f.submit %>
  <% end %>
```

7. Let's add some validations for your model

> Why Use Validations?
> Validations are used to ensure that only valid data is saved into your database. For example, it may be important to your application to ensure that every user provides a valid email address and mailing address. Model-level validations are the best way to ensure that only valid data is saved into your database. They are database agnostic, cannot be bypassed by end users, and are convenient to test and maintain. Rails makes them easy to use, provides built-in helpers for common needs, and allows you to create your own validation methods as well. - [Rails Guides](http://edgeguides.rubyonrails.org/active_record_validations.html)

`song.rb`

```
class Song < ApplicationRecord
  validates :title, presence: :true
  validates :runtime, numericality: { greater_than_or_equal_to: 1}
end
```

8. Let's fix our controllers

```
  def create

    @doctor = Doctor.new(name: params[:doctor][:name], speciality: params[:doctor][:speciality])
    if @doctor.valid?
      @doctor.save
    else
      render 'new'
    end
  end
```

9. Mass Assignment

At the bottom of `doctors_controller.rb`

```
  private
    def doctor_params
      params.require(:doctor).permit(:name, :speciality)
    end
  end
```

```
  def create
    @doctor = Doctor.new(doctor_params)
    if @doctor.valid?
      @doctor.save
    else
      render 'new'
    end
  end
```

## Resources

* [Security](http://guides.rubyonrails.org/v3.2.8/security.html)
* [Rails Guides](http://edgeguides.rubyonrails.org/active_record_validations.html)

---
title: Rails Form Associations
layout: post
---

# <a id="rails-associations">Rails Associations</a>

## SWBATs

* Refresher on has_many and belongs_to
* Use Rails form helper methods that create an associated object
* Implement dependent: :destroy in order to destroy associated objects to normalize database


## Resources

* [Example Video](https://youtu.be/FrXjK9M9FfM)
* [Starter Code](https://github.com/learn-co-curriculum/lectures-starter-code/tree/master/rails/forms-associations)


## Outline

```text
20m Create a new application
5m Review Active record associations (has_many, belongs_to)
20m Build form using form_for :object and f.collection select
===
45m Total
```


### Create a new application

`rails new flavortown`

Introduce scaffold generator and explain difference between model, controller, resources and scaffold generators.

Create a new model Doctor `rails g resources User name`
Create a new model Doctor `rails g resources Post name user_id:integer`

migrate:
`rails db:migrate`

Add the appropriate relationships

Stress the importance of dependent destroy
What happens when you delete an instance without dependent: :destroy?
```ruby
class User < ApplicationRecord
  has_many :posts, dependent: :destroy
  # provide methods like User#posts
end

class Post < ApplicationRecord
  belongs_to :user
end

```

Create the form using the DIY method first and relate it to sinatra

```html
<!-- DIY f.collection_select -->
  <select name="post[user_id]">
    <% User.all.each do |user| %>
      <option value="<%= user.id %>">
        <%= user.name %>
      </option>
    <% end %>
  </select>
```

Then show them the RAILS WAY™️
```ruby
  <%= form_for(@post) do |f| %>
    <%= f.label :title %>
    <%= f.text_field :title %>

    <%= f.label :content %>
    <%= f.text_area :content %>

    <%= f.label :user %>

      # First arg is method we want to call on @post (:user_id),
      # Second The collection we want to use to populate the dropdown(User.all),
      # Third The value we want in our params: User#id,
      # Fourth What do we want to display in the tag itself? User#name

  <%= f.collection_select(:user_id, User.all, :id, :name) %>
  <%= f.submit %>
<% end %>
  ```


Be sure to _break_ the collection select and replace each of the arguments and show how they change the params


# <a id="forms-validations">Rails Forms and Validations</a>

## SWBATs

* Explain the difference between render and redirect
* Create server side validations using Active record
* Validate different data types i.e. string, numericality, boolean
* Create custom validations
* Implement the Flash Hash to render error messages

## Resources

* [Example Video](https://www.youtube.com/watch?v=I_FBuK5XxZA)

* [Example Video 2](https://youtu.be/H9LdhJ5HKlg)

* [Starter Code](https://github.com/learn-co-curriculum/lectures-starter-code/tree/master/rails/rails-forms-validations)

## Outline


```text
20m Create a new application
10m Display errors with @ errors
10m Explain Flash hash
10m Display errors with flash[:errors]
===
50m Total
```


## Why Use Validations?

### Validations

- This is your typical user:
  ![Your users on your site](https://camo.githubusercontent.com/bd5a0e0355fa6a8c1f5478f197be5562a479d41a/68747470733a2f2f6d656469612e67697068792e636f6d2f6d656469612f5a665531314f44616e6c6f43412f67697068792e676966)


We want to make sure our app is being used the right way:

Validations are used to ensure that only valid data is saved into your database. For example, it may be important to your application to ensure that every user provides a valid email address and mailing address. Model-level validations are the best way to ensure that only valid data is saved into your database. They are database agnostic, cannot be bypassed by end users, and are convenient to test and maintain. Rails makes them easy to use, provides built-in helpers for common needs, and allows you to create your own validation methods as well.

- We want to protect against unwanted, unexpected data. We should be programming defensively

- For example, would it make sense for our app to allow a bagel with an empty name to be created?

- ActiveRecord provides us _several_ built in validations and I **highly recommend reading the docs** [Rails Guides](http://edgeguides.rubyonrails.org/active_record_validations.html)

- If we need custom functionality, we can also write our own methods

- These validations will be run **any time i try to write to the database** => `Bagel.create`, `@bagel.update`, `@bagel#save`

```ruby
# validations occur in the model/bagel.rb
class Bagel < ApplicationRecord
  # validates the requirement for name to BOTH be a non empty string and unique
  validates(:name, { presence: true, uniqueness: true })
  # validates :price, numericality: { presence: true, only_integer: true }

  # Custom validations
  validate :validate_num_for_price

  def validate_num_for_price
    # call the attribute you want to validate then put in conditions
    if self.price.class != Fixnum || self.price > 30
      # Add errors to the error's array
      errors.add(:price, "Needs to be a number less than 30")
      # errors array -> [{price: "Needs to be a number less than 30"}]
    end
  end

end
```

_Note_ Walk students through a couple of the validations on the Rails Guides documentation and show them how to try new ones. It is helpful for them to see how easy this is. Reiterate that this not something you simply memorize but something you work on and get practice with.



### Annotated BagelsController

```ruby
class BagelsController < ApplicationController

  # show ALL bagels
  def index
    @bagels = Bagel.all #ask Bagel model for data and pass @bagels instance var to the view
    render :index # look for folder called /bagels in the views folder, then render the index.html.erb
  end

  # show form to create a new bagel
  def new
    @bagel = Bagel.new # create a blank instance to pass to form_for
    render :new # render app/views/bagels/new.html.erb
  end

# POST request from our new bagel form
# create is called when our app receives a POST request to /bagels
  def create
    #@bagel = Bagel.create(bagel_params)
    # this would remove the need to call .new and then .save

    @bagel = Bagel.new(bagel_params) # pass in return value of private bagel_params method, which is a hash of whitelisted attributes

    if @bagel.valid? # checking validations; method is provided by ActiveRecord => returns boolean
      @bagel.save # if bagel is valid, save to database
      flash[:notice] = 'Bagel created!' # save a notice for our user in the flash hash
      redirect_to(bagels_path) # redirect fires new GET request, which will hit the BagelsController#index
    else # if bagel is not valid
      # set the errors into an instance variable to pass to view
      # @errors = @bagel.errors.full_messages
      # because I am not redirecting, instance var @bagel maintains the attributes from the form
      #render(:new) # render DOES NOT TRIGGER NEW GET REQUEST but will change the URL based on the form submission route
      # because render(:new) is NOT a new get request, I don't need to send a flash along

      # rails provides a method for sending data across multiple requests
      # we can access this via flash[:KEY] hash syntax
      flash[:errors] = @bagel.errors.full_messages

      # Should be REDIRECTING because you want to keep the same URL in the event the user decides to hit refresh on the browser
      # Check the terminal logs and see the POST, the rollback transaction then the redirect status 300 then the NEW GET REQUEST
      # Important to note with the NEW GET request the previous "state" is gone and @bagel will be from the show page which is @bagel.new
      redirect_to new_bagel_path
    end
  end

#everything below private keyword is private
private
  def bagel_params
    # return a hash of whitelisted attributes from params
    params.require(:bagel).permit(:name, :price, :tasty)
    # strong params returns a hash of attributes {name: 'some name', price: 2, tasty: true}
  end

end
```


- [Active Record Validations Docs](http://guides.rubyonrails.org/active_record_validations.html)
- [Displaying Validations in Views Rails Docs](http://guides.rubyonrails.org/active_record_validations.html#displaying-validation-errors-in-views)

# <a id="sessions">Rails Sessions and Cookies</a>

## SWBATs

* Describe the stateless nature of HTTP
* Explain that cookies are a way to store data on browsers
  * Cookies are key-value pairs with some extra info
* Practice adding and removing information from the session
* Practice adding and removing information from the session using flash

## Resources

* [Example Video](https://www.youtube.com/watch?v=q9_f6NtuCWk&feature=youtu.be)
* [Starter Code](https://github.com/learn-co-curriculum/lectures-starter-code/tree/master/rails/sessions-cookies-beta)

## Outline

```text
 10m Intro to Problem: How can our game remember a users score?
 7m The Rails session method makes this easier
 15m The Rails session is built using cookies
 15m Implementing our Deliverables
 3m Conclusion
===
50m Total
```

### How can our game remember a users score?
I like to use an actual project to make illustrate the challenge posed by stateless http and make the problem less hypothetical:
We start with an app, which presents the user with questions in succession. Each time they submit a response we can store it in the database, but we want a way for the game to keep track of that specific users responses from question to question...
Students start to realize the difference between "session" type data and the "state-like" data they have been working with so far.
Go further to demonstrate how hard it would be to keep track of a users responses without a session:

* We could make a user create an account and login, then redirect them to a route with the user_id as a parameter in the URL
    * Our path helpers would stop working and we would have to define custom routes for all of our routing
* We could use the request.remote_ip to differentiate this users responses from other users responses
    * The IP can be spoofed, our database would be overworked

Draw out the client-server request cycle on the whiteboard to illustrate the statelessness of http- data is either in the request or the response and will not inherently persist from one to the other. The diagram can be used later to demonstrate how cookies work.

### The Rails session method makes this easier
In the responses#create method, initialize a number_correct variable in the session: 
```ruby
...
    def create
        session[:number_correct] ||= 0
        response = Response.create(response_params)
        if response.question.correct_answer == response.answer
            @number_correct = @number_correct + 1
            puts "Correct"
        else
            puts "Incorrect"
        end
        puts "Answered Correctly: #{session[:number_correct]}"
        redirect_to '/random-question'
    end
...

```
Answer several questions correctly and watch the value increase in the rails s output. This demonstrates how the value persists and is incremented from request to request. 

Hopefully students will now:
* Understand what the session method provides for us
* Understand why the session method is useful
* **Be curious** as to how the session accomplishes this functionality

### Rails session is built using cookies
This is where we transition into explaining how the session works as apposed to what it does.
* Explain what cookies are, show (using your diagram) how the server sends information in its first response to initialize cookies, and how the client will include those cookies in the following requests.
* Look at cookies in the Chrome Console, demonstrate how they can be manipulated by the client are therefore unsafe. Delete your cookies and show how it resets your `:number_correct` counter.
* I like to use this opportunity to discuss dates, by examining why some cookies have an expiration date of December 31, 1969 11:59:59 (its the epoch less one second)
* Explain how we can protect the data by using an identifier in the cookie to find data stored remotely on the server, either in a file or in memory or in the database.

### Implementing our Deliverables
* Use a helper method to expose the session variable `:number_correct` as an instance variable:
```ruby
    ...
    before_action :define_question, :define_response, :define_number_correct
    ...
    def  define_number_correct
        @number_correct = session[:number_correct]
    end
    ...
```
* Use the `@number_correct` instance variable in your view to display the number of correct answers to the user
    * The view is in views -> responses -> new.html.erb

* Now try to implement our second deliverable; a message to the user to tell them whether or not they got the last question right:
* Add a `:message` variable to the session:
```ruby
    ...
    before_action :define_question, :define_response, :define_number_correct, :define_message
    ...
    def create
        session[:number_correct] ||= 0
        response = Response.create(response_params)
        if response.question.correct_answer == response.answer
            session[:number_correct] = session[:number_correct] + 1
            session[:message] = 'Correct! Great job!'
        else
            session[:message] = 'Sorry, that was incorrect. Hang in there.'
        end
        redirect_to '/random-question'
    end
    ...
    def  define_message
        @message = session[:message]
    end
```
* Render the `@message` variable in the view near the top of the page.
* Demonstrate how this works
* Demonstrate how the message sticks even if we refresh the page, or navigate away and come back to the page. Discuss how this could be hella confusing to the user.
* Explain how we often need data which persists for only one request response cycle, and introduce the flash as a rails' method designed to help us by cleaning up after itself after one such cycle. Refactor the `:message` variable into the flash instead of the session:
```ruby
    ...
    before_action :define_question, :define_response, :define_number_correct, :define_message
    ...
    def create
        session[:number_correct] ||= 0
        response = Response.create(response_params)
        if response.question.correct_answer == response.answer
            session[:number_correct] = session[:number_correct] + 1
            flash[:message] = 'Correct! Great job!'
        else
            flash[:message] = 'Sorry, that was incorrect. Hang in there.'
        end
        redirect_to '/random-question'
    end
    ...
    def  define_message
        @message = flash[:message]
    end
```
* Answer another question, then demonstrate how the message is cleared if we refresh the page.

### Conclusion
Conclude by admitting that the app is incomplete and would ideally allow a user to create an account so that their responses could be accessed at a later time, and use this as an opportunity to foreshadow the next days lecture on authentication and authorization.

---
title: Rails Auth
layout: post
---

# <a id="authentication">Auth in Rails</a>

## Objectives
- Understand, theoretically, how authentication and authorization work
- Discuss different encryption and hashing schemes, and `bcrypt` specifically
- Augment a user model in rails using `bcrypt` and `password_digest`
- Expose this information in a sample rails app
- Go over sessions, cookies, and implement sign up, log in, and log out


## Preparation
Generally, this is the last Rails lecture. Students may have already taken the coding challenge before learning about Auth.

Have some kind of application set up that could use some user interaction.

## Steps

### How does auth work in theory? (25 minutes)
Answer the following questions together:
##### What is the difference between sign-in and sign up?

Sign-up happens once, and afterwards the information that is used to authenticate a user exists in the system for sign-in.

##### What is authentication?

It boils down to a really interesting question: _Are you who you say you are?_ And we use the username/password as a proxy for that.

##### What is the difference between Authentication and Authorization?

Authorization happens after authentication. It's about scope, and specific information. _What is the user allowed to see/interact with?_

##### How do passwords work?

Do websites save our passwords? And if they do, how are they stored? Talk about encryption, and why hashed passwords are encrypted. We don't want malicious employees or hackers to see our passwords.

##### What is the difference between hashing and encrypting?

What is encryption? What can be encrypted? Anything that can be encrypted, must also be able to be decrypted. You can use this time to talk about ciphers, and show how at it's core, encryption and hashing is about these principles. In order to decrypt a cypher, you need to know the cypher used and any parameters (offset, perhaps) used to encrypt the information.

Hashing is a little different: the ultimate goal of one-way hashing is that you cannot "decrypt" the original text. In addition to any encryption scheme, each authenticated user has a "salt", added information that augments the password to make decryption even harder.  

Give an example of various text going through some kind of hashing scheme with salts, so that the students can see this in action. Be sure your example shows that the server is actually validating the equality of the _hashed password_ with the hashed input.

### Using `bcrypt` to create passwords in Rails (10 minutes)
What's cool about `bcrypt`? By design, it's slow. This means that anyone who wants to crack it has to take a long time to brute-force passwords. It also allows you to define a column called `password_digest` and it will do the rest of the work.

_Remember, convention over configuration._ And especially in this case, we generally don't have the time or energy to build our own encryption that surpasses what already exists.

After installing the `bcrypt` gem, you can use a macro in your user model called `has_secure_password`, which does a lot of the integration for you. Go in and test this in the console. You can show how the `user` model ends up with a `password_digest` attribute even though you send in `password` through the `create`. Do it again, this time with a `password_confirmation` in the initialization hash. You can show how rails rejects the transaction.

Now that you've created a user with a password, you can do `user.authenticate("password")`.

### Exposing user authentication in the UI (20 minutes)
_These steps don't have to happen all in one order. Play with whatever flow works best for you._

You can set up routes to work with users in the app.
```ruby
resources :users, only: [:new, :create, :show]
```

Now you can build a `form_for` for the `new` action:

```erb
<%= form_for @user do |f| %>
  <%= f.label :username %>
  <%= f.text_field :username %>
  <%= f.label :password %>
  <%= f.text_field :password %>
  <%= f.label :password_confirmation %>
  <%= f.text_field :password_confirmation %>
  <%= f.submit %>
<% end %>
```

Go through making the `create` controller:

```ruby
@user = User.new(user_params)
if @user.valid?
  @user.save
  redirect_to @user
else
  redirect_to new_user_path
end
```

Our form doesn't hide the password in the `input`, so change the text field to `f.password_field`.

So, to recap the necessary steps:
1. `password_digest` as an attribute in our `users` table
2. `bcrypt` installed in `Gemfile`
3. `has_secure_password` in the `User` model

_If it comes up, talk about `devise` and why it's more valuable to learn auth by doing it with vanilla `bcrypt`._

### Sessions and cookies (25 minutes)
How does an application keep you logged in between requests? Remember, requests are stateless, so sessions allow us to provide a user a sense of continuity as the interact with the website.  

How do cookies fit into this? Talk briefly about how they're made, how the application creates, accesses and maintains them. Show what cookies are, in chrome. Ultimately, they're just key-value pairs. Make it clear that each website has it's own cookies, and that cookies aren't secure, because they're not necessarily encrypted.

What information do we want to store in the cookie?

Sessions aren't really stored in the database, so we don't use a model for them. However, they still need routes, a controller and views.

`routes.rb `
```ruby
get "signup", to: "users#new", as: "signup"
get "login", to: "sessions#new", as: "login"
post "sessions", to: "sessions#create", as: "sessions"
```

`sessions_controller.rb`
```ruby
def new
  # don't need anything in here, cause we're not setting up a
  # blank model to couple with the form
end

def create
  # no strong params cause there is no mass assignment
  user = User.find_by(username: params[:username])
  if @user && @user.authenticate(params[:password])
    redirect_to @user
  else
    redirect_to login_path
  end
end
```
Use this time to talk about how in certain cases, it's more secure to offer _less_ feedback to the user. This is why we both authenticate on the existence of the username, and the password match. Still, it's helpful to use `flash[:error]` here.

`sessions/new.html.erb`

Use a `form_tag` instead of a `form_for` here, we don't have a model to couple the form with.

_All forms need an action and a method, and here the action is `/sessions`, but that may not be intuitive to the students, so call it out explicitly._
```erb
<%= form_tag sessions_path do %>
  <%= label_tag "Username" %>
  <%= text_field_tag :username %>
  <%= label_tag "Password" %>
  <%= password_field_tag :password %>
  <%= submit_tag "Sign In" %>
<% end %>
```

#### Authorization and User-specific content (25 minutes)

Have some model such that the user `has_many`. Given this association, we can show the user their specific objects (in this example, `song`) on their own page.

Augment `sessions_controller#create` with the following line after a successful authentication:
```ruby
session[:user_id] = @user.id
```
This allows us to save the user_id in the session cookie. `session` persists across the entire usage of the application, and `flash` works just between 2 requests. Show that this new code adds the cookie in browser as well.

Here are the steps that we can use to get our user's songs through the session:
1. Get the sessions by user_id
2. Get the user by user_id
3. get the songs by user

In `SongsController#index`:
```ruby
if session[:user_id]
  @user = User.find(session[:user_id])
  @songs = @user.songs
else
  @songs = Song.all # or force a login
end
```
Show how this works and filter's the song by user (when logged in). However, you don't want to do this work over and over again. Where can you do this? `ApplicationController`!

`application_controller.rb`

```ruby
def current_user
  if session[:user_id]
    @user = User.find_by(id: session[:user_id])
  else
  end
end

def logged_in?
  !!current_user
end
```

Now, you can refactor `SongsController#index`
```ruby
if logged_in?
  @songs = current_user.songs
else
  @songs = Song.all # or force a login
end
```
This is still not perfect. We want to be able to redirect to the login page if the user isn't logged in yet.

Add the following to `ApplicationController`:
```ruby
def authorized
  redirect_to login_path unless logged_in?
end
```

Now, in each controller/action that needs to do this redirect, you can add:
```ruby
before_action :authorized
```
Make sure not to use this for the login path. Instead, you should use:
```ruby
skip_before_action :authorized, only: [:new, :create] # or whatever onlys you need
```

#### Logging out (10 minutes)

So how do you log out? By destroying the session.

`routes.rb`
```ruby
delete "sessions", to: "sessions#destroy"
```

`sessions_controller.rb`
```ruby
def destroy
  session.delete(:user_id) # or session[:user_id] = nil
end
```
To expose this, talk about a button that shows a "Log Out" button if logged in, and a "Log In" button otherwise.

The best place to do this is in `application.html.erb`, but to expose our controller's method here, we must use the `helper_method :logged_in?` macro in our `ApplicationController`

Finally, in `application.html.erb`:

```erb
<% if logged_in? %>
  <%= link_to "Logout", sessions_path, method: :delete %>
<% else %>
  <%= link_to "Login", login_path %>
<% end %>
```

#### Conclusion (5 minutes)
This is just the tip of the iceberg. Encourage students to do their own research on cookies, sessions, encryption, hashing, and all the stuff we've gone over. There are so many levels to security.

## Resources
None because Johann is a legend.


---
title: React Jwt Auth 1
layout: post
---

# <a id="jwt1">React JWT Auth 1</a>

The aim of this lecture is to introduce the students to a basic setup for authorization. This lecture should draw on their familiarty with previously taught auth concepts such as:

1. POSTing login/signup data
2. BCrypt for authenticating passwords
3. Cookies to store user data in browser

The modular pattern used to manage API calls is useful but not essential to their understanding of the following concepts.

## SWBATs

* Explain the difference between Authentication vs. Authorization
* Authenticate via a basic controller action in Rails triggered by a `fetch` in React
* Store user data in state on login/signup
* Implement `localStorage` to store identifying information about a user in the browser (just a user ID for now)
* Automatically fetch user information based on contents of `localStorage` for already logged-in users


## Resources

* [Example Video](https://www.youtube.com/watch?v=KvVDXV9LQXc)
* [Starter Code]()

## Outline

     5m The Authentication Problem
    10m Recap and Setup
    30m Basic Auth Code in Action
    15m Introducing Local Storage
    ===
    60m Total

### The Authentication Problem
The HTTP protocol is _stateless_. This means the server does not remember anything about a client between requests. So if we authenticate a user with a username and password, then on the next request, our application won't remember us.

The _old way_ of dealing with this was to store who was logged in on the server. Every time the server received a request from a client, it would check to see if that client was logged in or not. This is not very efficient:

1. Every time a user logs in, the server has to create a record somewhere on the server. If lots of users are logging in, the overhead on our server increases.

2. If the logged-in information is stored in local memory on a server, the user will only be able to make requests to that server. This is not ideal - what if we have a bunch of servers, but most of the users are forced into using the original server they logged in at?

There are a few other problems, but these two are the main ones.

### Recap and Setup

Start by going over the existing Auth information that the students already might know. Confirm that Authentication is "are you who you say you are?" and Authorization is "what does this user have access to". So, how did this used to work? Recap sessions being stored as cookies, such that browsers could remember each app's logged-in users.

Now, discuss that cookies are domain-specific, but in a Rails-backed React app, we no longer use just one domain, we have two. So what is our alternate strategy?

Whenever you add a new feature to your app, ask the following questions:

* Does my schema need to change? To figure out what data structure you need to make everything work.
* What routes do I need? Because without these there are no entry-points into your app.

Adding auth means that you'll need to introduce a "User" model to your application, and a series of auth-related routes.

### Basic Auth Code in Action

Creating a new user is just a CRUD action, so feel free to do this in the console. Ensure the `has_secure_password` macro in Rails sets up the `password_digest` in the User model.

Once you have a user, you can fill out a login form, and fetch to an `AuthController` in Rails, something like `api.auth.login(username, password)`.

```js
const login = (username, password) => {
  return fetch(`${API_ROOT}/auth/`, {
    method: 'POST',
    headers: headers,
    body: JSON.stringify({ username, password });
  }).then(res => res.json());
}
```

You can set up your routes to look something like this:

```ruby
namespace :api do
  namespace :v1 do
    resources :something
    post '/auth', to 'auth#create'
  end
end
```

Once you confirm that that wiring happens, you can add the authentication code in your action:

```ruby
user = User.find_by(username: params[:username])
if user && user.authenticate(params[:password])
  render json: { id: user.id, username: user.username }
else
  render json: { error: "User is invalid" }, status: 401
end
```

_Note that we're not sending back the entire user, because that would include the password digest and perhaps some other unnecessary metadata. Also, the 401 status means "Not Authenticated"._

Show that you can see the status code returned from the server by going to the network tab.

Now we can change our Login callback:

```js
handleSubmit = e => {
  e.preventDefault();
  api.auth
    .login(this.state.fields.username, this.state.fields.password)
    .then(res => {
      if (res.error) {
        this.setState({ error: true });
      } else {
        //res is our user hash
        this.setState({
          currentUser: res
        });
      }
    });
};
```

Note that we need to set up our `currentUser` state at a top level so that it can be accessed everywhere, meaning it must go to the App.

```js
class App extends React.Component {
  state = { auth: { currentUser: {} } };

  handleLogin = user => {
    const currentUser = { currentUser: user };
    this.setState({ auth: currentUser });
  };
}
```

Now you can update all of your components such that a logged-in user is reflected in them. (The easiest one is a Navbar that might have a "Login" button).

Next, we want to be able to pass all of our state about the logged-in user around, and we can do this using router's history:

```jsx
<Route
  path="/login"
  render={routerProps => {
    return (
      <Login history={routerProps.history} handleSuccess={this.handleLogin} />
    );
  }}
/>
```

And our handle submit's success can have:

```js
this.props.handleSuccess(res);
this.props.history.push('/');
```

to redirect us home.

You can now use much of the same code to add signup. The signup form is very similiar to the login form, except that you might ask for a password confirmation in addition to username an password. The `user#create` controller action should very much resemble the `auth#create` action, the only difference being that a user is _created_ based upon username and password, rather than just being _found_ and _authenticated_. 


### Introducing Local Storage

How do we maintain logged-in state across requests/refreshes? `localStorage`! Explain that this is just a key-value store, like an object. When a user logs in, add:

```js
localStorage.setItem('token', user.id);
```

_Note: you can discuss the difference between localStorage and sessionStorage, and that sessionStorage lasts for less time._

And then on `componentDidMount`, check for this token and authenticate and set the current user if it exists. Make sure your logout deletes this token as well!

```ruby
# /routes.rb
get '/current_user', to: 'auth#show'
```

```ruby
# /AuthController.rb

def show
  token = request.headers['Authorization']  
  user = User.find_by(id: token)
  if user
    render json: { id: user.id, username: user.username }
  else
    render json: { error: "Invalid Token" }, status: 401
  end
end
```


```js
// /services/api.js

const token = localStorage.getItem('token');
const headers = {
  'Content-Type': 'application/json',
  Accepts: 'application/json',
  Authorization: token
};

const getCurrentUser = () => {
  return fetch(`${API_ROOT}/current_user`, {
    headers: headers
  }).then(res => res.json());
};
```


```js
// /App.js

componentDidMount() {
  const token = localStorage.getItem('token');
  if (token) {
    api.auth.getCurrentUser().then(user => {
      this.setState({ auth: { currentUser: user } })
    })
  }
}
```

Why is our current implementation of `token` not great? You can easily set the token if you know the User's id.

If time allows, `handleLogout` can be written that:
1. Resets `currentUser` to an empty object or `null`
2. Removes `token` from `localStorage`
3. Redirects to `/login`

---
title: React Jwt Auth 2
layout: post
---

# <a id="jwt2">React JWT Auth 2</a>

The code from the previous lecture (React JWT Auth 1) should suffice as starter code. You should have:

1. Login and signup forms in React
2. Login and signup routes in Rails
3. React state that holds `currentUser`
4. `localStorage` setup to accept a token (only holds a user ID under a key of `token`)
5. `componentDidMount` in `App.js` that automatically fetches to an `/auth/show` route if a key of `token` is in your `localStorage`
6. HTTP Requests with authorization headers

## SWBATs

* Generate JWTs on user signup/login
* Store JWTs in `localStorage`
* Setup a pipeline to obtain the current user whenever a valid JWT is included in an authorization header
* Authorize and protect routes

## Resources

* [Example Video]()
* [Starter Code]()

## Outline

```
  10m | JWT Basics and Flow
  15m | Encoding and Decoding JWTs
  15m | Integrating JWT into Auth Flow
  20m | Authorization
  ===
  60m | Total
```

### JWT Basics and Flow

* Token-based authentication is stateless. We are not storing any information about a logged in user on the server. No stored information means your applicaiton can scale and add more machines as necessary without worrying about where a user is logged in.

* Here is the JWT authentication flow:
  1. User requests access with username and password
  2. The app validates the credentials
  3. The app gives a signed token to the client
  4. The client stores the token and presents it with every request 

* JWTs are composed of three strings separated by periods:

  ```
  aaaaaaaaaaaaaaa.bbbbbbbbbbbbbbbbbbbbb.ccccccccccccccccccc
  ```

  * The first part (aaaaaaaaaaaa) is the header

  * The second part (bbbbbbbbbbbb) is the payload - the good stuff, like who this person is, and their id in our database.

  * The third part (ccccccccccccc) is the signature. The signature is a hash of the header and the payload. It is hashed with a secret key, that we will provide.

  * Head on over to [jwt.io](http://jwt.io/#debugger) and see what I mean:

  <img width="750" alt="JWTs" src="https://cloud.githubusercontent.com/assets/25366/9151601/2e3baf1a-3dbc-11e5-90f6-b22cda07a077.png">

### Encoding and Decoding JWTs

* Add `gem 'jwt'` inside your Gemfile
* Functionality can be shown in the Rails console
  * `JWT.encode` takes up to three arguments: a payload to encode, an application secret of the user's choice, and an optional third that can be used to specify the hashing algorithm used. Typically, we don't need to show the third. Returns a JWT as a string
  * `JWT.decode` takes three arguments as well: a JWT as a string, an applicatin secret, and optionally a hashing algorithm.
  
    ```ruby
    #in console
    > payload = {beef: 'steak'}
    > jwt = JWT.encode(payload, 'boeuf')
    > decoded_hash = JWT.decode(jwt, 'boeuf')
    > data = decoded_hash[0]
    ```
  
  * Useful to show: decoding an invalid JWT, decoding using an application secret that doesn't match the one provided during encoding, and that `decoded_hash` is an array with the encoded data being store at index 0
  * Good to ask what data the class thinks will be encoded. Bring them back to the idea that storing a user's ID in `localStorage` might not be a good idea, and that we will be replacing the value of `token` in `localStorage` to an encoded JWT that contains the payload `{user_id: <ID>}` . Decoding will allow our application and only our application access to this payload. 

* Build into functions in `application_controller.rb`
  * Good to ask the class to explain why we're choosing `application_controller.rb`
  
    ```ruby
    class ApplicationController < ActionController::API
      def issue_token(payload)
        JWT.encode(payload, "supersecretcode")
      end
      
      def decode_token(token)
        JWT.decode(token, "supersecretcode")[0]
      end
    end
    ```

### Integrating JWT into Auth Flow

* A token should be issued in two different controller actions: `auth#create` and `users#create`. We simply call our `issue_token` method, passing the found/created user's ID in a payload. The newly created JWT can then be passed back along with the user's data. The user data can be stored in state while the token can be stored in `localStorage`.

  ```ruby
  # auth_controller.rb
  def create
    user = User.find_by(username: params[:username])
    if user && user.authenticate(params[:password])
      payload = {user_id: user.id}
      token = issue_token(payload)
      render json: { jwt: token, yay: true }
    else
      render json: { error: "You dun goofed!"}
    end
  end
  
  # users_controller.rb
  def create

    user = User.new(username: params[:username], password: params[:password])
    if user.save
      payload = {user_id: user.id}
      token = issue_token(payload)
      render json: { jwt: token, yay: true }
    else
      render json: { error: "You dun goofed!"}
    end
  end
  
  
  ```

* In the previous build, the token (which only held the user's ID) was received by the backend via a request header. This will not change, and can be integrated into our growing pipeline

  ```ruby
  class ApplicationController < ActionController::API
    def issue_token(payload)
      JWT.encode(payload, "supersecretcode")
    end
    
    def decode_token
      JWT.decode(get_token, "supersecretcode")[0]
    end
    
    def get_token
      request.headers["Authorization"]
    end
  end
  ```
  
* We can then complete our pipeline by automatically obtaining the user whenever an authorization header is present

  ```ruby
  class ApplicationController < ActionController::API
    def issue_token(payload)
      JWT.encode(payload, "supersecretcode")
    end
    
    def decode_token
      JWT.decode(get_token, "supersecretcode")[0]
    end
    
    def get_token
      request.headers["Authorization"]
    end
    
    def current_user
      User.find(decode_token["user_id"])
    end
    
    def logged_in
      !!current_user
    end
  end
  ```
  
  Error handling can be added to the above code to make it more robust.
  
* With the above pieces in place, we can simplify our `auth#show` to the following, which will work, but _only_ if we pass an authorization header along with our GET request

  ```ruby
  # auth_controller.rb
  
  def show
    if logged_in
      render json: current_user
    else 
      render json: {error: "You dun goofed!"}
    end
  end
  ```
  
### Authorization

* Authorization is primarily used to obtain information related only to the user that's currently logged in (e.g. user dashboards or feeds), to limit a user's access to parts of an application, and of course to prevent unauthenticaed users from accessing parts of application that should be accessible to only users who are logged in

* Authorizing inside the component

  ```jsx
    class MyComponent extends React.Component {
    
      state = {
        loading: true
      }
      
      componentDidMount () {      
        if (!localStorage.getItem('jwt')) {
          this.props.history.push('/login')
        } else if(this.props.loggedIn) {
          this.setState({loading: false})
        }
      }
      
      componentWillReceiveProps (nextProps) {
        if (!localStorage.getItem('jwt')) {
          nextProps.history.push('/login')
        } else if(this.props.loggedIn || nextProps.loggedIn) {
          this.setState({loading: false})
        }
      }
      
      render(){
        if (this.state.loading) {
          return <div>I'M LOADING</div>
        } else {
          return <div>I'M THE TARGET CONTENT</div>
        }
      }
    }
  ```
  
* This code is not very DRY and would have to be written everywhere we want authorization, so instead, we can write a HOC to wrap around any components we want authorized.

  ```
  import React from 'react' 
  
  export default function (RenderedComponent) {
    return class extends React.Component {
    
      state = {
        loading: true
      }
      
      componentDidMount () {      
        if (!localStorage.getItem('jwt')) {
          this.props.history.push('/login')
        } else if(this.props.loggedIn) {
          this.setState({loading: false})
        }
      }
      
      componentWillReceiveProps (nextProps) {
        if (!localStorage.getItem('jwt')) {
          nextProps.history.push('/login')
        } else if(this.props.loggedIn || nextProps.loggedIn) {
          this.setState({loading: false})
        }
      }
      
      render(){
        if (this.state.loading) {
          return <div>I'M LOADING</div>
        } else {
          return <RenderedComponent {...this.props}/>       }
      }
    }
  }
  ```
  
* Another important feature of auth is the ability to grab the details of whichever user is logged in using our `current_user` method. Rather than having to include a body to our request, we simply include an authorization header

  ```js
  fetch(RAILS_API_URL + "/my_posts", {
    method: "GET",
    headers: {
      "Authorization": localStorage.getItem("token")
    }
  })
  ```

  ```ruby
  # posts_controller.rb
  
  def my_posts
    if logged_in
      render json: current_user.posts
    else 
      render json: {error: "You dun goofed!"}
    end
  end
  ```

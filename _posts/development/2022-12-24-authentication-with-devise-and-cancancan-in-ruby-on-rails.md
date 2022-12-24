---
layout: post
title:  Authentication with Devise and cancancan in Rails
date:   2022-12-24 02:00:00 -0700
categories: [Development]
path: "development"
tags: ["Ruby on Rails"]
math: true
mermaid: true
# image:
#   path: /assets/img/posts/2022/rails-7-bootstrap-jquery-importmap.jpg
#   width: 800
#   height: 500
#   alt: How to use an array field in a database table in Ruby on Rails
---

To use the cancancan gem with devise in a Ruby on Rails app, you will need to do the following:

#### First, you need to add the cancancan gem to your Gemfile and run ```bundle install```.

#### Then create a Ability model by running the following command:

```terminal
rails g cancan:ability
```
This will create a new file at app/models/ability.rb that contains the Ability class.

#### In the Ability class, define the permissions for different user roles. For example:

```ruby
class Ability
  include CanCan::Ability

  def initialize(user)
    if user.admin?
      can :manage, :all
    else
      can :read, :all
    end
  end
end
```

#### In your controllers, use the load_and_authorize_resource method to load and authorize the resource. For example:
```ruby
class PostsController < ApplicationController
  load_and_authorize_resource

  def show
    # The @post instance variable has already been loaded and authorized
  end
end
```

#### In your views, use the can? method to show or hide content based on the user's permissions. For example:
```erb
<% if can? :update, @post %>
  <%= link_to 'Edit', edit_post_path(@post) %>
<% end %>
```

I hope this helps! Let me know if you have any questions.

<br />
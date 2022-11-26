---
layout: post
title:  "Using Action Text in Rails 6"
date:   2022-01-14 15:33:05 -0700
categories: [Development]
path: "development"
tags: ["Ruby on Rails"]
---
In order to have Action Text in your application you have to follow a few steps. We need to install Active Storage and then Action Text.

#### Install Action Text
```sh
# Terminal: Development
rails action_text:install
```

#### Import style and javascript
```js
// application.js
require("trix")
require("@rails/actiontext")
```

```scss
// application.scss
@import "trix/dist/trix";
@import "./actiontext.scss";
```
Now we can attach it to a model, render a rich_text_area in our form, then render the content and we're done
```ruby
# post.rb
class Post < ApplicationRecord
  has_rich_text :content
end
```

```ruby
# _form.html.erb
<%= form_with model: post do |form| %>
  <%= form.label :content %>
  <%= form.rich_text_area :content %>
<% end %>
```

```ruby
# show.html.erb
<%= @post.content %>
```
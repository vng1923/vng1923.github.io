---
layout: post
title:  "Set page titles and meta tags in Rails views"
date:   2022-01-13 19:33:05 -0700
categories: [Development]
path: "development"
tags: ["Ruby on Rails"]
---
Title and Meta tags are types of HTML tags that provide search engines with information about a webpage (metadata). It is not displayed on the page itself. Search engines use this metadata to understand additional information about the webpage for crawling and indexing.

So, we often need to customize the page title and meta tags for individual views. I'm doing it by add helper methods to use in the views to override the default.

First, add these methods to `application_helper.rb`

```ruby
module ApplicationHelper
  def title(text)
    content_for :title, text
  end

  def meta_tag(tag, text)
    content_for :"meta_#{tag}", text
  end

  def yield_meta_tag(tag, default_text="")
    content_for?(:"meta_#{tag}") ? content_for(:"meta_#{tag}") : default_text
  end
end
```

Next, change the title tag in `app/views/layouts/application.html.erb` to look something like this:
```ruby
<title>
  <%= if content_for?(:title) then yield(:title) + ' | ' end %>
  BenNguyen's Blog
</title>
<meta name='keywords' content='<%= yield_meta_tag(:keywords, 'blog, development, software, engineer') %>' />
<meta name='description' content='<%= yield_meta_tag(:description, 'blog, development, software, engineer, ruby on rails') %>' />
```

Now just set title and meta tags for each view like this:
```ruby
<% title @post.title %>
<% meta_tag :description, @post.description %>
<% meta_tag :keywords, @post.keywords.join(',') %>
```
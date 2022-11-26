---
layout: post
title:  "Use gem 'meta-tags' in Rails app to improve Search Engine Optimization (SEO)"
date:   2022-01-20 07:22:05 -0700
categories: [Development]
path: "development"
tags: ["Ruby on Rails"]
---


### [MetaTags](https://github.com/kpumuk/meta-tags){:target="_blank"}: a gem to make your Rails application SEO-friendly

#### First, add meta-tags to your Gemfile
```ruby
gem 'meta-tags'
```
And run ```bundle install```

#### Then, add this code to your layout (application.html.erb)
```erb
<head>
  <%= display_meta_tags site: 'Ben Blog' %>
</head>
```

#### Now, just need to add this to each views
```erb
<h1><%= title 'Use gem meta-tags in Rails app to improve Search Engine Optimization (SEO)' %></h1>
```

#### When views are rendered, the page title will be included in the right spots:
```html
<head>
  <title>Ben Blog | Use gem meta-tags in Rails app to improve Search Engine Optimization (SEO)</title>
</head>
<body>
  <h1>Use gem meta-tags in Rails app to improve Search Engine Optimization (SEO)</h1>
</body>
```

#### Using MetaTags in View
```erb
<% title 'Use gem meta-tags in Rails app to improve Search Engine Optimization (SEO)' %>
<% description 'a gem to make your Rails application SEO-friendly' %>
<% keywords 'Rails, SEO' %>
```
#### Or use set_meta_tags method instead
```erb
<% set_meta_tags  title: 'Use gem meta-tags in Rails app to improve Search Engine Optimization (SEO)',
                  description: 'a gem to make your Rails application SEO-friendly',
                  keywords: 'Rails, SEO' %>
```
#### We can set default value in ```application_helper.rb```
```ruby
def default_meta_tags
  {
    title:       'Ben Blog',
    description: 'This is my blog about programming and my hobbies.',
    keywords:    'blog, development, software, engineer, ruby on rails',
    separator:   "&mdash;".html_safe,
    og: {
      site_name: 'Ben Blog',
      title: 'Ben Blog',
      description: 'This is my blog about programming and my hobbies.', 
      type: 'website',
      url: request.original_url,
      image: image_url('ben-blog-social.jpg')
    }
  }
end
```
And then can use it in layout:
```erb
<%= display_meta_tags(default_meta_tags) %>
```

This is my thought about using [meta-tags](https://github.com/kpumuk/meta-tags){:target="_blank"} gem. 

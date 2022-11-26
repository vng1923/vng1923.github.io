---
layout: post
title:  "How to instantiate class from string in Rails?"
date:   2022-03-01 09:15:05 -0700
categories: [Development]
path: "development"
tags: ["Ruby on Rails"]
---

### How to instantiate class from string in Rails?

```ruby
result_object = Object.const_get "ClassName"
```

Below is an example how to instantiate class and call methods

```ruby
# ukraine.rb
class Ukraine
  def say
    puts "Stop Putin! Stop War in Ukraine!!!"
  end
end
```

```sh
# Terminal: Development
irb(main):001:0> ukraine = Object.const_get "Ukraine"
irb(main):001:0> ukraine.say
--> Stop Putin! Stop War in Ukraine!!!
```
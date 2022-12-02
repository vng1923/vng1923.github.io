---
layout: post
title:  "How to add tags to jekyll post on Github Pages"
date:   2022-04-29 22:15:05 -0700
categories: [Development]
path: "development"
tags: ["Ruby on Rails", "jekyll", "github"]
---
In this post, I will show you the way I'm using to add tags to jekyll post on Github Pages

### Add tags to posts
In each post, you need to add tags to the header. Below is an example:
```markdown
---
layout: post
title:  "How to add tags to jekyll post on Github Pages"
date:   2022-04-29 22:15:05 -0700
categories: development
path: "development"
tags: ["Ruby on Rails", "jekyll", "github"]
---
```

### Create layout for tags
Create new file ```tag.html``` in ```_layouts``` folder with the content below:
```html
---
layout: default
---
<article class="post">

  <header class="post-header">
    <h1 class="post-title">{% raw %}{{ page.title | escape }}{% endraw %}</h1>
  </header>

  <div class="post-content">
    {% raw %}{{ content }}{% endraw %}
  </div>

</article>
```

### Create page for tags
Create folder ```tags```. All tag page will save here
Each tag have a different page. For example with ```tag: jekyll``` we have a file named ```jekyll.markdown``` in folder ```tags``` with the content below:
```markdown
---
layout: tag
title: "Tag: jekyll"
tags: ["jekyll"]
permalink: /t/jekyll
---

<ul class="post-list">
  {% raw %}{%- for post in site.tags['jekyll'] -%}{% endraw %}
  <li>
    {% raw %}{%- assign date_format = site.minima.date_format | default: "%b %-d, %Y" -%}{% endraw %}
    <span class="post-meta">{% raw %}{{ post.date | date: date_format }}{% endraw %}</span>
    <h3>
      <a class="post-link" href="{{ post.url | relative_url }}">
        {% raw %}{{ post.title | escape }}{% endraw %}
      </a>
    </h3>
    {% raw %}{%- if site.show_excerpts -%}
      {{ post.excerpt }}
    {%- endif -%}{% endraw %}
  </li>
  {% raw %}{%- endfor -%}{% endraw %}
</ul>
```

### Edit homepage or any page you want to show tags
Add this code to the loop of posts
```markdown
{% raw %}{%- for tag in post.tags -%}{% endraw %}
  <a href="/t/{{ tag | downcase | replace: ' ', '-' }}">{% raw %}#{{ tag }}{% endraw %}</a> &nbsp;
{% raw %}{%- endfor -%}{% endraw %}
```
Here is an example of my homepage:
```markdown
---
layout: default
---

<div class="home">
  {% raw %}{%- if page.title -%}{% endraw %}
    <h1 class="page-heading">{% raw %}{{ page.title }}{% endraw %}</h1>
  {% raw %}{%- endif -%}{% endraw %}

  {% raw %}{{ content }}{% endraw %}
  {% raw %}{%- if site.categories['development'].size > 0 -%}{% endraw %}
    <h2 class="post-list-heading">{% raw %}{{ page.list_title | default: "Posts" }}{% endraw %}</h2>
    <ul class="post-list">
      {% raw %}{%- for post in site.categories['development'] -%}{% endraw %}
      <li>
        {% raw %}{%- assign date_format = site.minima.date_format | default: "%b %-d, %Y" -%}{% endraw %}
        <span class="post-meta">{% raw %}{{ post.date | date: date_format }}{% endraw %}</span>
        <span class="post-meta" style="padding-left: 20px;">
          {% raw %}{%- for tag in post.tags -%}{% endraw %}
            <a href="/t/{{ tag | downcase | replace: ' ', '-' }}">{% raw %}#{{ tag }}{% endraw %}</a> &nbsp;
          {% raw %}{%- endfor -%}{% endraw %}
        </span>
        <h3>
          <a class="post-link" href="{{ post.url | relative_url }}">
            {% raw %}{{ post.title | escape }}{% endraw %}
          </a>
        </h3>
        {% raw %}{%- if site.show_excerpts -%}
          {{ post.excerpt }}
        {%- endif -%}{% endraw %}
      </li>
      {% raw %}{%- endfor -%}{% endraw %}
    </ul>
    <p class="rss-subscribe">subscribe <a href="{{ "/feed.xml" | relative_url }}">via RSS</a></p>
  {% raw %}{%- endif -%}{% endraw %}
</div>
```

### Edit post template to show tags in each post
Add this code to ```post.html``` in ```_layouts``` folder
```html
<div class="row">
  <div class="col-12">
    Tags: 
  {% raw %}{% for tag in page.tags %}{% endraw %}
    <a class="post" href="/t/{{ tag | downcase | replace: ' ', '-' }}">{% raw %}#{{ tag }}{% endraw %}</a>{% raw %}{% unless forloop.last %}, {% endunless %}{% endraw %}
  {% raw %}{% endfor %}{% endraw %}
  {% raw %}{% include social-sharing.html %}{% endraw %}
  </div>
</div>
```

Above is the way currently I'm using to add tags to jekyll posts in Github Pages.

<br />

> I also created a video to show it. You can check it out on Youtube here:
{: .prompt-info }

<iframe width="560" height="315" src="https://www.youtube.com/embed/BGCa46-70PU" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
<br />
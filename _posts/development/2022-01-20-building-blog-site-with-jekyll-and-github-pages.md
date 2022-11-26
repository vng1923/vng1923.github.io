---
layout: post
title:  "Building Blog Website with Jekyll and Github pages"
date:   2022-01-20 18:22:05 -0700
categories: [Development]
path: "development"
tags: ["Ruby on Rails", "jekyll", "github"]
---

I created this blog by using Jekyll and Github Page. Jekyll is a gem that help you transform your plain text into static websites and blogs.

Jekyll uses the [Liquid](https://shopify.github.io/liquid/){:target="_blank"} templating language to process templates. Checkout this [document](https://shopify.github.io/liquid/){:target="_blank"} if you want to learn more about Liquid.

### Install Jekyll

```sh
gem install bundle jekyll
```

### Create new app with jekyll
```sh
jekyll new blog
cd blog
bundle jekyll serve --trace
```
Now you can access your site at http://127.0.0.1:4000 by default.

### [Folder Structure](https://jekyllrb.com/docs/structure/){:target="_blank"}

```markdown
.
├── _config.yml
├── _data
│   └── members.yml
├── _drafts
│   ├── begin-with-the-crazy-ideas.md
│   └── on-simplicity-in-technology.md
├── _includes
│   ├── footer.html
│   └── header.html
├── _layouts
│   ├── default.html
│   └── post.html
├── _posts
│   ├── 2007-10-29-why-every-programmer-should-play-nethack.md
│   └── 2009-04-26-barcamp-boston-4-roundup.md
├── _sass
│   ├── _base.scss
│   └── _layout.scss
├── _site
├── .jekyll-cache
│   └── Jekyll
│       └── Cache
│           └── [...]
├── .jekyll-metadata
└── index.html # can also be an 'index.md' with valid front matter
```


### [Permarklinks](https://jekyllrb.com/docs/permalinks/){:target="_blank"}

Permalinks are the output path for your pages, posts, or collections. They allow you to structure the directories of your source code different from the directories in your output.
There are 2 ways to set Permarklinks:
- Global in `_config.yml`

```
permalink: /:year/:month/:day/:title:output_ext
```

- In each page (Front Matter)

```
---
permalink: /my-stories/
---
```

### Create blog posts

Each post is an individual file in `_posts` folder. Adding a new file to this folder will make a new blog post appear on your website.

The blog posts file names follow a `date-slug.markdown` naming convention. The date should be formatted like this `YYYY-MM-DD`. The slug is the part of the URL identifying a particular post.

Jekyll posts and pages are written in Markdown. Markdown is a markup language which uses plain-text formatting syntax. For example, headings in markdown are made by a set preceding # sign(s). Below is a H1 HTML equivalent in markdown.
```erb
{% raw %}
# This is post title
{% endraw %}
```

You can learn common markdown syntax [here](https://www.markdownguide.org/cheat-sheet/){:target="_blank"}.

This is an example about my post
```markdown
---
layout: post
title:  "Building Blog Website with Jekyll and Github pages"
date:   2022-01-20 18:22:05 -0700
categories: development
path: "development"
tags: rails jekyll github
---

My Post content here

```


### Custom layout

All layouts inside `_layout` folder. By default, jekyll using [minima](https://github.com/jekyll/minima){:target="_blank"} as default theme:
- `home.html`: layout for homepage
- `page.html`: layout for page
- `post.html`: layout for post

All are inherited from `default.html`

You can also create your own new theme by
```sh
# Terminal: Development
jekyll new-theme your-awesome-theme
```

Check [it](https://jekyllrb.com/docs/themes/){:target="_blank"} out for more details...

### Deploy

Now, you just need to follow [this instruction](https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll){:target="_blank"} to deploy your blog to github page and can use it with your custom domain.


<br />

> I also created a video to show it. You can check it out on Youtube here:
{: .prompt-info }

<iframe width="560" height="315" src="https://www.youtube.com/embed/l5RZJEyg5WU" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
<br />
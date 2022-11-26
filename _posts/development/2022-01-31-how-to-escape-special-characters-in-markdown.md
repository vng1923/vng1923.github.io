---
layout: post
title:  "How to escape special characters in markdown"
date:   2022-01-31 15:26:05 -0700
categories: [Development]
path: "development"
tags: ["Ruby on Rails", "jekyll", "Markdown", "github"]
---

With [previous post](https://bennguyen.us/2022/01/21/building-blog-site-with-jekyll-and-github-pages.html){:target="_blank"}, I show you guys how to create blog site with jekyll and github pages. And when working on that post, I had some troubles with showing special characters in view. So this post will show you how I play with it.

Markdown treats these characters as ordinary text if there is backslash escape character in front of them:

```markdown
\\ backslash itself
\` backtick
\* asterisk
\_ underscore
\{ \} curly braces
\[ \] square brackets
\( \) parentheses
\# hash mark
\+ plus sign
\- minus sign (hyphen)
\. dot
\! exclamation mark
```

About the ampersand (&), less than (<) and greater than (>)
```markdown
&amp; &
&lt; <
&gt; >
```

Finally, if you want to escape ```{% raw %} {%  {% endraw %}``` in markdown, you need to wrap it with {% raw %} ```{% raw %}``` {% endraw %} and ```{% raw %}{%{% endraw %} endraw {% raw %}%}{% endraw %}``` tags.
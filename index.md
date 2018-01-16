---
title: Calum's Pages

project:
  name: "Calum's Pages"
  tagline: "Work in progress"

navigation:
  - name: "Example"
    link: "/2018/01/16/example.html"
---

# Home Page

_This is a work in progress._

```shell
$ sudo shutdown
```
<ul>
  {% for post in site.posts %}
    <li>
      <a href="{{ post.url }}">{{ post.title }}</a>
    </li>
  {% endfor %}
</ul>

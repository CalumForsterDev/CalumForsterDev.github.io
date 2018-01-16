---
title: Calum's Pages
---

# Home Page

_This is a work in progress_

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

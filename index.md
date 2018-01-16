---
title: Calum's Pages

navigation:
  {% for post in site.posts %}
    - name: "{{ post.title }}"
      link: "{{ post.url }}"
  {% endfor %}
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

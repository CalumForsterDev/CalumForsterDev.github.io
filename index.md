# Home Page

_This is a work in progress._

```shell
$ sudo shutdown
```

## Posts
{% for post in site.posts %}
 * [{{ post.title }}]({{ post.url }})
{% endfor %}

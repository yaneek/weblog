---
layout: default
---

{% for post in site.posts %}

{{ post.date }} - [{{ post.title }}]({{ site.baseurl }}{{ post.url }})

> {{ post.excerpt }}

---
{% endfor %}

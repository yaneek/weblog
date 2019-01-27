---
layout: default
---

{% for post in site.posts %}
{{ post.date | date: "%m/%d/%Y" }} - [{{ post.title }}]({{ site.baseurl }}{{ post.url }})

> {{ post.excerpt }}

---
{% endfor %}

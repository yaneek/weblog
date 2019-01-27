---
layout: default
---

{% for post in site.posts %}
## {{ post.date | date: "%Y-%m-%d" }} - [{{ post.title }}]({{ site.baseurl }}{{ post.url }})

### {{ post.excerpt }}

---
{% endfor %}

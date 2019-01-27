---
layout: default
---

{% for post in site.posts %}
## {{ post.date | date: "%Y-%m-%d" }} - [{{ post.title }}]({{ site.baseurl }}{{ post.url }})

### {{ page.excerpt | strip_html }}

---
{% endfor %}

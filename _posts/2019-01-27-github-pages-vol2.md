---
layout: default
title:  "Test GitHub Pages - #2"
permalink: "/posts/github-pages-test-vol2"
---

# Jak z Github Pages zrobic plaformę blogową

Ok, w poprzednim poście udało nam się stworzyć readme i go opublikować. Ale pojedynczy plik to jeszcze nie platforma blogowa. Tutaj z pomocą przychodzi system [Jekyll](https://jekyllrb.com/). Jest to generator stron opierający się o pliki tekstowe (takie jak *.md). Na Jekyll-u jest zbudowany cały Guthub Pages. To znaczy, że już mamy plaformę i wystarczy ją dokonfigurować.

## Jak pisać posty?

* tworzymy folder `_posts`
* tworzymy plik w formacie `YYYY-MM-DD-tytul-strony.md`, np `2019-01-27-github-pages-vol2.md`
* każdy post musi się rozpoczynać od nagłówka (tzw [Front Matter](https://jekyllrb.com/docs/front-matter/)):

```
---
layout: default
title:  "Test GitHub Pages - #2"
permalink: "/posts/github-pages-test-vol2"
---

# Some page content

![some image](../img/image.png)
```
Eksperymantalnie doszedłem do tego, że aby zarówno w edytorze jak i na stronie poprawnie wyświetlały się obrazki należy ustawić ścieżkę `permalink` na jeden poziom zagnieżdzenia np `permalink: "/any-virtual-path/blog-page-name"` i wtedy URL-e obrazków definiujemy względnie `../img/some-image-file`. W innym przypadku albo będziemy mieli poprawne wyświetlanie w edytorze albo na stronie.

> Jest jeszcze opcja ustawienia własnej domeny i to też zadziała ale tutaj się tym nie będę zajmował.

## Definicja strony głównej

Posty już mamy na repo ale nadal nie widać ich na naszej stronie? Jedyne co widzimy to ładnie sformatowany plik readme, który stworzyliśmy w poprzednim artykule.

Aby pokazać nasze posty musimy utworzyc dokument strony głównej. Musi to być plik `index.md` (lub `.html`) i wypełniamy go używając silnika szablonó [liquid](https://jekyllrb.com/docs/step-by-step/02-liquid/). Tak jak przy poście musimy mieć nagłówek, następnie iterujemy po wszystkich postach i wyświetlami linka z url-em:

{% raw %}
```
---
layout: default
---

{% for post in site.posts %}
## {{ post.date | date: "%Y-%m-%d" }} - [{{ post.title }}]({{ site.baseurl }}{{ post.url }})

### {{ post.excerpt | strip_html }}
---
{% endfor %}
```
{% endraw %}
Jest tutaj trochę magii z formatowaniem, nie wygląda to czytelnie ale robimy to tylko raz.


Przydatne linki:
* [Jekyll cheatsheet](https://devhints.io/jekyll)
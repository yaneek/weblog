---
layout: post
title:  "GitHub Pages - test"
---

# Start

Cześć! To jest test Github Pages, zastanawiam się czy można to w prostym zakresie wykorzystać jako platforma mini blogowa. Szczególnie jestem zainteresowany możliwością wstawiania sformatowanego kodu źródłowego w różnych językach oraz screenshotów.

No to do dzieła! Założyłem, że chcę publikować pliki *.md, nie czytałem dokumentacji, ale zakładam, że jest to możliwe. O moich doświadczeniach przeczytacie w dalszej części.

## Jak edytować pliki md?

Zanim opublikujemy pliki `*.md` musimy je stworzyć. Oczywiście tutaj nie ma wielkiej filozofii ale ja szukam czegoś więcej niż nodepad. Praktycznie dowolny edytor kodu rozpoznaje rozszerzenie *.md i z dużym prawdopodobieństwem będziemy mieli formatowanie składni. Jako przykład bardziej zaawansowanych narzędzi pokażę dwa: Visual Studio Code oraz Markdown Monster

### Visual Studio Code
Szeroko stosowany edytor kodu, więc nie trzeba dodatkowych, zewnętrznych narzędzi, obłsuga plików *.md jest natywna tzn nie musimy instalować dodatkowych rozszerzeń.
![Visual Studio Code](img/vsc.png)

### Markdown Monster
Narzędzie open source lecz nie oznacza to, że jest darmowe. Za darmo dostaje się wyłącznie wersję trial. Jest to specjalizowany kombajn obsługujący tworzenie, konwersje jak również wdrożenia.

![Markdown Monster](img/mm.png)

### Porównanie

#### Formatowanie

Przykładowy kod yaml:
```yml
stages:
  - audit
  - prepare
  - lint
  - build
  - test
  - prepare-deploy
  - deploy

.defaults: &defaults
  image: node:8.9
  tags:
    - docker
    - giftcard

audit-code:
  image: axabee/security-scanner:latest
  tags:
    - docker
    - giftcard
  stage: audit
  script:
    - security-scanner
  allow_failure: true

install-deps:
  <<: *defaults
  stage: prepare
  cache:
    key: "node_modules_cache"
    paths:
      - node_modules_cache
  script:
    - >
      yarn install \
        --no-progress \
        --non-interactive \
        --cache-folder ./node_modules_cache
    - yarn run bootstrap
  artifacts:
    paths:
      - node_modules
      - packages/**/node_modules
    expire_in: 20min
```

**MM**: Podgląd jest dobrej jakości ale samo formatowanie kodu słabiutkie:
![](img/mm-yaml.png)

**VSC**: Dobrej jakości formatowanie i podgląd:
![](img/vsc-yaml.png)


#### Podgląd dokuemntu
* **vsc**: Cały kod pokazywany jest na żywo w trakcie pisania. Na podglądzie zawsze mamy zaznaczony pionową kreską paragraf, który edytujemy
* **mm**: Podgląd aktualizuje się z pewnymi interwałami, czasami przestaje się aktualizować, szczególnie gdy mamy błąd w składni to nawet gdy ten błąd poprawimy to juz widok pozostaje taki sam do czasu aż nie zmienimy paragrafu

#### Outline

@TODO

#### Nawigacja pomiędzy zlinkowanymi dokumentami

@TODO

#### Tabelki

Przykład kodu tabelki:

```
|Header 1|Header 2|Header 3|
|---:|:---:|:---|
| Column 1 | Column 2 | Column 3 aaaa |
| Column 1 | Column 2 bbb | Column 3 |
| Column 1 ccc| Column 2 | Column 3 |
```

**MM** Tabelka:
![](img/mm-table.png)

**VSC** Tabelka:
![](img/vsc-table.png)

#### Obrazki

Obydwa edytory dobrze wyświetlają obrazki ale to co jest zdecydowanie na plus dla MM to obsługa wklejania obrazków ze schowka, CTRL+V i pokazuje się dialog, w którym wskazujemy lokalizację i nazwę pliku (png, jpg, gif). Czegoś takiego właśnie szukałęm! Jest też możliwość przenoszenia obrazków z eksploratora bezpośregnio do dokumentu.

### Ostateczne podsumowanie

Poniżej wskażę funkcjonalności, które wykorzystuję edytując pliki *.md. Skupię się głównie na tych, które w znaczny sposób się różnią pomiędzy edytorami:

|Funkcjonalność|Visual Studio Code|Markdown Monster|
|-|-|-|
| Platforma | windows, linux, macos | windows |
| Podgląd na żywo | tak | z opóźnieniem |
| Podgląd dokumentu | tak | tak |
| Formatowanie składni markdown | tak | nie zawsze czytelne |
| Formatowanie cytowanych kodów źródłowych | tak | nie zawsze czytelne |
| Wybór renderer-a | nie | tak, wiele różnych platform, np github, medium itd |
| Obsługa wstawiania zdjęć | nie | tak, ze schowka, pliku, drag & drop |
| Formatowanie za pomocą skrótów CTRL+B, CTRL+I itd | nie, wymaga zainstalowania rozszerzenia | tak |
| Zmiana ścieżek do obrazków przy przy zmianie nazwy obrazka | nie | nie |
| Krytyczne bugi | nie zauważyłem | tak, np. zawieszenie aplikacji przy nawigacji po folderach, gubienie plików po drag & drop |

Ostatecznie z MM będę korzystał chyba wyłącznie do łatwego wklejania zrzutów ekranów a przy codziennej pracy znacznie pewniejszym narzędziem jest VSC.

## Jak opublikować GitHub Pages

Strony, które chcecie opublikować będą dostępne pod adresem `https://[user name].github.io/[repository name]/`. Aby aktywować GitHub Pages należy wykonać parę kroków. Oczywiście minimalne wymagania to konto na githubie i minimalne pojęcie jak korzystać z `git-a`.

### Publikacja plików *.md

Oczywiście rozpoczynamy od pusha pliku `README.md` na nasze repozytorium. Plik ten musi się znajdować w jednej z lokalizacji:
* folder `/` na branch-u `master`
* folder `/docs` na branch-u `master`
* folder `/` na branch-u `gh-pages`

Oczywiście jeżeli ktoś chce to może umieścić pliki inne niż *.md. Np `index.html`, w którym mamy znacznie większe możliwości ale nie to jest celem tego artukułu - skupiamy się na plikach md, md i jeszcze raz md :)

### Konfiguracja repozytorium github

* wchodzimy w konfigurację repozytorium: `settings/options/GitHub Pages`
![](img/github-entry-settings.png)
![](img/github-entry-settings-2.png)
![](img/github-entry-settings-3.png)
* `Source` wskazujemy na rozwijanej liście lokalizacje naszego pliku `md`. Akceptujemy za pomoca `Save` i już po paru chwilach mamy opublikowaną stronę
![](img/github-entry-settings-4.png)

Przydatne linki:
* [Markdown cheatsheet](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet)
* [Markdown Monster](https://markdownmonster.west-wind.com/)
* [Visual Studio Code - markdown support](https://code.visualstudio.com/docs/languages/markdown)
* [Visual Studio Code - markdown shortcuts extension](https://marketplace.visualstudio.com/items?itemName=mdickin.markdown-shortcuts)
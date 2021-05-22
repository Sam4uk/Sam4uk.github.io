---
title: "Десять кроків до особистого блогу на Github Pages." 
date: 2020-12-07
# date: 2020-01-03
# publishdate: 2020-12-07
description: "Покрокова інструкція по створенню безкоштовного блогу або сайту на Github Pages з використанням Hugo для початківців."
draft: false
hideToc: false
enableToc: true
enableTocContent: false
author: Vitaly Khabarov
authorDesc: Энтузиаст разработки цифровых продуктов
authorImageUrl: https://vitkhab.pro/images/vitkhab.webp # your image url. We use `authorImageUrl` first. If not set, we use `authorImage`.
socialOptions: # override params.toml file socialOptions
  github: https://github.com/vitkhab
# authorEmoji: 🎅
pinned: false
tags:
- hugo
- github pages
- blog
- personal brand
series:
-
categories:
- hugo
- tutorials
# image: images/feature2/color-palette.png
################
# tags: ["github pages", "blog", "hugo", "personal brand"]
# draft: false
# comments: false
# cover: "https://images.pexels.com/photos/262508/pexels-photo-262508.jpeg?cs=srgb&dl=pexels-pixabay-262508.jpg&fm=jpg"
# summary: "Покрокова інструкція по створенню безкоштовного блогу або сайту на Github Pages з використанням Hugo для початківців."

# author:
#   name: "Vitaly Khabarov"
#   desc: "Энтузиаст разработки цифровых продуктов"
#   avatar: "https://vitkhab.pro/images/vitkhab.webp"
# categories:
# - tutorials
---

[//]: # (Обложка взята с https://owips.com/clipart-15997066)

### Крок перший. Підготовка інструментів.

<!-- 
Разработчики Hugo подробно описали методы установки на популярные ОС в&nbsp;[документации](https://gohugo.io/getting-started/installing/). Hugo с помощью Homebrew и Linuxbrew устанавливается командой:
 -->
<!-- ```zsh
brew install hugo
```

Также тебе потребуется `git`. Методы установки описаны в [руководстве по Git](https://git-scm.com/book/ru/v2/%D0%92%D0%B2%D0%B5%D0%B4%D0%B5%D0%BD%D0%B8%D0%B5-%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%BA%D0%B0-Git).

Теперь тебе доступны команды `hugo` и `git`.
 -->
### Крок другий. Репозиторій на Github.

Настав час [зареєструватися на GitHub](https://github.com/join), якщо ви цьго ще не зробили. Після [створи репозиторій](https://github.com/new). Ім'я репозиторію має відповідати шаблону `<OWNER>.github.io`, де `<OWNER>`, тут та надалі ім'я твого облікового запису чи організації, якій належить репозиторій. Репозиторій має бути порожнім та публічним. Сняти галочку з `Initialize this repository with a README`, а перемикачі `Add .gitgnore` та `Add a license` виставити в положення `None`.

![github-repo](https://raw.githubusercontent.com/vitkhab/vitkhab.pro/master/content/blog/2020-01-03-how-to-create-blog/github-repo.png)

Тепер у вас є репозиторій. В ньому ви будуте зберігати статті та налаштування блогу.

### Крок третій. Кодова база.

Hugo генерує сайт на основі шаблонів, налаштувань та вихідного тексту. Створи основу нового сайту командою:

```zsh {linenos=false}
hugo new site <OWNER>.github.io
```

Ініціалізуйте git-репозиторій та підєднайте до Github'у. Для персональних сайтів виду `<OWNER>.github.io`, GitHub Pages відображує сайт з вітки `master`. Відка буде порожня, доки відсутній згенерований сайт. Виконайте команди:

```zsh {linenos=false}
cd <OWNER>.github.io
git init
git commit --allow-empty -m "Initializing master branch"
git remote add origin git@github.com:<OWNER>/<OWNER>.github.io.git
git push -u origin master
```

Саму кодову базу та вихдний код з якого генеруватиметься сайт, будемо зберігати у гілці `devel`. Так ми розділимо код і результуючий артефакт. Зможемо працювати з ними незалежно. Виконай команди:

```zsh {linenos=false}
git checkout -b devel
git add --all .
git commit -m 'Initial commit'
git push -u origin devel
```

### Крок четвертий. Вибір та установка стилю.


Обери довподоби своєму блогу стиль на [сайті тем Hugo](https://themes.gohugo.io/). Підєднай тему, що сподобалась як субмодуль git  команда виду, для прикладу використовуєтьс тема `dream-plus`:
```zsh {linenos=false}
git submodule add git@github.com:UtkarshVerma/hugo-dream-plus.git themes/dream-plus
```

<!-- Тему можешь скачать в директорию `<OWNER>.github.io/themes` или склонировать репозиторий с темой в ту же директорию. Я предпочитаю использовать субмодули. Темы можно легко обновлять из источника. Тему можно дополнить модулями в&nbsp;директории `<OWNER>.github.io/layouts`. Почитать о выборе между использование `git clone` или `git submodule` для тем Hugo можешь в [обсуждении](https://discourse.gohugo.io/t/adding-a-theme-as-a-submodule-or-clone/8789). -->

### Крок п'ятий. налаштування Hugo.

Настав час налаштувати Hugo. Відредагуйте файл `config.toml` до наступного змісту, забудь відредагувати параметри під свій сайт:

<!-- # Язык сайта, для английского используй "en-us"
languageCode = "ru-ru" -->
```toml {linenos=false}
# Адреса вашого сайту
baseURL = "https://<OWNER>.github.io/"


# Назва вашого сайту
title = "Супер бложик"

# Тема що використовується
theme = "dream-plus"

# Сюди Hugo збереже згенерований сайт
publishdir = "./public/"
```

### Крок шостий. Директорія для публикації.

Вихідний коди та сам сайт зберігаються в різних відках. Перемикатися між ними та переносити зміни -  незручно. Тому підєднуємо вітку `master` в робосий каталог `public` командами:

```zsh {linenos=false}
git worktree add -B master public origin/master
echo "public" >> .gitignore
git add .gitignore
git commit -m 'Add .gitignore'
```

Таку операцію доведеться повторювати при створенні робочого каталогу, на кожному робочому комп'ютері.
Генерацію сайту можна передати CI-системі та забути про ручні зміни.

### Крок сьомий. Публікація головної сторінки. 

Пора вийти в світ з пісочниці. Для початку згенеруй сайт командою:

```zsh {linenos=false}
hugo
```

А тепер вивантажи його на GitHub командами:

```zsh {linenos=false}
pushd public
git add .
git commit -m 'Add index page'
git push
popd
```

І ось тут ваш сайт має стати доступним. Але черз невідомі мені причини GitHub Pages стабільно підхоплює новий сайт тільки після другого-третього комміту. Не розстроюйтесь, скоро ми його зробимо.

### Крок восьмий. Перший пост.

Створи перший пост командою:

```zsh {linenos=false}
hugo new posts/first-post.md
```

Hugo підготує шаблон нової сторінки. Відкрий файл `posts/first-post.md` та відредагуй його. На початку ви помітите блок з метаданими посту, після яких починається сам текст статті у форматі `markdown`, хоча є можливість використати інший формат [другой формат](https://gohugo.io/content-management/formats/). 

```toml {linenos=false}
---
# Назва статті
title: "Блог на Github Pages для чайників"

# Дата статті
date: 2019-12-25T21:32:05+03:00

# Теги статті
tags: ["github pages", "blog", "hugo"]

# Ознака чернетки, допоки в занченні "true", Hugo не буде відображати цю статтю
draft: false

# Увімкнення коментарів
comments: true

# Стислий опис статті
summary: "Покрокова інструкція по створенню безкоштовного блогу або сайту на Github Pages з використанням Hugo для початківців."
---
```

<!-- Конечно же, первый пост должен быть о том, как сделать свой собственный блог. Можешь взять за основу [исходный текст статьи, которую ты сейчас читаешь](https://raw.githubusercontent.com/vitkhab/vitkhab.pro/master/content/blog/2020-01-03-how-to-create-blog/index.md) ;) -->

### Крок десятий. 
<!-- Навигационное меню. -->

<!-- Создай на сайте навигационное меню. Для этого добавь в файл `config.toml` строки:
```toml
[[menu.main]]
    # Отображаемое название раздела
    name = "Статьи"

    # Вес для сортировки пунктов меню, чем меньше - тем раньше пункт будет отображен
    weight = 100

    # Идентификатор родителя для вложенных пунктов, не все темы поддерживают вложенность
    identifier = "blog"

    # Путь до раздела со статьями, соответствует имени папки внутри <OWNER>.github.io/content/
    url = "/blog"
```

Для добавления нового пункта, добавь еще один блок `[[menu.main]]` целиком.  -->

### Крок десятий. Profit!

Ми пройшли всю необхідну підготовчу роботу. Збережи зміни кодової бази:

```zsh {linenos=false}
git add .
git commit -m 'Add index page, first post, navigation menu and config'
git push
```

Згенеруй сайт та вивантаж зміни на Github.

```zsh {linenos=false}
hugo

pushd public
git add .
git commit -m 'Publish first post'
git push
popd
```

Зачекай кілька хвилин, доки GitHub Pages опрацює зміни. Зайти на персональний сайт `https://<OWNER>.github.io/` та насолоджуйся результатом!

# Режим Pro або що далі?

А ділі потрібно автоматизувати генерацію сайту з допомогою CI, налаштувати красивий персональний домен, під'єднати коментарі та налаштувати систему аналітики GoogleAnalytics. Про це іншим разом

Stay tuned!

[Оригінал статті](https://vitkhab.pro/blog/2020-01-03-how-to-create-blog/)

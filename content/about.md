---
title: About
date: 2017-08-20 21:38:52 +0800
lastmod: 2017-08-28 13:41:52 +0000
weight: 50
comment: false
mathjax: false
type: page
menu:
  main:
    weight: 1

---
Hugo has a lot of templates published on the net, but when designing the way you want it, you will create your own theme. To create a theme, first output the template with the following command.

    $ hugo new theme ＜テーマ名＞
    

For example, if you execute as follows, the `themes/my-theme`directory will be created.

    $ hugo new theme my-theme
    

The generated file group is as follows and the directory structure is batched, but the description in the file is almost empty. Based on this file group, I will create a template.

    themes/my-theme/
       ├── LICENSE.md（MIT ライセンス）
       ├── archetypes/
       │   └── default.md（ほぼ空っぽ）
       ├── layouts/
       │   ├── 404.html（空っぽ）
       │   ├── _default/
       │   │   ├── list.html（空っぽ）
       │   │   └── single.html（空っぽ）
       │   ├── index.html（空っぽ）
       │   └── partials/
       │       ├── footer.html（空っぽ）
       │       └── header.html（空っぽ）
       ├── static/
       │   ├── css/
       │   └── js/
       └── theme.toml（デフォルトの設定ファイル）
    

## Create layout of top page (layouts / index.html)

![create-theme1.png](http://maku77.github.io/hugo/create-theme1.png)

In the theme directory `layouts/index.html`is the template file for the top page of the site. If you create a site (SPA: Single Page Application) consisting of only one HTML file, you only need to create this file. Since nothing is written in the initial state, let's start by modifying it so that it displays only the site name at the beginning.

#### themes / my-theme / layouts / index.html

    <h1>{{ .Site.Title }}</h1>
    

By doing the above, you can output the value `.Site`of the `Title`field of the variable holding the site information . Here, the value set in the site setting file ( `config.toml`) `title`is expanded.

After creating so far, let's display the site using this theme.

    $ hugo server -t my-theme
    

After starting up the server, you can check the display by accessing [**http: // localhost: 1313 /**](http://localhost:1313/) .

## Display a list of all pages on the top page

![create-theme2.png](http://maku77.github.io/hugo/create-theme2.png)

By referring to variables `layouts/index.html`in the top page template ( ), you can retrieve `.Data.Pages`information ( [**Page variable**](https://gohugo.io/variables/page/) ) of all pages . `range`If you loop through this information, you can output the link tag to all pages.

#### themes / my-theme / layouts / index.html

    <h1>{{ .Site.Title }}</h1>
    <ul>
      {{ range .Data.Pages }}
        <li><a href="{{ .RelPermalink }}">{{ .Title }}</a> ({{ .Date.Format "2006-01-02" }})
      {{ end }}
    </ul>
    

## Create a layout for each page (layouts / _default / single.html)

Since each page of the link destination `layouts/_default/single.html`is generated based on the template file, this file must also be created in advance. Within this template, you can refer to the field (for example ) of the [**Page variable**](https://gohugo.io/variables/page/)`.Title` .

#### themes / my-theme / layouts / _ default / single.html

    <h1>{{ .Title }}</h1>
    {{ .Content }}
    

The content of each page is `content/`created in the directory as follows.

#### content / page1.md

    ---
    title: "Page1 Title"
    date: 2017-09-10
    ---
    
    Page1 Content
    

If you create the layout and content as above, the contents of each page should be displayed as below.

![create-theme3.png](http://maku77.github.io/hugo/create-theme3.png)
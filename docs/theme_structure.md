# Theme Structure
The following is an extensive guide on how themes should work in OctoberCMS

?>This guide assumes that you have a basic understanding of `html`, `css`, `twig`, and OctoberCMS theming. If you do not, I suggest you read the documentation below.
<br><br> [MDN Docs on HTML :fas fa-external-link-alt:](https://developer.mozilla.org/en-US/docs/Web/HTML)
<br>[MDN Docs on CSS :fas fa-external-link-alt:](https://developer.mozilla.org/en-US/docs/Web/CSS) 
<br> [Symphony's Documentation on Twig :fas fa-external-link-alt:](https://twig.symfony.com/doc/2.x/)
<br> [OctoberCMS Theming Docs :fas fa-external-link-alt:](https://octobercms.com/docs/cms/themes)

</br>

## Initial Structure
When  creating themes in OctoberCMS, use this structure:
``` html
└── 📁 theme-name
    └── 📁 assets
    |     ├── 📁 css
    |     |     └── #️⃣ styles.css        <!-- main css file. do not change name. -->
    |     ├──  📁 js
    |     |     └── 📄 script.js         <!-- main js file. do not change name. -->
    |     └──  📁 img
    |     |     └── 🖼️ image.jpg         <!-- all theme images go gere -->
    ├── 📁 content                       <!-- how all content will be structured. -->
    |     ├── 📁 page_name
    |     |     └── 🟧content_name.htm 
    |     ├── 📁 page_name_2
    |     |     └── 🟧content_name_2.htm 
    ├── 📁 layouts
    |     ├── 🟧 default.htm             <!-- main layout file. do not change name. -->
    |     └── 🟧 page.htm                <!-- main layout file for pages. do not change name. -->
    ├── 📁 pages
    |     └── 🟧 home.htm                <!-- home page. do not change name -->
    └── 📁 partials
          ├── 🟧 head.htm                <!-- head code for pages. do not change name. -->
          ├── 🟧 header.htm              <!-- navigation code for pages. do not change name. -->
          ├── 🟧 foot.htm                <!-- foot code for pages (before closing </body> tag). do not change name. -->
          └── 🟧 footer.htm              <!-- footer for pages. do not change name. -->
```

!>Note: this is a strict guideline. Do not change the names of these files or folders under any circumstance. These are put in place to make sure everyone knows where the files are and how to get to them, thus creating a workable, consistent coding environment.

Below is a explanation on what files each folder will have and how each folder will be structured.

</br>

## Assets

The `📁assets` folder is where we will store all of our `#️⃣css`, `📄js`, and `🖼️img` files. The files in these folders will style and create the functionality of theme so it's imperative that we keep the file count small and easy to navigate. 

### CSS
The `📁css` folder should contain one main file to style the entire theme. This file name is called `#️⃣styles.css`. If this file does not exist, you will need to create it. 

!>The name of this file __will not be changed__ and we will not add any other `#️⃣.css` files here unless they are modules or extensions. 

If you need to add other modules on the site that require a `#️⃣.css` file, add them here.
For example, if you would like to add [jquery.fancybox](https://fancyapps.com/), add this `#️⃣.css` file in this folder.

``` html
└── 📁 css
    └── #️⃣ styles.css                   <!-- main css file. do not change name. -->
    └── #️⃣ jquery.fancybox.min.css      <!-- fancybox css file -->
```

Be sure to call it in your `🟧head.htm` partial as well. 

``` twig
...
<link rel="stylesheet" href="{{ 'assets/css/jquery.fancybox.min.css'| theme }}>
...
```

### JS
The `📁js` folder should contain one main javascript file for the entire theme. This file name is called `📄script.js`. If this file does not exist, you will need to create it. 

!>The name of this file __will not be changed__ and we will not add any other `📄.js` files here unless they are modules or extensions. 

If you need to add other modules on the site that require a `📄.js` file, add them here.
For example, if you would like to add [jquery.fancybox](https://fancyapps.com/), add this `📄.js` file in this folder.

``` html
└── 📁 js
    └── 📄 script.js                   <!-- main js file. do not change name. -->
    └── 📄 jquery.fancybox.min.js      <!-- fancybox js file -->
```

Be sure to call it in your `🟧foot.htm` partial as well. 

``` twig
...
<script src="{{ 'assets/js/jquery.fancybox.min.js'|theme }}>
...
```

### IMG
The `📁img` folder should contain all of the images associated with the theme.

?> This should not contain images that can be dynamically generated. More specifically, this folder should contain images that need to be rendered in each partial, and page directly.

Example of the image file structure

``` html
└── 📁 img
    └── 🖼️ logo.png
    └── 🖼️ hero.jpg
```

</br>

## Content

`🟧content` files are chunks of HTML code that are used to display static content across the site. __They do not use `twig` and are not dynamic.__ When creating content files, make sure they are in a folder relative to the page name on which they will be displayed. Example below:

```
└── 📁 content                      
    ├── 📁 home
    |     ├── 🟧hero-title.htm 
    |     └── 🟧hero-description.htm 
    └── 📁 about
          ├── 🟧about-title.htm 
          └── 🟧about-description.htm 
```

!> Note: `🟧 content` files will not contain any HTML classes, ids, divs, special html tags (e.g. `<article>`, `<section>`, etc), or attributes. The only tags that these files are allowed to have are as follows:
<br><br> `<p>`
<br> `<ul>`
<br> `<li>`
<br> `<span>`
<br> `<blockquote>`
<br> `<strong>`

### Rendering
To render those files, you will need to use the `{% content %}` tag like so:

``` twig
<div class="hero">
    <div class="container hero-container">
        {% content 'home/hero-title' %}
        {% content 'home/hero-description' %}
    </div>
</div>
```

?> Note, when using plugins associated with `🟧content` files, make sure you maintain this structure. This makes it easy for clients to go and make edits and easy for us to find files. If you would like to know more on how content files work, read the [OctoberCMS Documentation :fas fa-external-link-alt:](https://octobercms.com/docs/markup/tag-content)

</br>

## Layouts
Layouts define the page scaffold, that is everything that repeats on a page, such as a header and footer. Layouts will contain the `<html>` tag as well as the `<head>` and `<body>` tags.

We create layouts when we need to create a general structure on how the code should be rendered. Here's an example of how the `🟧default.htm` layout will look like:

``` twig
<!DOCTYPE html>
<html>
    <head>
        {% partial 'head' %}
    </head>
    <body>
        {% partial 'header' %}

        {# Where page 🟧content will be rendered #}
        {% page %} 

        {% partial 'footer' %}

        {% partial 'foot' %}
    </body>
</html>
```

?> Note: Use this a base on rendering layouts. Add `🟧partials` where needed. Do not add direct code here. 

### Rendering
In order to render the layout, you'll need to assign the layout to the page you're working with. Example below:

``` twig
title = "Home"
url = "/"

{# setting the layout here #}
layout = "default"
```


!> Note: You should only need to create a new layout if the entire structure of the the site will change, or a layout requires the use of a plugin (like the [Pages Plugin :fas fa-external-link-alt:](https://octobercms.com/plugin/rainlab-pages#documentation) for example)

</br>

## Pages

All websites have `🟧pages`. In OctoberCMS, `🟧pages` are represented with page templates.

 Each page has an ID which is associated with the filename. For example, if you create a page named `🟧home.htm` in the `📁pages` folder, the ID of the page will be `home`. 

`🟧pages` require layouts to be styled accordingly. They also accept [`🟧components`](/docs/code_of_conduct#components) can be used to display [`🟧partials`](#partials) & [`🟧content`](#content) as well.

### Creating A Page

To setup a page, create a `.htm` file in the `📁pages` folder and use the following markup as a base:

``` twig
title = "Home"      {# title of the page. Displayed in the backend #}
url = "/"           {# Where the page will be accessible in the browser #}
layout = "default"  {# Layout the page is using #}
==                  {# Marks the beginning of HTML #}

<div class="hero">
    <div class="hero-container">
        <h3>
            {# renders the page title onto the page #}
            {{ this.page.title }} 
        </h3>
        <p>A Cool Hero</p>

        {# Displaying a partial #}
        {% partial 'homePageAlert' %}

        {# displaying a content file #}
        {% content 'home/hero-content.htm' %}
    </div>
</div>
```

?>Note: Please name your pages according to the page's function. (e.g the Homepage should be named `🟧home.htm`)

### Rendering

To render page content, you need to use the `{% page %}` tag in a [`🟧layout`](#layouts). Simple example below:

``` twig
<html>
    <body>
        {% page %}
    </body>
</html>
```
</br>

## Partials

`🟧partials` are chunks of global, reusable code that is used throughout the theme and are rendered with the `{% partial %}` tag.

The `📁partials` folder should contain four main files that will be used across the theme. Those files are `🟧head.htm`, `🟧header.htm`, `🟧foot.htm` and `🟧footer.htm`. If they do not exist, you will need to create them.

Here's an example of the folder structure below. 

``` html
└── 📁 partials
    ├── 🟧 head.htm    <!-- head code for pages. do not change name. -->
    ├── 🟧 header.htm  <!-- navigation code for pages. do not change name. -->
    ├── 🟧 foot.htm    <!-- foot code for pages (before closing </body> tag). do not change name. -->
    └── 🟧 footer.htm  <!-- footer code for pages. do not change name. -->
```

!>The name of these files __will not be changed__ and we will not add any other partials in the root of the folder unless they meet the following requirements:
<br><br>The `partial` is going to be a global component (e.g. custom alerts.)
<br>The `partial` will be used across the entire website.
<br><br>If the partial does not meet any of these requirements, they need to be implemented per page and must be included in a folder. The folder name will be related to the function of the partial.

### `head.htm` Partial

This partial will contain all the code that goes in the `<head>` tag. This partial will __not__ contain the `<head>` tag itself. Example below:

``` twig
{# Bootstrap & FancyBox Stuff #}
<link rel="stylesheet" href="{{ 'assets/bootstrap/css/bootstrap.min.css'|theme }}"> 
<link rel="stylesheet" href="{{ 'assets/css/jquery.fancybox.min.css'|theme }}">

{# main css file. Do not change #}
<link rel="stylesheet" href="{{ 'assets/css/styles.css'|theme }}">

{# where styles will be injected for plugins #}
{% styles %}

{# viewport stuff for mobile #}
<meta name="viewport" content="width=device-width, user-scalable=no, initial-scale=1.0">

{# favicon stuff #}
<link rel="apple-touch-icon" sizes="180x180" href="{{ 'assets/img/apple-touch-icon.png'|theme }}">
<link rel="icon" type="image/png" sizes="32x32" href="{{ 'assets/img/favicon-32x32.png'|theme }}">
<link rel="icon" type="image/png" sizes="16x16" href="{{ 'assets/img/favicon-16x16.png'|theme }}">
```
?> Theme files can combined together. More info [here:fas fa-external-link-alt:](https://octobercms.com/docs/markup/filter-theme#combine-css-javascript) 

### `header.htm` Partial

This partial will contain the navigation of the site, typically right after the opening `<body>` tag depending on the theme. Example below:

``` twig
{# Using Bootstrap 4 in this example #}
<nav class="navbar navbar-light navbar-expand-md align-items-center">
    <div class="container">
        <a class="navbar-brand" href="{{ 'home'|page }}">
            <img class="img-fluid" src="{{ 'assets/img/logo.png'|theme }}">
        </a>
        <button data-toggle="collapse" class="navbar-toggler" data-target="#navcol-1">
            <span class="sr-only">Toggle navigation</span><i class="fas fa-bars"></i>
        </button>
        <div class="collapse navbar-collapse" id="navcol-1">
            <ul class="navbar-nav">
                <li class="nav-item active">
                    <a class="nav-link" href="{{ 'home'|page }}">Home</a>
                </li>
                <li class="nav-item">
                    <a class="nav-link" href="{{ 'features'|page }}">Features</a>
                </li>
                <li class="nav-item">
                    <a class="nav-link" href="{{ 'pricing'|page }}">Pricing</a>
                </li>
            </ul>
        </div>
    </div>
</nav>
```

You may notice that this template contains `twig` code referencing to a page. This code will render links to the pages in the [`📁pages`](#pages) folder.

The navigation style will vary from theme to theme, so change this code accordingly.

### `foot.htm` Partial
This partial will contain all of the code needed before the closing `<body>` tag. Usually javascript. Example below: 

``` twig
{# reference to jquery #}
<script src="{{ ['@jquery']|theme }}"></script>

{# Bootstrap Stuff #}
<script src="{{ 'assets/bootstrap/js/bootstrap.min.js'|theme }}"></script>

{# main script file. Do not change #}
<script src="{{ 'assets/js/script.js'|theme }}"></script>

{# reference to the OctoberCMS Framework. #}
{# Should be only included ONCE and after #}
{# jquery has been called.                #}
{% framework extras %}

{# where scripts will be injected for plugins #}
{% scripts %}
```

### `footer.htm` Partial

This partial will contain the footer code for the site. This code will be presented at the bottom of the page after all the content but before the `🟧foot.htm` partial. Example below

``` twig
{# Using Bootstrap 4 in this example #}
<div class="section footer">
    <div class="container">
        <div class="row">
            <div class="col-12 col-lg-3">
                <h5 class="footer-header">Navigation</h5>
                <ul class="nav flex-column">
                    <li class="nav-item">
                        <a class="nav-link" href="{{ 'home'|page }}">Home</a>
                    </li>
                    <li class="nav-item">
                        <a class="nav-link" href="{{ 'about'|page }}">Link</a>
                    </li>
                    <li class="nav-item">
                        <a class="nav-link" href="{{ 'contact'|page }}">Link</a>
                    </li>
                </ul>
            </div>
        </div>
    </div>
    <p class="small text-muted text-center">
        Copyright © Acme Inc. All Rights Reserved
    </p>
</div>
```

### Rendering
In order to render a partial, use the following code in a layout: 

``` twig
{# change the name to whatever partial you are referencing #}
{% partial 'footer' %}
```



## Next Steps

Now that you have a general idea on how our themes will be structured, lets move on to the Code of Conduct.

[Code of Conduct :fas fa-arrow-right:](/docs/code_of_conduct.md)
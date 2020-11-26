# Theme Structure
The following is an extensive guide on how themes should work in OctoberCMS

>This guide assumes that you have a basic understanding of html, twig, and OctoberCMS theming. If you do not, I suggest you read the following:
> - [MDN Docs on HTML](https://developer.mozilla.org/en-US/docs/Web/HTML) 
> - [Symphony's Documentation on Twig](https://twig.symfony.com/doc/2.x/)
> - [OctoberCMS Themeing Docs](https://octobercms.com/docs/cms/themes)

## Initial Structure
When  creating themes in OctoberCMS, use this structure:
``` html
└── 📁 theme-name
    └── 📁 assets
    |     ├── 📁 css
    |     |     └── #️⃣ styles.css        <!-- main css file. do not change name. -->
    |     ├──  📁 js
    |     |     └── 📄 script.js         <!-- main css file. do not change name. -->
    |     └──  📁 img
    |     |     └── 🖼️ image.jpg         <!-- all images go gere -->
    ├── 📁 content                       <!-- how all content will be structured. -->
    |     ├── 📁 page_name
    |     |     └── 🟧content_name.htm 
    |     ├── 📁 page_name_2
    |     |     └── 🟧content_name_2.htm 
    ├── 📁 layouts
    |     ├── 🟧 default.htm             <!-- main layout file. do not change name. -->
    |     └── 🟧 page.htm                <!-- main layout file for pages. do not change name. -->
    ├── 📁 pages
    |     └── 🟧 page_name.htm           <!-- main layout file for pages. do not change name. -->
    └── 📁 partials
          ├── 🟧 head.htm                <!-- head code for pages. do not change name. -->
          ├── 🟧 header.htm              <!-- navigation code for pages. do not change name. -->
          ├── 🟧 foot.htm                <!-- foot code for pages (before closing </body> tag). do not change name. -->
          └── 🟧 footer.htm              <!-- footer for pages. do not change name. -->
```

>Note: this is a strict guideline. Do not change the names of these files or folders under any circumstance. These are put in place to make sure everyone knows where the files are and how to get to them, thus creating a workable, consistent coding environment.

Below is a explanation on what files each folder will have and how each folder will be structured.


## Partials

`🟧partials` are chunks of global, reusable code that is used throughout the theme.

The `📁partials` folder should contain four main files that will be used across the theme. Those files are `🟧head.htm`, `🟧header.htm` `🟧foot.htm` and `🟧footer.htm`. If they do not exist, you will need to create them.

Here's an example of the folder structure below. 

``` html
└── 📁 partials
    ├── 🟧 head.htm    <!-- head code for pages. do not change name. -->
    ├── 🟧 header.htm  <!-- navigation code for pages. do not change name. -->
    ├── 🟧 foot.htm    <!-- foot code for pages (before closing </body> tag). do not change name. -->
    └── 🟧 footer.htm  <!-- footer code for pages. do not change name. -->
```

>The name of these files __will not be changed__ and we will not add any other partials here unless they meet the following requirements:
> - The `partial` is going to be a global component (e.g. custom alerts.)
> - The `partial` will be used across the entire website.
>
>If the partial does not meet any of these requirements, they need to be implemented per page and must be included in a folder. The folder name should be related to the function of the partial.

### `🟧head.htm` Partial

This partial will contain all the code that goes in the `<head>` tag. This partial will __not__ contain the `<head>` tag tho. Example below:

``` twig
<link rel="stylesheet" href="{{ 'assets/bootstrap/css/bootstrap.min.css'|theme }}"> 
<link rel="stylesheet" href="{{ 'assets/css/jquery.fancybox.min.css'|theme }}">

{# main css file. Do not change #}
<link rel="stylesheet" href="{{ 'assets/css/styles.css'|theme }}">

{# Theme files can combined together. 
More info here: https://octobercms.com/docs/markup/filter-theme#combine-css-javascript #}

{# where styles will be injected for plugins #}
{% styles %}

{# viewport stuff for mobile #}
<meta name="viewport" content="width=device-width, user-scalable=no, initial-scale=1.0">

{# favicon stuff #}
<link rel="apple-touch-icon" sizes="180x180" href="{{ 'assets/img/apple-touch-icon.png'|theme }}">
<link rel="icon" type="image/png" sizes="32x32" href="{{ 'assets/img/favicon-32x32.png'|theme }}">
<link rel="icon" type="image/png" sizes="16x16" href="{{ 'assets/img/favicon-16x16.png'|theme }}">
```

### `🟧header.htm` Partial

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

You may notice that this template contains twig code referencing to a page. This code will display links to the pages in the `📁pages` folder.

The navigation style will vary from theme to theme, so change this code accordingly.

### `🟧foot.htm` Partial
This partial will contain all of the code needed before the closing `<body>` tag. Usually javascript. Example below: 

``` twig
{# reference to jquery #}
<script src="{{ ['@jquery']|theme }}"></script>

{# Bootstrap Stuff #}
<script src="{{ 'assets/bootstrap/js/bootstrap.min.js'|theme }}"></script>

{# main script file. Do not change #}
<script src="{{ 'assets/js/scriptjs'|theme }}"></script>

{# reference to the OctoberCMS Framework. #}
{# should be only included ONCE and after #}
{# jquery has been called.                #}
{% framework extras %}

{# where scripts will be injected for plugins #}
{% scripts %}
```

### `🟧footer.htm` Partial

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


## Layouts
Layouts are a combination of partials that make up the theme. We create layouts when we need to create a general structure on how the code should be rendered. Here's an example of how the `🟧default.htm` layout will look like:

``` twig
<!DOCTYPE html>
<html>
    <head>
        {% partial 'head' %}
    </head>
    <body>
        {% partial 'header' %}

        {# Where page content will be rendered #}
        {% page %} 

        {% partial 'footer' %}

        {% partial 'foot' %}
    </body>
</html>
```

> Note: You should only need to create a new layout if the entire structure of the the site will change, or a layout requires the use of a plugin (like the [Pages Plugin](https://octobercms.com/plugin/rainlab-pages#documentation) for exapmle)

## Assets

The `assets` folder is where we will store all of our `#️⃣css`, `📄js`, and `🖼️img` files. These folders will style the website and create the theme so it's imperative that we keep them small and easy to navigate. 

### `#️⃣CSS`
The `📁css` folder should contain one main file to style the entire theme. This file name is called `#️⃣styles.css`.

>The name of this file __will not be changed__ and we will not add any other css files here unless they are modules or extensions. If this file does not exist, you will need to create it. 

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

### `📄JS`
The `📁js` folder should contain one main javascript file for the entire theme. This file name is called `📄script.js`.

>The name of this file __will not be changed__ and we will not add any other js files here unless they are modules or extensions. If this file does not exist, you will need to create it. 

If you need to add other modules on the site that require a `📄.js` file, add them here.
For example, if you would like to add [jquery.fancybox](https://fancyapps.com/), add this `📄.js` file in this folder.

``` html
└── 📁 css
    └── 📄 script.js                   <!-- main js file. do not change name. -->
    └── 📄 jquery.fancybox.min.js      <!-- fancybox js file -->
```

Be sure to call it in your `🟧foot.htm` partial as well. 

``` twig
...
<script src="{{ 'assets/js/jquery.fancybox.min.js'|theme }}>
...
```

### `🖼️IMG`
The `📁img` folder should contain all of the images associated with the theme.

> This should not contain images that can be dynamically generated. More specifically, this folder should contain images that are being rendered in each partial, and page.

Example of the image file structure

``` html
└── 📁 img
    └── 🖼️ logo.png
    └── 🖼️ hero.jpg
```
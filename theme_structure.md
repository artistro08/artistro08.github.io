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

Below is a detailed explanation on what files each folder will have and how each folder will be structured.


## Partials

`🟧partials` are chunks of global, reusable code that is used throughout the theme.

The `📁partials` folder should contain four main files that will be used across the theme. Those files are `🟧head.htm`, `🟧header.htm` `🟧foot.htm` and `🟧footer.htm`. If they do not exist, you will need to create them.

Here's an example of the folder structure below. 

``` html
└── 📁 partials
    ├── 🟧 head.htm                <!-- head code for pages. do not change name. -->
    ├── 🟧 header.htm              <!-- navigation code for pages. do not change name. -->
    ├── 🟧 foot.htm                <!-- foot code for pages (before closing </body> tag). do not change name. -->
    └── 🟧 footer.htm              <!-- footer code for pages. do not change name. -->
```

The name of these files __will not be changed__ and we will not add any other partials here unless they meet the following requirements:

 - The `partial` is going to be a global component (e.g. custom alerts.)
 - The `partial` will be used across the entire website.

If the partial does not meet any of these requirements, they need to be implemented per page and must be included in a folder. The folder name should be related to the function of the partial.

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



## Assets

The `assets` folder is where we will store all of our `#️⃣css`, `📄js`, and `🖼️img` files. These folders will style the website and create the theme so it's imperative that we keep them small and easy to navigate. 

### `CSS`
The `css` folder should contain one main file to style the entire theme. This file name is called `#️⃣styles.css`.

The name of this file __will not be changed__ and we will not add any other css files here unless they are modules or extensions. If this file does not exist, you will need to create it. 

If you need to add other modules on the site that require a `#️⃣.css` file, add them here.
For example, if you would like to add [jquery.fancybox](https://fancyapps.com/), add this `#️⃣.css` file in this folder.

``` html
└── 📁 css
    └── #️⃣ styles.css                   <!-- main css file. do not change name. -->
    └── #️⃣ jquery.fancybox.min.css      <!-- fancybox css file -->
```

Be sure to call it in your `head.htm` partial as well. 

``` twig
...
<link rel="stylesheet" href="{{ 'assets/css/jquery.fancybox.min.css'| theme }}>
...
```
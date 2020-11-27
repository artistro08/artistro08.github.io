# Code of Conduct

This page is documentation on how naming conventions and coding structure should work out. Refer to each section for information on everything.
> This documentations uses case styling. Read more about them here: 
> - [Case Styles](https://medium.com/better-programming/string-case-styles-camel-pascal-snake-and-kebab-case-981407998841)

## HTML

### Classes
The naming conventions for classes in HTML have to make sense to the component/div you're designing. For example `class="hero"` should __ONLY__ target the `hero` div and other divs like it. Creating a combo class for `hero` on other pages works as well. for example `class="hero about-hero"`. 

> All classes will have kebab style casings. (e.g. hero-title)


### IDs 
ID attribues (e.g. `id="hero"`) should only be added if the selected div will be used in javascript or are apart of a module/component. Typically, component markups contain these and should stay in place unless you intend to replicate that functionality differently in the `📄script.js` file. 

> All IDs will have camelCase style casings. (e.g. `toggleButton`)

## CSS
CSS styles in the the file should be structured as per the standard. example below: 

``` css
.hero {
    display: flex;
    justify-content: center;
    text-align: center;
    /* more styles */
}

.hero .about-hero {
    /* extra styles here */
}

#component {
    /* more styles */
}
```

> It is encouraged, but not required that you leave comments in the css file for quick references in the code editor. 


## Components

Components are pieces of code that create the structure of plugins. These reside in the `📁 plugins/*author*/*plugin_name*/components` folder (replace things in the asterisks accordingly) and can be copied into the `📁 partials` folder to change the structure. Each component has it's own folder and a `default.htm` file. 



Example of the folder structure below:

``` html
└── 📁 partials                      
    └── 📁 pluginName <!-- camelCase styling -->
         └── 🟧default.htm 
```

### Rendering

Each component will have an alias attached to the file. Example below:

``` twig
{# component attached to a page #}

title = "Home"
url = "/"
layout = "default"

[blog blogPosts]
```

 
All components should be singular in reference unless they contain multiple entities. All components that are extended need their own folder.

> Components folders will be named in the camelCase format. (e.g. `blog` & `blogPost`).


> `📁 component` folders will __not__ contain the plugin name unless there is nothing else you can name it. For example, if you have a Blog plugin, it would make sense to name the components `blog` and `blogPost` but if you have a plugin named Records, you should name the component to the function that it is providing. (e.g. `team` or `sponsors`). 

### Attaching

When attaching components to `🟧pages`, `🟧partials`, or `🟧layouts`, you need to make sure of the following:

 - The component will be used directly and frequently wherever it is placed. For example, a component for SEO will go where the `🟧head.htm` partial is but not on the `🟧default.htm` layout because it is not being directly used there. 
 - The component needs to be placed on a specific `🟧page`, `🟧partial`, or `🟧layout` because of how it works. For example, you have a SEO plugin you need to attach to the `🟧head.htm` partial, but it only works on the `🟧default.htm` layout. Check your plugin's documentation on where it needs to be. 


 ### Next Steps

 Now that you're up to speed on the Code of Conduct, you should be good to go to start theming! Be sure to check out the Resources page too for documentation on plugins we always use. 

 [Resources :fas fa-arrow-right:](resources.md)
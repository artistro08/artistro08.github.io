# Code of Conduct

When coding in OctoberCMS (Specifically creating themes), you have to follow this structure:
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
    |     ├── 🟧 default.htm          <!-- main layout file. do not change name. -->
    |     └── 🟧 page.htm             <!-- main layout file for pages. do not change name. -->
    ├── 📁 pages
    |     └── 🟧 page_name.htm        <!-- main layout file for pages. do not change name. -->
    └── 📁 partials
          ├── 🟧 head.htm             <!-- head code for pages. do not change name. -->
          ├── 🟧 header.htm           <!-- navigation code for pages. do not change name. -->
          ├── 🟧 foot.htm             <!-- foot code for pages (before closing </body> tag). do not change name. -->
          └── 🟧 footer.htm           <!-- footer for pages. do not change name. -->
```
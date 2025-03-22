
!!! warning ":construction: Under Construction :construction:"

    This section is still under construction. Facts, information, and data in here may not be complete or accurate yet. 


# How to Add Custom Fonts to a New Django Web Dev Project

This is a general guide to how to add custom fonts to a new Django web dev project. This will cover a few different methods and include a few resources for fonts used at Dunosis.


## Method 1: Google Fonts (Easiest!)

The first method to add new and custom fonts to a website is by using free Google fonts and their CDN. Let's dive in!

Googlefonts.com has tons of free fonts with licensing to use in projects. Once you select one or multiple fonts or font-families, use the side bar and copy the code to add to your project. 

![Google Fonts](./assets/custom-fonts/new-repo1.jpeg)

Within your project directory, add the code to the head of the HTML body. It should look something like this: 

``` html
    code
```

!!! note
    you may need to close and reopen your development server and hard-reload (click and hold refresh button in Chrome or command+shift+R on mac) your browser to reset the cache in order to see the new font load in


## Method 2: Custom Font Files

While google fonts is great, their library is limited or you may find some other fonts on other platforms. In this case follow these steps for using custom font files in the django project: 

1. Download and manage font files

    This can be in many formats and ideally you want the same font type in multiple formats to ensure maximum compatiblity. here are a few font types you can expect:

    - .tff
    - .woff
    - .woff2
    - .eot

    Usually, it's a good idea to install these fonts onto your machine to view them in any other program as well (Photoshop, Affinity, Figma, etc) by following your regular font installation instructions depending on your OS. 

    !!! warning "Be Mindful of Licensing"
        Often times, fonts have licensing that needs to be managed or bought. Use free or open licensed fonts to avoid any copyright issues

    Move the font files into the project directory using this file structure: 

    templates > assets > fonts

    ```plaintext
    📂 Project_Repo
    ├── templates
    │   ├── assets
    │   │   ├── fonts
    │   │   ├── images
    │   │   ├── json
    │   │   ├── logos
    │   ├── html
    │   ├── css
    │   ├── js
    ```

2. Add to CSS

    Add and define the font types in the index.css file

    ``` css
        @font-face {
            font-family: "Noir Pro";
            src: url("../fonts/NoirPro-Regular.eot");
            src: url("../fonts/NoirPro-Regular.eot?#iefix") format("embedded-opentype"),
                url("../fonts/NoirPro-Regular.woff2") format("woff2"),
                url("../fonts/NoirPro-Regular.woff") format("woff"),
                url("../fonts/NoirPro-Regular.ttf") format("truetype");
            font-weight: normal;
            font-style: normal;
        }
    ```

3. Add font to Tailwind configs (OPTIONAL)

    This is very usefule to use tailwind properties to assign fonts especially if the project is manageing multiple fonts in different sections. 

    First add the font to the **tailwind.config.js** file

    ``` js
        theme: {
            extend: {
                fontFamily: {
                    custom: ["Noir Pro", "sans-serif"],
                },
                colors: {
                    "bg-primary": "#f5f5f5",
                    "du-red": "#C62A2C",
                    "du-green": "#029A4D",
                    "du-blue": "#4D40f0",
                    "du-yellow": "#ECB731",
                    "du-purple": "#68008A",
                },
            },
        },
    ```

    !!! info
        This may be only applicable with Tailwindcss 3.X. With new 4.0 version, the confiurations are changing. Currently, projects and templates for Dunosis use older version but is in the process of migrating to newer version. Documentation will be updated accordingly

    Once defined in tailwind configurations, you can apply font types in HTML like this: 

    ``` html
        <p class="tw-font-property-name"> Hello World </p>
    ```
    
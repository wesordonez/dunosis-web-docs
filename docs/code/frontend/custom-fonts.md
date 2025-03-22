
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



# How to Add Custom Fonts to a New Django Web Dev Project

This guide covers how to add custom fonts to a Django-based web development project. We’ll look at a few different methods, with examples and notes based on best practices at Dunosis.

---

## Method 1: Google Fonts (Easiest!)

The easiest way to add fonts is to use the **free Google Fonts CDN**.

Go to **[Google Fonts](https://fonts.google.com/)** and select one or more fonts you'd like to use. Once selected, Google will generate a snippet of code for you to embed.

📸 Example from Google Fonts:  
![Google Fonts](./assets/custom-fonts/du-docs-custom-fonts-1.png)
![Google Fonts](./assets/custom-fonts/du-docs-custom-fonts-2.png)

### ✅ Steps:

1. Copy the `<link>` tag from the Google Fonts sidebar.

2. Paste it into the `<head>` of your base HTML template file:

    ```html
    <!-- base.html or main.html -->
    <head>
        ...
        <link rel="preconnect" href="https://fonts.googleapis.com">
        <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
        <link href="https://fonts.googleapis.com/css2?family=Roboto:ital,wght@0,100..900;1,100..900&display=swap" rel="stylesheet">
        ...
    </head>
    ```

3. Then reference it in your CSS:

    ```css
    body {
        font-family: "Inter", sans-serif;
    }
    ```
    Or define a new class for that specific font:

    ```css
    .new-font-name {
        font-family: "Inter", sans-serif;
    }
    ```

!!! note
    If fonts don’t show up, try **restarting your development server** and doing a **hard refresh** in the browser:

    - Chrome: Hold `Shift` and click the Reload button  
    - Mac: `Cmd + Shift + R`

---

## Method 2: Using Local Custom Font Files

If your desired fonts aren't available via Google Fonts, you can host and use **custom font files** directly.

### 1. Download & Manage Font Files

Fonts often come in several file formats for compatibility:

- `.ttf` (TrueType Font)  
- `.woff` / `.woff2` (Web Open Font Format)  
- `.svg` (Scalable Vector Graphics Font)  
- `.otf` (OpenType Font)  
- `.pfa` / `.pfb` (PostScript Fonts)  
- `.dfont` (Mac OS X Data Fork Font)  
- `.bdf` / `.pcf` (Bitmap Distribution Format / Portable Compiled Format)  
- `.ps` (Type 1 PostScript Fonts)  
- `.webfont` (Generic Web Font Format)

!!! tip
    It's also a good idea to install the fonts on your local machine for use in apps like Figma, Photoshop, etc.

!!! warning "Be Mindful of Licensing"
    Only use fonts with open or commercial-use licenses. Many custom fonts require purchasing or permission for use in web projects.

---

### 2. Add Fonts to Your Project Directory

Organize font files under your static or template directory, like this:

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

---

### 3. Reference Fonts in Your CSS

In your CSS file (e.g., `index.css`, `styles.css`), declare the font using `@font-face`:

```css
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

Then use it like any other font:

```css
body {
    font-family: "Noir Pro", sans-serif;
}
```

---

### 4. (Optional) Add Font to Tailwind Config

If you’re using **TailwindCSS**, you can define your custom font in the `tailwind.config.js`:

```js
// tailwind.config.js
theme: {
  extend: {
    fontFamily: {
      custom-font-name: ["Noir Pro", "sans-serif"],
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

!!! info "Tailwind Version Notes"
    This guide assumes usage of TailwindCSS 3.x. Tailwind 4.0 introduces major changes in config and file structure.  
    Dunosis templates are currently based on v3 but are in the process of migrating. Updates will be reflected in future documentation.

You can now use the custom font in your HTML:

```html
<p class="font-custom-font-name">Hello World</p>
```

---

## 📚 Resources

- [Google Fonts](https://fonts.google.com/)
- [Font Squirrel (Free fonts)](https://www.fontsquirrel.com/)
- [TailwindCSS Docs](https://tailwindcss.com/docs/font-family)
- [AI Font Pairing](https://fontjoy.com)
- [Collaborative Digital Type Foundry](http://www.losttype.com/)
- [Icons as Fonts](https://fontawesome.com/v5/cheatsheet)
- [Archive of Free Fonts](https://www.dafont.com/)

---

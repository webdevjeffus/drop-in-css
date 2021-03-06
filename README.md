# Drop-In CSS
#### A drop-in CSS stylesheet to instantly style any web app MVP

![Drop-In CSS](https://github.com/webdevjeffus/drop-in-css/blob/master/img/readme_splash.png "Style your app in 60 seconds!")

## UPDATE - DECEMBER 5, 2016 - v2.1 AVAILABLE!

A new version of **drop-in.css** is now available from this repository. This 2.0 version refines and improves **drop-in** over v1.0, and is intended to be fully-compatible with that version. Testing will be conducted in the next few days to confirm that the new version doesn't break pages designed with the previous version, which remains available in the CSS folder in this repo, as **drop-in-1-0.css**.

#### Drop-in.css v2 offers the following new or updated features:
- Greater consistency and efficiency of CSS rule-sets throughout the stylesheet
- Upgrade linked **normalize.css** to current version, 5.0.0.
- Add styling for nav list in footer
- Add new theme "Whiteboard" as css/drop-in-wb.css (previews images and documentation to come)
- All themes now updated to drop-in.css v2.1!
- Compatible with [**griddy.css**](https://github.com/webdevjeffus/griddy), my own super-light responsive grid system.

#### Still to come
- Docs in this repo have not been updated for v2.0 yet, though the use and functionality of **drop-in.css** has not changed

### GRIDDY compatibility in testing!
**drop-in.css** has a companion project&mdash;[**griddy.css**](https://github.com/webdevjeffus/griddy), a very lightweight, simple-to-apply responsive grid system. **drop-in.css** is a pre-made CSS3 stylesheet that can be linked to any unstyled web page or app to instantly apply attractive styling sufficient at the very least for MVP purposes. **griddy.css** provides a concise set of CSS classes that allow a dev to quickly turn a non-responsive page or app into a fully responsive one. The two projects started separately, but I am now almost finished revising them both so that they can also be used together.

Because the two stylesheets apply their styling differently&mdash;**drop-in** uses HTML tags as selectors, while **griddy** uses classes&mdash;they can be used together with very little massaging. **drop-in** provides the "design" of the page&mdash;colors and fonts, along with a very basic, non-responsive layout&mdash;while **griddy** is responsible for the responsiveness. To make this work, you just need to link in both stylesheets in the &lt;head&gt; of your html document, **drop-in** first, **griddy** next, and your own application.css last.

I am currently overhauling my own web dev portfolio site using **drop-in** and **griddy** together. Once that is done, and any lingering bugs or conflicts have been found and squashed, I'll update the docs in both repos to detail the procedure for using the two stylesheets in conjunction with one another.

<hr>

# Documentation for drop-in.css v1.0

## Features
- **Drop-in.css** instantly styles any semantic HTML5 document, without the addition of classes or styles
    - Apply **drop-in.css** by inserting one link to the remotely-hosted stylesheet
    - Or serve the stylesheet as part of your own site by copy-pasting one CSS file
- **Drop-in.css** automatically imports the resources it needs, including:
    - [normalize.css](https://necolas.github.io/normalize.css/)
    - Web fonts from [Google Fonts](https://www.google.com/fonts)
- Choose from a variety of [**drop-in** themes](https://github.com/webdevjeffus/drop-in-css/blob/master/docs/themes.md), or easily create your own
- No dependencies! **drop-in.css** works with vanilla HTML5/CSS3&mdash;no preprocessing required!
- All **drop-in.css** stylesheets are validated as CSS3 using the [WC3 CSS Validation Service](https://jigsaw.w3.org/css-validator/)
<br />
<img style="border:0;width:88px;height:31px" src="http://jigsaw.w3.org/css-validator/images/vcss" alt="Valid CSS!" />

## TLDR
This page offers full instructions on how to use **drop-in.css** in your app; the [**Drop-in.css**, line by line](https://github.com/webdevjeffus/drop-in-css/blob/master/docs/tutorial.md), not surprisingly, breaks down the entire **drop-in.css** stylesheet rule by rule and declaration by declaration. If you are in a hurry, you can skip down to the ["Dropping it in"](#dropping-it-in) section and follow the instructions there to link **drop-in.css** into your app in just a few minutes. If your HTML code is clean and follows best practices for semantic HTML5, the pre-generated files will work fine. If you have any trouble, refer back to the instructions on this page to troubleshoot.

## Contents
### On this page...
- [TLDR](#tldr)
- [Introduction](#introduction)
- [Basic semantic HTML5](#basic-semantic-html5)
- [The Drop-In stylesheet](#the-drop-in-stylesheet)
- [Dropping it in](#dropping-it-in)
- [Licenses](#licenses)

### Elsewhere in this repo...
- [CSS Specificity and **drop-in.css**](https://github.com/webdevjeffus/drop-in-css/blob/master/docs/specificity.md)
- [**Drop-in.css**, line by line](https://github.com/webdevjeffus/drop-in-css/blob/master/docs/tutorial.md)
- [Themes for **drop-in.css**](https://github.com/webdevjeffus/drop-in-css/blob/master/docs/themes.md)
- Contribute to the Drop-In CSS project&mdash;coming soon.

## Introduction
The **drop-in.css** project offers web developers a ready-made CSS stylesheet that can be dropped in on any web app at the beginning of the development process, instantly applying a "good-enough" set of styling rules that make the app easier to look at and use, without adding any classes, ids, divs, or other non-semantic elements. For some development projects, **drop-in.css** may be all the styling you ever need; for others, you may ultimately add to it or replace it with custom stylesheets. But in either case, the **drop-in.css** stylesheet will carry the project through the early phases of development, while the basic features and functionality of the app are being implemented.

#### What is the Drop-In stylesheet for?
The original purpose for the **drop-in.css** stylesheet is to provide new web apps "good-enough" styling during the early phases of their development, so the developers can concentrate on implementing app's database, models, and functionality without having to spend thinking time on CSS. It is designed to handle the most commonly-encountered HTML code in typical web apps, regardless of the framework being used to create them.

Once the app is at a point that it requires custom styling, the developers have a decision to make. They can either repeal-and-replace the **drop-in.css** stylesheet with a custom stylesheet created by their own front-end devs, or use **drop-in.css** as the foundation for further, customized styling. Since **drop-in.css** relies entirely upon HTML elements as selectors, it will not interfere with styling rules that use classes or id's as selectors. Frameworks like Bootstrap and Foundation, which use class-based selectors, will easily override the rules in **drop-in.css** whenever conflicts arise.

#### DIY, or Pret-a-Porter?
This repo can be used in two ways. Front-end developers who are so inclined can follow the [**Drop-in.css**, line by line](https://github.com/webdevjeffus/drop-in-css/blob/master/docs/tutorial.md) document to build their own reusable stylesheet following **drop-in.css** principles, and use it as the foundation for styling their app. Full-stack or back-end developers, on the other hand, may wish to simply download and install the ready-to-go **drop-in.css**, to use with their existing HTML template, or with one of the provided view files.

#### Origin of the Drop-In CSS project
This project was originally prepared as a tutorial to support a "lightning-talk" presentation on quickly styling MVP web apps, to be presented to the Phase 2 students at [Dev Bootcamp NYC](http://devbootcamp.com/). The original incarnation of this repo, which was aimed specifically at Ruby/Sinatra and Ruby/Rails apps, can still be found at my [CSS for Sinatra](https://github.com/webdevjeffus/css-for-sinatra) repo, though as of March 18, 2016, it will no longer be updated. All future development on the Drop-In project will occur in this repo.


## Basic semantic HTML5
The **drop-in.css** stylesheet is able to instantly style almost any HTML document without the addition of any id's, classes, divs, or other special code. It does this by using HTML element tags to build its CSS selectors. In order for this to work, it relies upon you to write clean, semantic HTML5 code&mdash;which is fine, 'cause you're doing it already anyway, right?

#### Semantic tags
The **drop-in.css** stylesheet expects that your HTML is organized semantically, using HTML5 tags including \<header>, \<nav>, \<main>, \<footer>, \<section>, \<article> and \<aside>. The general structure it expects is something like this:

```html
<body>
  <header>
    <h1>APP NAME</h1>
    <nav>
      <!-- Nav links organized as an unordered list -->
    </nav>
  </header>

  <main>
    <section>
      <!-- First section content - Full-page width -->
    </section>
    <section>
      <article>
        <!-- Second section article content - wide column on left side -->
      </article>
      <aside>
        <!-- Second section sidebar content - narrow column on right side -->
      </aside>
    </section>
  </main>

  <footer>
    <!-- Footer content -->
  </footer>
</body>
```

If you follow this structure, the **drop-in.css** stylesheet will be able to tell the difference between, for example, an \<h1> heading in the \<header> element&mdash;which will be styled as a logo for the site&mdash;and an \<h1> in the \<main> element, which will appear as a prominent headline. Similarly, it will also know to display text in \<p> elements in the \<footer> at a smaller size than \<p> text in the \<main> section.

#### Under the hood
For more information about how **drop-in.css** uses the rules and conventions of CSS to select and style the elements in your HTML document, refer to the [CSS Specificity and _drop-in.css_](https://github.com/webdevjeffus/drop-in-css/blob/master/docs/specificity.md) page in the **drop-in.css** documentation.


## The Drop-In stylesheet
The **drop-in.css** stylesheet is organized into five major groups of CSS rules. The first two groups&mdash;Import Commands, Utility Styles and Design Styles&mdash;apply to the whole page, while the latter three&mdash;Header Styles, Main Styles, and Footer Styles&mdash;each contain the rules that apply within their related element in the DOM tree. On this page, I'll briefly introduce each of these five groups, and explain generally how they display your HTML document. For a detailed, rule-by-rule breakdown of the entire **drop-in.css** file, refer to [Drop-in.css, line by line](https://github.com/webdevjeffus/drop-in-css/blob/master/docs/tutorial.md).

### Import Commands
These @import commands bring in other css resources needed by **drop-in.css**. The first loads a minimized version of normalize.css from cdnjs.com, so you don't have to store it on your app's server. Since **drop-in.css** relies upon **normalize.css**, if you remove this command, you'll need to include normalize.css from another source.

The second import command loads the fonts used by **drop-in.css** from Google Fonts. You can change the fonts in your app by replacing this link with a link to another pair of Google Font faces; if you do that, you'll also need to change the "font-family" rules in the [Design Styles](#design-styles) section.

### Utility Styles
**Drop-in.css** relies upon [**normalize.css**](https://necolas.github.io/normalize.css/) to eliminate inconsistencies in how different browsers render certain HTML elements by default, and adds a few more general-purpose rules of its own. It is recommended that you include **normalize.css** in your project along with **drop-in.css**; download the **normalize.css** file, and link it in the \<head> element of your HTML file, just before the link to **drop-in.css**.

In its Utility Styles section, **drop-in.css** includes a few style rules that simplify various browsers' default element-rendering, to make styling more designer-friendly. Specifically, these rules:
* Use box-sizing: border-box on all block elements.
* Assign min- and max-widths to be the body, and set the margins to center the body in the browser window.
* Resets the margins and padding for all elements to zero, so that we can set our own margins and paddings to the exact values we want.
* Adds 0.5rem of margin to the bottom of all headings ( \<h1> to \<h6> ), as well as paragraphs ( \<p> ).

### Design Styles
In its Design Styles section, **drop-in.css** collects all the rules that specify the font and colors used throughout the site. By keeping these rules together, near the top of the file, **drop-in.css** makes it easy for developers to change the look and feel of their app by making minor changes to just a few CSS rules.

#### Fonts
**Drop-in.css** relies upon [Google Fonts](https://www.google.com/fonts) to serve its fonts, which are imported by the second @import command in the [Import Commands](#import-commands) section, above. **Drop-in** uses only two fonts&mdash;a simple, highly legible font for general text, and a fancier display font for major headers, including the app title/logo. By default, **drop-in.css** uses Open Sans as its general text font, and Alegreya as its display font. These fonts are declared in the first two rules in the Design Styles section of **drop-in.css**, and nowhere else, so they are easy to replace.

#### Colors
By default, **drop-in.css** uses several shades of gray for background and font colors, and two highly-contrasting red shades for inactive and active links. This color scheme was chosen for maximum contrast and readability, but it may be a bit bold for some projects. If you want to use a different set of colors, change out the colors assigned in this section, following the comments for each color declaration&mdash;or just go to the [Themes for **drop-in.css**](https://github.com/webdevjeffus/drop-in-css/blob/master/docs/themes.md) library and pick out an existing theme that strikes your fancy.

### Header Styles
The section of **drop-in.css** that styles the app's header will give you a logo in the form of the app's name in the site's display font, in very large type, at the left edge of the header section. The nav element will display as a horizontal series of links, separated by vertical bars, at the right edge of the header. In your HTML file, follow these guidelines to be certain everything displays properly:
* Create the logo by putting the name of the app in an \<h1> element; this should be the first element in the \<header>.
* Inside the nav element, mark-up your links as list elements ( \<li> ) in an unordered list ( \<ul> ).
* If you have a subhead under the \<h1>, mark it up as a \<p> element, and wrap the \<h1> and the \<p> inside a \<div> to properly position the \<p>. The \<div> lets **drop-in.css** style the logo \<h1> and the subhead \<p> to be floated left together. Refer to the snippets below for logos with and without a subhead. (As shown in the examples, if you don't have a subhead, you don't need the \<div> around the \<h1>.)

```html
<!-- LOGO WITHOUT A SUBHEAD: No <div> required -->
<body>
  <header>
    <h1>Appmazing!</h1>
    <nav>
      <ul>
        ...

<!-- LOGO WITH A SUBHEAD: Wrap them together in a <div> element -->
<body>
  <header>
    <div>
      <h1>Appmazing!</h1>
      <p>The Amazingest App Ever!</p>
    </div>
    <nav>
      <ul>
        ...
```

### Main Styles
Because the \<main> element is where the real action in your app is displayed, _where_ you put your HTML code for \<main> can get a bit complex, depending on what back-end framework you're using. **Drop-in.css** originally evolved while I was working on Ruby/Sinatra and Ruby on Rails projects at Dev Bootcamp, so the \<main> element in my layout.erb (or layout.html.erb, for Rails) often contained nothing more than a simple \<%= yield %> method; the actual layout of the pages would be determined by erb templates in my views folder or folders. In such cases, the use of semantic HTML tags within the \<main> element, including \<section>, \<article>, and \<element>, would often happen in those templates. No matter where the mark-up happens, though, **drop-in.css** will display it all correctly, so long as semantic HTML5 best practices are followed in structuring your pages.

#### Semantic HTML in the \<main> element: \<section>, \<article>, and \<aside>
**Drop-in.css** will handle some fairly complex structuring of content using the HTML5 semantic elements \<section>, \<article>, and \<aside>. Here are guidelines on how **drop-in.css** treats these elements:

* **\<article>** elements will take up 65% of the available width, and be floated to the left margin.
* **\<aside>** elements will take up 30% of the available width, and be floated to the right. Thus, using an \<article> element alongside an \<aside> element will produce the main-column/sidebar format so familiar on the internet.
* To help distinguish between main-column and sidebar content, all text within an **\<aside>** will be displayed at 80% of its normal font-size; this affects all sizes of headers, as well as paragraphs. Also, \<aside> content will appear within a box with a distinctive background color.
* **\<section>** elements will take up 100% of the available width. A horizontal rule (automatically created by drop-in.css as a border&mdash;no \<hr> element required) will separate one section from the next.
* **\<section>** elements can be used to sub-divide content in the \<main> element, within \<article> elements, and even within \<aside> elements.
* _**Final note:** Don't use **\<section>**, **\<article>**, or **\<aside>** elements if you don't **need** them!_
    * Use **\<section>** elements only if your content has multiple distinct sections which need to be separated semantically and visually. If you only have one section, you don't need \<section> tags.
    * Never use an **\<article>** element without a matching **\<aside>**, and vice versa. **drop-in.css** uses these elements to set up a main-column-and-sidebar layout; using one without the other just wastes space.

#### Lists
Unordered lists are very common in web apps. **Drop-in.css** displays unordered lists within the \<main> element with the list items indented 1rem from the left margin, without bullets.

#### Forms
Forms are even more common in web apps than are lists. **Drop-in.css** styles forms in a generic way that emphasizes readability over compactness; you will probably want to restyle your forms with classes once you are past the MVP stage. Here is how **drop-in.css** handles form elements by default:
* Most **\<input>** elements&mdash;including text, email, url, password, and many more&mdash;will take 100% of the available width, as will **\<textarea>** elements.
* **\<label>** elements are displayed on their own lines. If you put a \<label> in the HTML immediately before the \<input> element it labels, it will appear on the line right above the \<input>.
* **Buttons** will be 12rem wide and centered, whether they are created as \<button> elements, or \<input type="submit">. (If the text on your buttons doesn't fit in 12rem, go into **drop-in.css** and make the buttons wider.)
* **Checkboxes** and **radio buttons** display inline; that is to say, if your HTML calls for three radio buttons in sequence, all three buttons will appear (with their labels) on the same line. Use \<div> elements to separate checkboxes and radio buttons that should go on different lines, or to group ones that should appear on the same line. Refer to the code snippet below for examples:

```html
<!-- These radio buttons will display on a single line: -->
<div>
  <label for="grape">Grape</label>
  <input type="radio" name="flavor" id="grape" value="grape">
  <label for="strawberry">Strawberry</label>
  <input type="radio" name="flavor" id="strawberry" value="strawberry">
  <label for="plum">Plum</label>
  <input type="radio" name="flavor" id="plum" value="plum">
</div>

<!-- These checkboxes will display on separate lines: -->
<div>
  <label for="condiment">Ketchup</label>
  <input type="checkbox" name="condiment" value="ketchup">
</div>
<div>
  <label for="condiment">Mustard</label>
  <input type="checkbox" name="condiment" value="mustard">
</div>
<div>
  <label for="condiment">Mayonnaise</label>
  <input type="checkbox" name="condiment" value="mayo">
</div>
```

#### Tables
Tables should only be used to display data that is best understood in table form&mdash;don't use tables for page layout purposes. Tables in **drop-in.css** display with a lighter background color than the \<main> background-color. Table borders match the \<main> font color. Text in each cell of a table is centered.

By default, tables take up 100% of the available width. That width will be divided among the columns proportionally, based on the length of the longest entry in each column.

### Footer Styles
All text in the footer will be centered, and displayed at 80% of the size it would appear in the \<main> element. You can use heading elements (\<h1>, \<h2>, etc.) as well as paragraphs; they will be scaled down to 80% of their regular size as well.

## Dropping it in
There are two ways to apply the **drop-in.css** stylesheet to your web app&mdash;you can link to the minified stylesheet hosted online, or you can save a copy of the stylesheet to your app's repo, and serve it as part of your own site. The first method is easier&mdash;you only need to add one link to your HTML file&mdash;but some devs may feel that copying and hosting the file themselves is safer or more flexible.

### Linking to the minified stylesheet<br>_NOTE: Linked, minified stylesheets not yet updated to drop-in.css v2.1_
To apply the **drop-in.css** stylesheet with a single link, simply copy and paste the link below into the \<head> element of your HTML file, _before_ the link to any custom stylesheets you've created for the app. The minified stylesheet still loads **normalize.css** and the necessary fonts from Google automatically.

```html
<link rel="stylesheet" href="http://www.webdevjeffus.com/drop-in-css/drop-in.min.css">
```

If you prefer the look of one of the **drop-in** themes to the default **drop-in** styling, you'll find direct links for minified stylesheets for all available themes on the [Themes for **drop-in.css**](https://github.com/webdevjeffus/drop-in-css/blob/master/docs/themes.md) page in this repo.

### Serving the stylesheet yourself
To host your own copy of the **drop-in** stylesheet and serve it along with your web app or site, just save a copy of the **drop-in.css** file in the proper folder in your app's folder structure, and link to it in the \<head> element of your HTML document. Which folder is the "proper folder" will depend upon how you've organized the resources that make up your website. Here's a very simple example:

```
SAMPLE FOLDER ORGANIZATION

appmazing
  |
  +-- css/
  |     |
  |     +-- drop-in.css
  |     |
  |     +-- application.css (or main.css, or styles.css, or whatever...)
  |
  +-- img/
  |
  +-- js/
  |
  +-- index.html
```

In this sample app, the css files are stored in a **css/** folder, which is in the root directory for the app, along with **index.html**. In this case, the link you'd need to load the **drop-in.css** stylesheet would be:

```html
<link rel="stylesheet" href="css/drop-in.css">
```

If or when you begin to add custom style rules to your app using classes and id's, you'll want to put those rules in a separate stylesheet. You can call this stylesheet anything you like&mdash;application.css, main.css, and styles.css are all common choices. But whatever you call it, be sure to put the link to your custom stylesheet _after_ the link to **drop-in.css**, to help ensure that your custom rules override the rules in **drop-in**. (There is a lot more on this topic in [CSS Specificity and **drop-in.css**](https://github.com/webdevjeffus/drop-in-css/blob/master/docs/specificity.md).) Together, the links would look like this:

```html
<head>
  <link rel="stylesheet" href="css/drop-in.css">
  <link rel="stylesheet" href="css/application.css">
    ...

</head>
```

<hr>

#### Licenses

The documentation in this repo is Copyright &copy; 2016 by Jeff George.

<a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/"><img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by-nc-sa/4.0/88x31.png" /></a><br /><span xmlns:dct="http://purl.org/dc/terms/" property="dct:title">Documentation for <b>Drop-In CSS</b></span> by
<a href="http://webdevjeff.us">Jeff George</a> is licensed under a <a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/">Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License</a>.

The code files in this repo, including **drop-in.css**, all **drop-in.css** themes, and all view files, may be used under the terms of the [MIT License](https://opensource.org/licenses/MIT).


# Drop-In CSS
#### A drop-in CSS stylesheet to instantly style any web app MVP

![Drop-In CSS](https://github.com/webdevjeffus/drop-in-css/blob/master/img/readme_splash.png "Style your app in 60 seconds!")

## Contents
### On this page...
- [Introduction](#introduction)
- [TLDR](#tldr)
- [Basic semantic HTML5](#basic-semantic-html5)
- [The Drop-In stylesheet](#the-drop-in-stylesheet)
- [Linking it all up](#linking-it-all-up)
- [Licenses](#licenses)

### Elsewhere in this repo...
- [CSS Specificity and **drop-in.css**](https://github.com/webdevjeffus/drop-in-css/blob/master/docs/specificity.md)
* [**Drop-in.css**, line by line](https://github.com/webdevjeffus/drop-in-css/blob/master/docs/tutorial.md)
* [Themes for **drop-in.css**](https://github.com/webdevjeffus/drop-in-css/blob/master/docs/themes.md)
* Contribute to the Drop-In CSS project&mdash;coming soon.

## Introduction
The **drop-in.css** project offers web developers a ready-made CSS stylesheet that can be dropped in on any web app at the beginning of the development process, instantly applying a "good-enough" set of styling rules that make the app easier to look at and use, without adding any classes, ids, divs, or other non-semantic elements. For some development projects, **drop-in.css** may be all the styling you ever need; for others, you may ultimately add to it or replace it with custom stylesheets. But in either case, the **drop-in.css** stylesheet will carry the project through the early phases of development, while the basic features and functionality of the app are being implemented.

#### What is the Drop-In stylesheet for?
The original purpose for the **drop-in.css** stylesheet is to provide new web apps "good-enough" styling during the early phases of their development, so the developers can concentrate on implementing app's database, models, and functionality without having to spend thinking time on CSS. It is designed to handle the most commonly-encountered HTML code in typical web apps, regardless of the framework being used to create them.

Once the app is at a point that it requires custom styling, the developers have a decision to make. They can either repeal-and-replace the **drop-in.css** stylesheet with a custom stylesheet created by their own front-end devs, or use **drop-in.css** as the foundation for further, customized styling. Since **drop-in.css** relies entirely upon HTML elements as selectors, it will not interfere with styling rules that use classes or id's as selectors. Frameworks like Bootstrap and Foundation, which use class-based selectors, will easily override the rules in **drop-in.css** whenever conflicts arise.

#### DIY, or Pret-a-Porter?
This repo can be used in two ways. Front-end developers who are so inclined can follow the tutorial to build their own reusable stylesheet following **drop-in.css** principles, and use it as the foundation for styling their app. Full-stack or back-end developers, on the other hand, may wish to simply download and install the ready-to-go **drop-in.css**, to use with their existing HTML template, or with the provided **layout.html** file.

#### Origin of the Drop-In CSS project
This project was originally prepared as a tutorial to support a "lightning-talk" presentation on quickly styling MVP web apps, to be presented to the Phase 2 students at [Dev Bootcamp NYC](http://devbootcamp.com/). The original incarnation of this repo, which was aimed specifically at Ruby/Sinatra and Ruby/Rails apps, can still be found at my [CSS for Sinatra](https://github.com/webdevjeffus/css-for-sinatra) repo, though as of March 18, 2016, it will no longer be updated. All future development on the Drop-In project will occur in this repo.

## TLDR
This page offers full instructions on how to use **drop-in.css** in your app; the [DIY tutorial](https://github.com/webdevjeffus/drop-in-css/blob/master/docs/tutorial.md) breaks down the entire **drop-in.css** stylesheet line by line. If you are in a hurry, you can skip down to the ["Linking it all up"](#Linking-it-all-up) section and follow the instructions there to link **drop-in.css** into your app in just a few minutes. If your HTML code is clean and follows best practices for semantic HTML5, the pre-generated files will work fine. If you have any trouble, refer back to the instructions on this page to troubleshoot.


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
The **drop-in.css** stylesheet is organized into five major groups of CSS rules. The first two groups&mdash;Utility Styles and Design Styles&mdash;apply to the whole page, while the latter three&mdash;Header Styles, Main Styles, and Footer Styles&mdash;each contain the rules that apply within their related element in the DOM tree. On this page, I'll briefly introduce each of these five groups, and explain generally how they display your HTML document. For a detailed, rule-by-rule breakdown of the entire **drop-in.css** file, refer to [Drop-in.css, line by line](https://github.com/webdevjeffus/drop-in-css/blob/master/docs/tutorial.md).

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
**Drop-in.css** relies upon [Google Fonts](https://www.google.com/fonts) to serve its fonts. It uses only two fonts&mdash;a simple, highly legible font for general text, and a fancier display font for major headers, including the app title/logo. By default, **drop-in.css** uses Open Sans as its general text font, and Alegreya as its display font. These fonts are declared in the first two rules in the Design Styles section of **drop-in.css**, and nowhere else, so they are easy to replace.

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

## Linking it all up
Just like any stylesheet, you'll need to \<link> to **drop-in.css** in the \<head> of your HTML file in order for the browser to apply the stylesheet when displaying your app. You'll also need to include the link to Google Fonts **drop-in** needs to serve its fonts.

### Folder organization
The HTML templates provided with **drop-in.css** expect assets to be stored in folders within the root directory, sorted by type (html, css, js, img, etc.). This is almost certainly _not_ the way you will need or want to organize the assets in your app repository. You'll need to adjust the paths described in the links to find the appropriate files within your folder structure.

### Font link
If you are satisfied with fonts **drop-in.css** uses by default, just copy the following link into the \<head> of your HTML file:

```html
<link href='https://fonts.googleapis.com/css?family=Alegreya:700|Open+Sans:400,700,400italic,700italic' rel='stylesheet' type='text/css'>
```

If you want to change the fonts in your app, navigate to [Google Fonts](https://www.google.com/fonts) and follow the instructions there to create the link to copy-paste into your app. You'll need to pick two fonts&mdash;an easy-to-read font as a default font, which will be used for paragraphs, buttons, links, and minor headings, and a display font, which will be used for major headings, including the app logo in the header. The best combination for clarity and readability is usually a sans-serif font for general text, and a complimentary display or serif font for major headings. Be sure to include normal, bold, italic and bold italic versions of the general font, but you'll only need one version of the display font (usually bold, if the font comes in different weights). Adding more versions will only slow down your load times, and they are not needed by **drop-in.css**.

Since the **drop-in.css** stylesheet refers to the fonts in the link to Google Fonts, be sure to put the Google Font link _before_ the **drop-in** link in the \<head> of your HTML document.

### Stylesheet links
You'll need to include three stylesheet links in your document's \<head>, in this order: **normalize.css**, **drop-in.css**, and **application.css** (or whatever you've named the file that holds your custom styles for the app). The links will look _something_ like this, although you will probably need to change the paths to suit your folder structure:

```html
<link rel="stylesheet" href="../css/normalize.css">
<link rel="stylesheet" href="../css/drop-in.css">
<link rel="stylesheet" href="../css/application.css">
```

**drop-in.css** will not display properly without **normalize.css** (which you should be using anyway, even without **drop-in**). The **css/** folder in this repo includes a copy of normalize.css v4.0.0, which is the latest version available as of March, 2016. For the very latest verstion, go to [**normalize.css**](https://necolas.github.io/normalize.css/).

Try not to make changes to **drop-in.css**, and if you must, try to use HTML tags as CSS selectors. If you've found a problem or a bug in **drop-in.css** please make a pull request to this repo, so that it can be fixed for all users. Changes to **drop-in.css** that require classes or id's as selectors will be rejected.

If you need to add or change CSS styling to meet specific needs in your app, make the changes by adding CSS rules to the custom **application.css** file for the project. If you use class- or id-based selectors in the CSS rules in your application stylesheet, you can be confident that they will override the tag-selected rules in **drop-in.css** and **normalize.css**.

<hr>

#### Licenses

The documentation in this repo is Copyright &copy; 2016 by Jeff George.

<a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/"><img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by-nc-sa/4.0/88x31.png" /></a><br /><span xmlns:dct="http://purl.org/dc/terms/" property="dct:title">Documentation for <b>Drop-In CSS</b></span> by
<a href="http://webdevjeff.us">Jeff George</a> is licensed under a <a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/">Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License</a>.

The code files in this repo, including **drop-in.css**, all **drop-in.css** themes, and all view files, may be used under the terms of the [MIT License](https://opensource.org/licenses/MIT).


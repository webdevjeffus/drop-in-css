# <i>CURRENTLY REVISING THIS REPO - 3/22/16</i>

# Drop-In CSS
#### A drop-in CSS stylesheet to instantly style any web app MVP

## Contents
### On this page...
- [Introduction](#introduction)
- [TLDR](#tldr)
- [Basic semantic HTML5](#basic-semantic-html5)
- [The Drop-In stylesheet](#the-drop-in-stylesheet)
- Linking it up

### Elsewhere in this repo...
* [DIY: Create your own drop-in.css stylesheet](https://github.com/webdevjeffus/drop-in-css/blob/master/docs/tutorial.md)
* Drop-In CSS themes
* Contribute to the Drop-In CSS project

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
This page provides in-depth coverage of what **drop-in.css** does, how it does it, and why; the [DIY tutorial](https://github.com/webdevjeffus/drop-in-css/blob/master/docs/tutorial.md) breaks down the entire **drop-in.css** file line by line. If you are in a hurry, you can skip down to the ["Linking it up"](#Linking-it-up) section and follow the instructions there to link pre-generated .css and .html files into your app in just a few minutes. The pre-generated files will work fine, but you won't learn as much doing it that way. Your call.


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
    </section>
  </main>

  <footer>
    <!-- Footer content -->
  </footer>
</body>
```

If you follow this structure, the **drop-in.css** stylesheet will be able to tell the difference between, for example, an \<h1> heading in the \<header> element&mdash;which will be styled as a logo for the site&mdash;and an \<h1> in the \<main> element, which will appear as a prominent headline. Similarly, it will also know to display text in \<p> elements in the \<footer> at a smaller size than \<p> text in the \<main> section.

#### CSS Specificity
The magic happens because CSS lets you build selectors using multiple tags to create increasingly specific rules. CSS's principle of _specifity_ states that a rule with a _more specific_ selector always overrides a rule with a _less specific_ one. Simply put, the more tags named in a CSS selector, the more specific it is. A rule with two tags in its selector will override a rule built with only one tag, and a rule with three tags in its selector will trump them both. Here are some examples:

```css
/* CSS Rules Examples */

/* Rule 1 */
p { color: black; }

/* Rule 2 */
main p { color: blue; }

/* Rule 3 */
main aside p { color: green }

/* Rule 4 */
footer p { font-size: 75% }
```

Using these style rules, paragraph text (the text within \<p> tags) throughout the document will be displayed as black, following Rule 1, with its one-tag selector, "p". Rule 2, with the selector "main p", overrides that first rule, changing all paragraphs in the \<main> element to display with blue text. Rule 3, "main aside p", trumps Rule 2 for any paragraph that is in a sidebar within the main element, making those paragraphs red. Rule 4, "footer p", applies only paragraph text within the footer section. They will appear as the default color for \<p> elements (black) because they are _not_ inside the \<main> element, but this rule sets them to be 25% smaller than the page's default font size.

Let's consider what happens when we apply the styling rules in the CSS example above to the HTML code below:

```html
<!-- HTML Document Example -->

<body>
  <main>
    <h1>This is the main heading!</h1>
    <p>This paragraph "A". It will be blue.</p><!-- Rule 2 applies -->

    <section>
      <article>
        <h2>This is an article heading</h2>
        <p>This is paragraph "B". It will also be blue.</p><!-- Rule 2 applies -->
      </article>
      <aside>
        <h2>This is the sidebar heading</h2>
        <p>This is paragraph "C". It will be red.</p><!-- Rule 3 applies -->
      </aside>
    </section>
  </main>

  <p>This is paragraph "D". It will be black.</p><!-- Rule 1 applies -->

  <footer>
    <p>This is paragraph "E". It will be black, but smaller.</p><!-- Rule 4 applies -->
  </footer>
</body>
```

Paragraphs A and B would both print as blue text&mdash;they are both \<p> elements within the \<main> element (Rule 2). Paragraph C would display as green text (Rule 3); C _is_ a \<p> element within the \<main> (Rule 2), but it's also a \<p> inside an \<aside> inside the \<main>. Since Rule 3 is more specific than Rule 2 (three tags in the selector, as opposed to just two), it is the one that wins. Paragraph D prints as black text, according to Rule 1&mdash;it's a \<p> element that isn't a descendant of anything but the body, so only Rule 1 applies to it. Finally, paragraph E shows up as black text at 3/4 the size of the other \<p> elements, since it's a \<p> inside the \<footer>, and therefore subject to Rule 4.

#### Descendants vs. Direct Children
Note that when more than one tag is included in a CSS selector, and the tag names are separated by **blank spaces**, the browser understands that each element is a descendant of the element to its left. That is to say, in the selector "main p", we are selecting _all_ \<p> elements found _anywhere within_ the \<main> element. If the tags in the selector were separated by a **greater than** character, as in "main**&gt;**p", the \<p> element would have to be a _direct child_ of the \<main> element&mdash;further down the DOM tree wouldn't qualify. If we changed the selector for Rule 2 from "main p" to "main&gt;p", then it would only apply to paragraph A, which is a direct child of the \<main> element; paragraph B&mdash;merely a descendant of \<main>, and not a _direct_ child&mdash;would be styled by Rule 1, and would appear as black text. Paragraph C would still print as red text, since the selector for Rule 3&mdash;"main aside p"&mdash;is still more specific than Rule 1, which is the only other rule which might apply.

Note that at the present time, to assure maximum flexibility, the **drop-in.css** stylesheet does not use direct-child selectors.

## The Drop-In stylesheet
The drop-in.css stylesheet is organized into five main sections. The first two sections&mdash;Resets and Design Styles&mdash;apply to the whole page, while the latter three&mdash;Header Styles, Main Styles, and Footer Styles&mdash;each contain the rules that apply within their related element in the DOM tree. On this page, I'll briefly introduce each of these five sections, and explain generally how they display your HTML document; for a detailed, rule-by-rule breakdown, refer to the [tutorial](https://github.com/webdevjeffus/drop-in-css/blob/master/docs/tutorial.md).

### Resets
Resets standardize the rendering of HTML elements by different browsers. **Drop-in.css** relies upon [**normalize.css**](https://necolas.github.io/normalize.css/) for general consistency, and adds a few more reset rules of its own. It is recommended that you include **normalize.css** in your project along with **drop-in.css**; download the **normalize.css** file, and link it in the \<head> element of your HTML file, just before the link to **drop-in.css**.

In its own Resets section, **drop-in.css** includes a few style rules that simplify various browsers' default element-rendering, to make styling more designer-friendly:
* Use box-sizing: border-box on all block elements.
* Assign min- and max-widths to be the body, and set the margins to center the body in the browser window.
* Remove margins and padding from all elements, then set a standard bottom margin of 0.5rem to all header and paragraph elements.

### Design Styles
In its Design Styles section, **drop-in.css** collects all the rules that specify the font and colors used throughout the site. By keeping these rules together, near the top of the file, **drop-in.css** makes it easy for developers to change the look and feel of their app by making minor changes to just a few CSS rules.

#### Fonts
**Drop-in.css** relies upon [Google Fonts](https://www.google.com/fonts) to serve its fonts. It uses only two fonts&mdash;a simple, highly legible font for general text, and a fancier display font for major headers, including the app title/logo. By default, **drop-in.css** uses Open Sans as its general text font, and Alegreya as its display font. These fonts are declared in the first two rules in the Design Styles section of **drop-in.css**, and nowhere else, so they are easy to replace.

#### Colors
By default, **drop-in.css** uses several shades of gray for background and font colors, and two highly-contrasting red shades for inactive and active links. This color scheme was chosen for maximum contrast and readability, but it may be a bit bold for some projects. If you want to use a different set of colors, change out the colors assigned in this section, following the comments for each color declaration.

### Header Styles
The section of **drop-in.css** that styles the app's header will give you a logo in the form of the app's name in the site's display font, in very large type, at the left edge of the header section. The nav element will display as a horizontal series of links, separated by vertical bars, at the right edge of the header. In your HTML file, follow these guidelines to be certain everything displays properly:
* Create the logo by putting the name of the app in an \<h1> element; this should be the first element in the \<header>.
* Inside the nav element, mark-up your links as list elements ( \<li> ) in an unordered list ( \<ul> ).
* If you have a subhead under the \<h1>, mark it up as a \<p> element, and wrap the \<h1> and the \<p> inside a \<div> to properly position the \<p>. (If you don't have a subhead, you don't need the \<div> around the \<h1>.)

### Main Styles
Because the \<main> element is where the real action in your app is displayed, _where_ you put your HTML code for \<main> can get a bit complex, depending on what back-end framework you're using. I developed the **drop-in.css** while working on Ruby/Sinatra and Ruby on Rails projects, so the \<main> element in my layout.erb (or layout.html.erb, for Rails) often contained a simple \<%= yield %> method; the actual layout of the pages would be determined by erb templates in my views folder or folders. In such cases, the use of semantic HTML tags within the \<main> element, including \<section>, \<article>, and \<element>, would often happen in those templates. No matter where the mark-up happens, though, **drop-in.css** will display it all correctly, so long as semantic HTML5 best practices are followed in structuring your pages.

#### Semantic HTML in the \<main> element: \<section>, \<article>, and \<aside>
**Drop-in.css** will handle some fairly complex structuring of content using the HTML5 semantic elements \<section>, \<article>, and \<aside>. Here are guidelines on how **drop-in.css** treats these elements:

* **\<article>** elements will take up 65% of the available width, and be floated to the left margin.
* **\<aside>** elements will take up 30% of the available width, and be floated to the right. Thus, using an \<article> element along with an \<aside> element will produce the main-column/sidebar format so familiar on the internet.
* To help distinguish between main and sidebar content, all text within an **\<aside>** will be displayed at 80% of its normal font-size; this affects all sizes of headers, as well as paragraphs. Also, \<aside> content will appear within a box with a distinctive background color.
* **\<section>** elements will take up 100% of the available width. A horizontal rule (automatically created by drop-in.css as a border&mdash;no \<hr> element required) will separate one section from the next.
* **\<section>** elements can be used to sub-divide content in the \<main> element, within \<article> elements, and even within \<aside> elements.

#### Lists
Unordered lists are very common in web apps. **Drop-in.css** displays unordered lists flush left, without bullets.

#### Forms
Forms are even more common in web apps than are lists. **Drop-in.css** styles forms in a generic way that emphasizes readability over compactness; you will probably want to restyle your forms with classes once you are past the MVP stage. Here is how *drop-in.css** handles form elements by default:
* Most **\<input>** elements&mdash;including text, email, url, password, and many more&mdash;will take 100% of the available width, as will **\<textarea>** elements.
* **\<label>** elements are displayed on their own lines. If you put a \<label> in the HTML immediately before the \<input> element it labels, it will appear on the line right before the \<input>.
* **Checkboxes** and **radio buttons** display inline; that is to say, if your HTML calls for have three radio buttons in a row, all three buttons will appear (with their labels) on the same line. Use \<div> elements to separate checkboxes and radio buttons that should go on different lines, or to group ones that should appear on the same line.
* **Buttons** will be 12rem wide and centered, whether they are created as \<button> elements, or \<input type="submit">.

#### Tables
Tables should only be used to display data that is best understood in table form&mdash;don't use tables for page layout purposes. Tables in **drop-in.css** display with a lighter background color than the \<main> background-color. Table borders match the \<main> font color. Text in each cell of a table is centered.

By default, tables take up 100% of the available width. That width will be divided among the columns proportionally, based on the length of the longest entry in each column.

### Footer Styles
All text in the footer will be centered, and displayed at 80% of the size it would appear in the \<main> element. You can use heading elements (\<h1>, \<h2>, etc.) as well as paragraphs; they will be scaled down to 80% of their regular size as well.


<hr>
#_Text not updated beyond this point - 3/22/16_

## Setting up your HTML file
For this to work, you need to set up your **layout.erb** (or **layout.html.erb**, in Rails) following some basic best-practices for semantic HTML. We'll be relying on HTML semantics to differentiate between tags of the same type in different areas of the page. For example, our stylesheet will handle an **\<h1>** tag differently if it appears in the app's **\<header>** element than if it is in the **\<main>**.

To begin, set up the **\<body>** element in your **layout.erb** as in this example. We'll cover the contents of [the **\<head>** element](#the-html-head-element) later in the tutorial.

```html
<!DOCTYPE html>
<html lang="en">

<head>
  <!-- Discussed in "The HTML <head> element", below -->
</head>

<body>
  <header>
    <h1><a href="/">APP NAME</a></h1>
    <nav>
      <ul>
        <li><a href="#">LINK 1</a></li>
        <li><a href="#">LINK 2</a></li>
      </ul>
    </nav>
  </header>

  <main>
    <%= yield %>
  </main>

  <footer>
    <p>FOOTER TEXT</p>
  </footer>
</body>
</html>
```

The "yield," wrapped in a printing erb tag, will tell Sinatra (or Rails) to render each view inside the **\<main>** element; you don't need to do anything else to this section. The **\<footer>** tag is even less complex&mdash;just drop your own footer text into the **\<p>** element.

The **\<header>** element has a bit more going on, but it's easy enough to understand. First is the **\<h1>** element that will serve as the logo for your MVP version. The **\<a>** link to the root route will make the logo a link back to the home page from any place in your app, so be sure you've defined the root among the routes in your controllers.

We'll set up the header so that the logo displays at the left edge, and the nav links appear lined up on the right. To make this happen, we'll put the links inside list items (**\<li>**), which are included in a single unordered list (**\<ul>**). The list is held within a semantic **\<nav>** element, so we can select it easily for styling.

Again, we'll loop back around and cover [the **\<head>** element](#the-html-head-element) of your **layout.erb** file after we've talked about the contents of the CSS file.



## The HTML Head element

At the beginning of this tutorial, I showed you how to set up the **\<body>** element of your **layout.erb** file, so that you could use semantic HTML tags as CSS selectors to style the page as intended. In this section, we double back and create the **\<head>** element, with the appropriate stylesheet links so that everything works properly. Here is the content for the **\<head>** element:

```html
<!DOCTYPE html>
<html lang="en">
<head>

  <link href='https://fonts.googleapis.com/css?family=Bangers|Open+Sans:400,700,400italic,700italic' rel='stylesheet' type='text/css'>

  <link rel="stylesheet" href="/css/normalize.css">
  <link rel="stylesheet" href="/css/drop-in.css">
  <link rel="stylesheet" href="/css/application.css">

  <script src="//ajax.googleapis.com/ajax/libs/jquery/1.9.1/jquery.min.js"></script>
  <script src="/js/application.js"></script>

  <title>APP NAME</title>
</head>
```

Our **\<head>** element includes four **\<link>** tags that are essential to the styling of the app, and they need to be included in the order shown to make sure they work properly.

#### Font link
The first link makes a call to [Google's free webfont service](https://www.google.com/fonts), to load our preferred fonts for the app. The link in the example uses Bangers&mdash;a brash, all-caps display font&mdash;for the headlines, and Open Sans&mdash;a clean, simple sans-serif font&mdash;for everything else, including paragraph text. If you decide to change the fonts, just go to Google fonts and select an attractive pair of typefaces; you just need one version of the display font used for headers, but you'll want to select four versions&mdash;normal, italic, bold, and bold italic&mdash;of the body font. Once you've made your choices, Google will provide you with the text for a single link that serves them all up, which you can copy and paste into your **\<head>** element. Be sure to delete the default Google fonts link, if you're changing the font choices.

#### Stylesheet links
You're probably going to need three CSS stylesheets. The first of these is **normalize.css**, which smooths out the differences in how various browsers render web pages; download and include [the latest version of **normalize**](https://necolas.github.io/normalize.css/).

The next link calls the Sinatra-styling CSS file you created in this tutorial, **drop-in.css**. The final stylesheet you should link in is **application.css**, which includes any style rules you've created specifically for the app you're working on. This is where you'd put any rules you needed to handle special cases in this particular app, most likely using classes as CSS selectors. As a general rule of thumb, if you needed a class to style an element, put it in **application.css**; if you used HTML tags as selectors, it goes in your version of **drop-in.css**.

#### Scripts
The **\<head>** element is also where you link to your Javascript libraries and files. In this example, we call for a recent version of **jQuery**, served by Google's CDN (content delivery network), as well as **application.js**, which includes any specific JavaScript you've written for this app.

#### Title
The text you enter into the **\<title>** element appears on the browser tab that holds your app. Entering your app name here is a subtle but impressive touch, and shows attention to detail.

## Putting it in place
Once you have created your drop-in CSS-for-Sinatra stylesheet, you'll want to use it. First I'll explain how to drop it in on an existing, unstyled app, then I'll talk about how to use it from the beginning with a new app. Although I'm assuming you're creating a Sinatra app, using the stylesheet for MVP styling on a Rails or other app won't be much different.

### Adding the stylesheet to an existing Sinatra app
First, you'll need to save your stylesheet to the folder in the app where you keep your stylesheets; in an app based on the Dev-Bootcamp-style Sinatra skeleton, that folder is **/public/css**. Then you simply add a link to the stylesheet in your app's **layout.erb** file (**layout.html.erb** for a Rails app). The link should come _after_ the link to **normalize.css**, but _before_ the link to the app-specific stylesheet, if there is one. You'll also need to insert the Google Fonts link _before_ all the stylesheet links.

Once you've saved drop-in.css in the right folder, and added the necessary links to your **layout** file, fire up your server and open the app in the browser, and marvel at the instant styling goodness!

### Starting from scratch
If you're using this drop-in stylesheet from the beginning of your development process, you'll begin by saving **drop-in.css**, along with the current version of **normalize.css**, in the appropriate folder in your app repo. Again, for a DBC-style Sinatra app, that's **/public/css**.

Then you'll want to replace the contents of the **layout.erb** file with the **\<body>** and **\<head>** elements shown in the examples, above. Alternately, you can use the **layout.erb** file included in this repo. The **layout** file in this repo assumes you're implementing user authentication and sessions, and includes the HTML for sign-up, login, logout, and user profile links in the nav bar. If you're not using user authentication, just replace the code inside the **\<nav>** element with simple navigation links, as in the code snippet in the example on this page, above.

In the **\<head>** element, be sure you've included a Google Font link to serve your chosen fonts, and stylesheet links to **normalize.css** and your version of **drop-in.css**.

<hr>

#### Licenses

This tutorial is Copyright &copy; 2016 by Jeff George.

<a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/"><img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by-nc-sa/4.0/88x31.png" /></a><br /><span xmlns:dct="http://purl.org/dc/terms/" href="http://purl.org/dc/dcmitype/Text" property="dct:title" rel="dct:type">Drop-In CSS for Sinatra Tutorial</span> by <a xmlns:cc="http://creativecommons.org/ns#" href="webdevjeffus.github.io/css-for-sinatra" property="cc:attributionName" rel="cc:attributionURL">Jeff George</a> is licensed under a <a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/">Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License</a>.

The other files in this repo, **drop-in.css** and **layout.erb**, may be used under the terms of the [MIT License](https://opensource.org/licenses/MIT).

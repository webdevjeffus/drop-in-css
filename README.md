# <i>CURRENTLY EDITING THIS FILE - 3/18/16</i>

# Drop-In CSS
#### A drop-in CSS stylesheet to instantly style any web app MVP

## Contents
### On this page...
* [Introduction to the Drop-In CSS project](#introduction-to-the-drop-in-css-project)
* [TL;DR](#tl;dr)
* [Basic semantic HTML5](#basic-semantic-html5)
* Linking it up

### Elsewhere in this repo...
* [DIY: Create your own drop-in.css stylesheet](https://github.com/webdevjeffus/drop-in-css/blob/master/docs/tutorial.md)
* Drop-In CSS themes
* Contribute to the Drop-In CSS project

## Introduction to the Drop-In CSS project
The **drop-in.css** project offers web developers a ready-made CSS stylesheet that can be dropped in on any web app at the beginning of the development process, instantly applying a "good-enough" set of styling rules that make the app easier to look at and use, without adding any classes, ids, divs, or other non-semantic elements. For some development projects, **drop-in.css** may be all the styling you ever need; for others, you may ultimately add to it or replace it with custom stylesheets. But in either case, the **drop-in.css** stylesheet will carry the project through the early phases of development, while the basic features and functionality of the app are being implemented.

#### What is the Drop-In stylesheet for?
The original purpose for the **drop-in.css** stylesheet is to provide new web apps "good-enough" styling during the early phases of their development, so the developers can concentrate on implementing app's database, models, and functionality without having to spend thinking time on CSS. It is designed to handle the most commonly-encountered HTML code in typical web apps, regardless of the framework being used to create them.

Once the app is at a point that it requires custom styling, the developers have a decision to make. They can either repeal-and-replace the **drop-in.css** stylesheet with a custom stylesheet created by their own front-end devs, or use **drop-in.css** as the foundation for further, customized styling. Since **drop-in.css** relies entirely upon HTML elements as selectors, it will not interfere with styling rules that use classes or id's as selectors. Frameworks like Bootstrap and Foundation, which use class-based selectors, will easily override the rules in **drop-in.css** whenever conflicts arise.

#### DIY, or Pret-a-Porter?
This repo can be used in two ways. Front-end developers who are so inclined can follow the tutorial to build their own reusable stylesheet following **drop-in.css** principles, and use it as the foundation for styling their app. Full-stack or back-end developers, on the other hand, may wish to simply download and install the ready-to-go **drop-in.css**, to use with their existing HTML template, or with the provided **layout.html** file.

#### Origin of the Drop-In CSS project
This project was originally prepared as a tutorial to support a "lightning-talk" presentation on quickly styling MVP web apps, to be presented to the Phase 2 students at [Dev Bootcamp NYC](http://devbootcamp.com/). The original incarnation of this repo, which was aimed specifically at Ruby/Sinatra and Ruby/Rails apps, can still be found at my [CSS for Sinatra](https://github.com/webdevjeffus/css-for-sinatra) repo, though as of March 18, 2016, it will no longer be updated. All future development on the Drop-In project will occur in this repo.

## TL;DR
This page provides in-depth coverage of what **drop-in.css** does, how it does it, and why; the [DIY tutorial](https://github.com/webdevjeffus/drop-in-css/blob/master/docs/tutorial.md) breaks down the entire **drop-in.css** file line by line. If you are in a hurry, you can skip down to the ["Linking it up"](#Linking-it-up) section and follow the instructions there to link pre-generated .css and .html files into your app in just a few minutes. The pre-generated files will work fine, but you won't learn as much doing it that way. Your call.


## Basic semantic HTML5
The **drop-in.css** stylesheet is able to instantly style almost any HTML document without the addition of any id's, classes, divs, or other special code. It does this by using HTML element tags to build its CSS selectors. In order for this to work, it relies upon you to write clean, semantic HTML5 code&mdash;which is fine, 'cause you're doing it already anyway, right?

#### Semantic tags
The **drop-in.css** stylesheet expects that your HTML is organized semantically, using HTML5 tags including \<header>, \<nav>, \<main>, \footer>, \<section>, \<article> and \<aside>. The general structure it expects is something like this:

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

If you follow this structure, the **drop-in.css** stylesheet will be able to tell the difference between, for example, an \<h1> heading in the \<header> element&mdash;which will be styled as a logo for the site&mdash;and an \<h1> in the \<main> element, which will appear as a prominent headline. It will also know to display text in \<p> elements in the \<footer> at a smaller size than \<p> text in the \<main> section.

#### CSS Specifity
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



<hr>
#_Text not updated beyond this point - 3/18/16_

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

## Creating the CSS file
In this tutorial, we'll actually be employing _three_ CSS files: **normalize.css** (more on this in [the **\<head>** element](#the-html-head-element), below); **application.css** (where you'll put any specific styling for this particular app; again, more in the **\<head>** session); and this type-based stylesheet, which I'll call **drop-in.css**.

I'll begin by creating and saving a new **drop-in.css** file, and setting up some commented-out section heads to help organize it. Here's how it looks at first:

```css
/* drop-in.css */

/* RESETS */

/* DESIGN STYLES  */

/* HEADER STYLES */

/* MAIN STYLES - Yield Block */

/* FOOTER STYLES */

```

### Resets
In this section, we'll add style rules that simplify various browsers' default element-rendering, to make styling more designer-friendly. This includes setting the document to size all block elements, including the header, main, footer and any divs, using **border-box** sizing, instead of the frustrating default, **content-box**. We'll also set all **margins** and **padding** to 0, since different browsers use different defaults for these properties. When we want margins or padding, we'll add them explicitly, so we get what we're expecting.

```css
/* RESETS */

html { box-sizing: border-box; }

*, *:before, *:after {
  box-sizing: inherit;
  margin: 0;
  padding: 0;
}

body {
  margin: 0 auto;
  min-width: 600px;
  max-width: 800px;
}

h1, h2, h3, h4, h5, h6, p {
  margin-bottom: 0.5rem;
}

```

In the **body** rule, we first set the left and right **margin** to **auto**, so that the app content will be centered on the page. We'll also set **min-width** and **max-width** values to keep our page within a range in which our styling works. If you want a fully-responsive site, you'll need to add media queries&mdash;but that's a separate tutorial.

Finally, we'll add a bottom margin of 0.5rem to our headers and paragraphs, to put just a bit of vertical whitespace between elements on the page. (I'll talk more about rems in the ["Header Styles"](#header-styles) section, below.)


### Design Styles
Design styles apply throughout the website, across all pages and in all sections; they determine the look of the app. Here, we'll set our font choices, as well as the colors for everything in the site. Fonts and colors are all we need to change to completely alter the look from one project to the next. By pulling those rules together at the top of the file, we make it easy to make changes.

```css
/* DESIGN STYLES */

/* Fonts */

html { font-family: 'Open Sans', sans-serif; }

h1, h2, h3, h4 {
  font-family: 'Bangers', sans-serif;
}
```

#### Fonts
In the Fonts section, we'll be specifying two fonts&mdash;one display font and one body font&mdash;and we have only need two rules to assign them throughout the app. The first rule, declared for the **\<html>** element, assigns our body font (Open Sans, in this case) as the default font for the site. The only elements that will use the display font we've chosen (Bangers, for this app) are the larger heading elements: **\<h1>** down through **\<h4>**. Chances are we won't even need any headings smaller than **\<h4>**, and if we do, we'll just leave them as bold-face Open Sans.

We'll be using Google Fonts to serve our chosen fonts; we set that up in the **\<head>** element, which I'll cover below.

```css

/* Colors */

html {
  background-color: #888;   /* medium gray */
  color: #ddd;              /* dark gray */
}

body,
header nav input[type="submit"] {
  background-color: #222;    /* dark gray */
}

main {
  background-color: #ddd;   /* light gray */
  color: #222;              /* dark gray */
}
```

#### Colors
We're using a deliberately simple color scheme here&mdash;four shades of gray for our backgrounds and font colors, and two tones of red for links, which contrasts well with both light and dark shades of gray. Even so, there are several CSS rules that need to include color properties, so this section _looks_ kind of long. That's because I've moved _all_ the rules which specify color to this section, for ease of maintenance. This probably isn't how you'd set up a stylesheet for the production version, but it makes this drop-in stylesheet easier to customize.

The **html** and **body** rules set up the background-color and font color for the site. The **html** background is a medium shade that contrasts with both the dark color of the **header** and **footer**, and the light shade in the **main** element. The **body** rule assigns a near-black gray as the background, and a near-white gray as the font color. These colors will appear in everything _except_ the **\<main>** element, which is to say the **\<header>** and **\<footer>** elements. I've added the **header nav input[type="submit"]** selector to the **body** rule, since we will want the background color for the "Logout" button on our nav bar to match the surrounding header. More on the "Logout" button in the ["Header Styles"](#header-styles) section, below.

The **main** rule sets the light background and dark font color for the **\<main>** element, which includes everything _except_ the **header** and **footer** of the app.

```css
/* Colors, con't. */

a:link,
a:visited,
header nav input[type="submit"] {
  color: #c00;              /* darker contrasting color; inactive links */
  font-weight: bold;
  text-decoration: none;
}

a:hover,
a:active,
header nav input[type="submit"]:hover,
header nav input[type="submit"]:active {
  color: #f22;              /* brighter contrasting color; active links */
}

header nav li {
  border-left: 3px solid #888;    /* match html background-color */
}

main table,
main th,
main td {
  border: 1px solid #222;   /* border should match body background-color */
  background-color: #eee;   /* even lighter than main background-color */
}

```

The next two rules, which start with **a:link** and **a:hover**, style the links throughout the page. The first rule, for inactive links, assigns a rich, dark red which contrasts nicely with both the light and dark backgrounds in the site. This rule also sets link text to bold, with no underline; these properties are inherited by active links as well. The second link rule highlights active links a vivid red, which is noticeably brighter than the dark red of the inactive links. The other selectors in these rules, which include **input[type="submit"]**, style the "Logout" button to use the same colors as other links.

Since the logo **\<h1>** in the header is also a link, it will automatically be styled with the red link color, helping it grab the user's attention. If red is too bold a choice for your contrasting color, try two shades of turquoise, gold, blue, green, or even pink. Just be sure that both shades contrast well with both the light and dark shades in your background. Readability trumps aesthetics for an MVP.

The last rule in the "Colors" section assigns the colors for any tables that are included in the **\<main>** element. The table borders should be the same color as the **background-color** of the **body**; the background-color for the table elements should be a shade lighter than the **\<main>** background, so the table stands out on the page.

### Header Styles
In this section, we'll set up the rules for the elements in our **\<header>** section. It is here that we see the flexibility of our type-based CSS selectors coming into play.

```css
header { padding: 1rem; }

header h1 {
  font-size: 3rem;
  float: left;
}

header nav { float: right; }

header nav ul { list-style: none; }

header nav li {
  display: inline-block;
  padding-left: 1rem;
}

header nav li:first-child { border-left: 0;}

header nav input[type="submit"] {
  overflow: visible;
  text-align: center;
  font-weight: bold;
  width: auto;
  border: none;
}
```

#### header
The general **header** rule just puts 1rem of padding around all four sides of the header, to keep the text from banging against the edges. I prefer rems ("root ems") for most CSS measurements because they scale smoothly if you make the site responsive. By default, 1rem = 16 pixels; if you want to change that value, just set a **font-size** property to some value other than 16 pixels in the style for the root element, **\<html>**. If you later change the root em value, then every font-size or element dimension that is sized in rems will scale with the root em.

#### header h1
In the **header h1** rule, we specify that any and all **\<h1>** elements in the **\<header>** should be rendered at a size of 3rems. Our CSS selector for the rule, "header h1", won't touch **\<h1>**s in any other element of the app&mdash;for example, an **\<h1>** in the **\<main>** element will be displayed at its default size, not at the 3rems specified in this rule. We also set the **header h1** to **float: left**, so that it displays against the left margin of the header section.

#### header nav
The rest of the styles in the "Header Styles" section deal with the components of the header's **\<nav>** element. To be sure that we don't affect list or nav elements elsewhere in the app, we begin each selector with a mention of both the **\<header>** and the **\<nav>** types. The **header nav** rule, which specifies **float: right**, pushes the nav links to the right-hand margin of the header. The **header nav ul** rule eliminates the bullet points that appear by default on unordered lists.

In the **header nav li** rule, **display: inline-block;** changes the links in the nav bar to appear as a horizontal row, instead of a vertical list. The **border-left** property establishes a vertical border between each pair of links, and the **header nav li:first-child** rule _turns off_ that border for the first link on the nav bar.

#### header nav input[type="submit"]
The last rule in this section, which styles **header nav input[type="submit"]** elements, is necessary because HTML and Sinatra all but _require_ the "logout" link to be created as a button. Since ending the current session requires a POST route with a hidden input to carry the "delete" action, it is usually created as a single-button form, rather than as a simple link. This rule removes the border and background from the button, so that it looks and behaves like the other links in the nav bar; recall that we set the colors for this input in the "Colors" section, above.

**Performance Note:** A selector like this one, that depends on the value of an attribute of an html tag, is just about the slowest possible CSS selector. We use it here because we are deliberately trying _not_ to have to add classes to our html file; in the deployed version of an app, you'd be better off to use a class as a selector, even if it's only used that once.

### Main Styles
In **main** styles section, we see our type-based selectors really pay off: they let us write an unlimited number of pages, partials, and forms which look decent (maybe not great, but certainly decent) with absolutely zero time spent on styling. Again, I'll show you the basic CSS code first, then break it down rule by rule.

```css
/* MAIN STYLES - Yield Block */

main {
  padding: 1rem;
  clear: both;
}

/* Lists */

main ul { margin: 0 auto 1.5rem; }

main ul li {
  list-style: none;
  margin: 0.5rem 0 1rem;
  font-size: 1.25rem;
}
```

#### main
The padding in the **main** rule just pushes the text in from the edges of the **main** element a little bit; we use rems instead of pixels here so that the width of the padding scales automatically with the fonts. The **clear: both** property is necessary to clear out the floats we used in the header; again, this isn't how we'd do it in the production version of our app, but it works fine for this quick-and-dirty, drop-in stylesheet.

Headers, paragraphs and links in the **main** element use the defaults set in the "Resets" and "Design Styles," so we generally don't need to add anything for them here. If you decide to increase the size of your headers from the default&mdash;and you very well might&mdash;do that in the Resets section of the **drop-in.css** stylesheet.

#### Lists: main ul and main ul li

Almost every index view in a Sinatra or Rails app is going to display some sort of list of objects from the data base, but the default presentation of unordered lists is very 1994. To bring our stylesheet into the current century, we'll set **list-style** to **none**, to eliminate the bullets. The **margin** properties are necessary to get the list back into the right spot once we've taken out the bullets. I like to set the font-size for list items to 1.25rem, because these lists tend to be pretty important in our Sinatra apps, and we want them to be prominent.

```css
/* Main Styles, con't. */

/* Forms */

main input {
  display: block;
  margin-bottom: 0.75rem;
  width: 100%;
}

main input[type="text"],
main input[type="password"],
main input[type="email"] {
  padding: 0 0.5rem;
}

main textarea {
  width: 100%;
  height: 5rem;
  margin-bottom: 1rem;
  padding: 0.5rem;
}

main input[type="radio"],
main input[type="checkbox"] {
  display: inline;
  width: 1.5rem;
}

main input[type="submit"] { width: 12rem; }
```

#### Forms: main input and main textarea

Forms are also very common in Sinatra and Rails apps, but again, the default styling for them is generally pretty ugly and unfriendly. We'll handle this mostly by styling the form input elements.

First, we'll set the **display** property of **main input** elements to **block**, so each one appears on its own line on the page. If you add a label for an input, it will default to **display: inline**, so labels will show up to the left of the text box they identify. If you prefer labels on the line above, you can add the following style rule to your CSS file to put them there:

```css
main label { display: block; }
```

The margins and padding we set for **input** and **textarea** elements add a bit of whitespace to the form, while setting the **width** of each to **100%** makes each field wide enough to display most input data without annoying sideways scrolling. Remember that **\<input>** elements display only a single line of text. For this reason, you'll want to use a **\<textarea>** form element for any field where users will be entering more than a few words, such as a blog post or comment.

To make sure that radio buttons and checkboxes appear with their labels, we need to add a special rule for those inputs of those types. We'll set them to **display: inline**, with **width: 1.5rem**. (These lines essentially _undo_ for radio buttons and checkboxes the styling we applied to input elements in general a few lines above.)

The **main input[type="submit"]** rule sets **Submit** buttons to 12rem wide, which is wide enough to display the full text on the button in most cases. If you need more space, just up the rem value in this rule. Also, note that since we styled these buttons using **main** along with **input**, this rule does not effect the Submit button that we used to log out the user in the **header nav** element.


```css
/* Main Styles, con't. */

/* Tables */

main table {
  margin-bottom: 1rem;
  width: 100%;
}

main th,
main td {
  width: 25%;
  padding: 0.25rem 0;
  text-align: center;
}
```

### Tables
If your app displays complex user or game data, you'll probably want to show it in a table. The **main table** rule sets the table to fill the main element from side to side, and adds a margin at the bottom for whitespace between the table and the next element. The other rule, for **main th** and **td**, handles individual cells in the table. It sets each cell, and therefore each column, to 25% of the width of the table, creating a four-column table; if you need more or fewer columns, just change the percentage accordingly. The cells rule also adds a bit of top and bottom padding within the cell, and centers the text within the cell.

Remember that the background and border colors for tables were set in the "Colors" setion, above.

## Footer Styles

There's just one rule in our footer section:

```css
/* FOOTER STYLES */

footer {
  text-align: center;
  font-size: 0.8rem;
  padding: 1rem;
}
```

This rule is intended to style a single line of credits, something like: "Created by Jeff George for Dev Bootcamp Phase 2," or whatever. The rule centers the text, sets it to 80% of the default font size, and adds 1rem of padding to all sides of the footer. If you add **\<a>** tags to the footer text, to link to your Github or website, the stylesheet will apply the standard link color and styling to them, which should look fine if you chose your colors carefully at the top of the stylesheet.

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

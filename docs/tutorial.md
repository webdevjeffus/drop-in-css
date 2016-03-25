# _WORK IN PROGRESS - 3/25/19_
The content on this page is incomplete and under revision; links may be temporarily broken. Pardon the mess - I'll have it cleaned up soon. &mdash;_Jeff_
<hr>

# _Drop-in.css_, line by line

This document goes under the hood to explore the function of each section and rule in the **drop-in.css** stylesheet. It's aimed at front-end devs who want to deconstruct the **drop-in.css** file, to customize it or create their own version. You don't need to read it in order to use **drop-in.css** in your project.

## Organization of the _drop-in_ stylesheet

The default _drop-in.css_ is organized into six sections:

- [**Google Font Link:**](#google-font-link) a commented-out copy of the link to the fonts used by **drop-in.css**, served by **googleapis.com**, to be copy-pasted into the \<head> of the HTML document for the app.
- [**Utility Styles:**](#utility-styles) a catch-all category for rules that apply throughout the document.
- [**Design Styles:**](#design-styles) all the rules pertaining to fonts and colors are collected here.
- [**Header Styles:**](#header-styles) rules that style the header for the page, including the logo and nav links.
- [**Main Styles:**](#main-styles) rules that style the main content of the site, including sections, articles, asides, lists, forms and tables.
- [**Footer Styles:**](#footer-styles) rules that style the footer for the page.

We'll go through each section rule-by-rule.

### Google Font Link
The first section of the **drop-in.css** file contains a commented-out copy of the link to the fonts used by the stylesheet. The link is created by the Google Fonts website when you select a set of fonts for use in a website; this copy is saved here for convenience, to keep it handy when linking the **drop-in.css** stylesheet into a project. This entire section can be deleted from the CSS file without affecting the functionality of the stylesheet, once you're sure the font link is working properly.

Instructions for choosing fonts for use with **drop-in.css** are included in the [Design Styles](#design-styles) section of this document, below.

### Utility Styles
This section includes an assortment of rules that **drop-in.css** applies throughout your app to display it properly. For the most part, they use single-tag selectors; apart from that, they don't have anything to do with one another.

```css
/* UTILITY STYLES ************************************************************/

html { box-sizing: border-box; }

*, *:before, *:after {
  box-sizing: inherit;
  margin: 0;
  padding: 0;
}
```

These rules set all block elements to use **border-box** sizing, instead of the frustrating default, **content-box**. For a full explanation of why border-box rocks and content-box sucks, read this article at [CSS-Tricks](https://css-tricks.com/box-sizing/).

The "\*" rule also sets all **margins** and **padding** to 0, since different browsers use different defaults for these properties. When we want margins or padding, we'll add them explicitly, so we get what we're expecting.

```css
body {
  margin: 0 auto;
  min-width: 600px;
  max-width: 800px;
}
```

The body rule includes a margin declaration that causes the body of the app (which includes all the visible content) to be centered left-to-right in the browser window. The min- and max-widths are good values for an app in development; you'll want to override them with media queries when you're ready to make your site fully responsive to screens of all sizes.

```css
h1, h2, h3, h4, h5, h6, p { margin: 0 0 0.5rem; }

p:last-child { margin-bottom: 0rem; }
```

The first of these two rules removes the top, right and left margin set for headings and paragraphs in normalize.css. It sets the bottom margin to 0.5rem, so that there's a little whitespace between elements, and especially between paragraphs. The second rule (p:last-child) removes the bottom margin from a paragraph if it's the last element within the parent element (usually the \<main> element or a \<section>), since the padding of the outer element already handles adding whitespace after the last element.

```css
header:after,
main:after,
section:after {
  content: "";
  display: table;
  clear: both;
}
```

This rule automatically applies a "clearfix" immediately after \<header>, \<main> and \<section> elements, since these elements are likely to contain elements that are floated left or right. It has no effect if nothing inside the element is floated, but they don't hurt anything by being there.

### Design Styles


# _Everything above this line is REVISED as of 3/25/16_
<hr>
### Everything below this line is old text, cloned from my prior repo, CSS for Sinatra.

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

#### Licenses

The documentation in this repo is Copyright &copy; 2016 by Jeff George.

<a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/"><img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by-nc-sa/4.0/88x31.png" /></a><br /><span xmlns:dct="http://purl.org/dc/terms/" property="dct:title">Documentation for <b>Drop-In CSS</b></span> by
<a href="http://webdevjeff.us">Jeff George</a> is licensed under a <a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/">Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License</a>.

The code files in this repo, including **drop-in.css**, may be used under the terms of the [MIT License](https://opensource.org/licenses/MIT).

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
The rules in the Design Styles section determine the look of the app. It is here that we specify the fonts and the colors for the site. These are the _only_ CSS rules that are changed to create a new **drop-in** theme; they are collected here, rather than being split up among the Header, Main and Footer Styles sections, to make it more convenient and manageable to change the appearance of the app. If you are tinkering with the styles in **drop-in.css**, and you want to change a font or a color, you _must_ make those changes inside the Design Styles section, or subsequent users won't be able to find them.

#### Fonts
These two rules in the Fonts sub-section are the _only_ rules in the **drop-in.css** stylesheet that declare fonts. If you need to make additional font declarations, we recommend that you do that with class-selected rules in your **application.css** file.

```css
/* DESIGN STYLES *************************************************************/

/* Fonts */

html { font-family: 'Open Sans', sans-serif; }

h1, h2, h3, h4 { font-family: 'Alegreya', serif; }
```

The first rule here, with the selector "html", declares the font that will be used by default through out the site&mdash;in the default **drop-in** theme, I've chosen Open Sans, an easy-to-read font that was designed for screen viewing. The second rule declares the display font to be used for larger headings, including the \<h1> in the \<header> element that serves as the site logo. A carefully-selected display font goes a long way in establishing the "attitude" of the app, so you can afford to sacrifice a little bit of legibility for the sake of coolness.

It's not difficult to change the fonts used by **drop-in.css**. Just go to Google Fonts and pick two fonts that look good together. The general font should be an easily-read serif or sans-serif font; the display font can be a bit fancier. When choosing the font package for your site, select the normal, bold, italic, and bold italic versions of the general font, and the bold version of the display font. (Some display fonts are only available in a single version, which they call "normal"; if that's the case, use that version.) Once you have chosen your fonts, click the "Use" button at the lower right hand corner of the Google Fonts page, and the site will automagically generate the link you need to include in the head of your HTML document, as well as the proper "font-family" information to put into the font rules in the Design Styles section of **drop-in.css**.

#### Colors
The Colors sub-section of the Design Styles section is the _only_ place where colors are declared in **drop-in.css**. Again, if you need to make more specific rules for color styling, do so using classes, and save them in your **application.css** file.

```css
/* Colors */

html {
  background-color: #888;   /* medium background color, eg: 50% gray */
  color: #ddd;              /* light font color, eg: 15% gray */
}

body,
header nav input[type="submit"] {
  background-color: #222;    /* dark background color, eg: 85% gray */
}

main {
  background-color: #ddd;   /* light backround color, eg: 15% gray */
  color: #222;              /* dark font color, eg: 85% gray */
}
```

The first three Colors rules establish the basic color palette of the site:

In the "html" color rule, the "background-color" declaration sets the color that will appear in the right and left margins, outside the centered body of the app; in the default theme, this is a medium gray. The "color" declaration sets the font color that will be used within the \<header> and \<footer> elements; since the default theme uses a near-black gray for the header and footer, it uses a near-white gray for the font color in those areas.

The "body" rule specifies the background color that will be used in the header and footer. The "input[type='submit']" selector is there to set the background color of any buttons in the header or footer to match the background of those elements; this is part of the process of styling the Logout button&mdash;which must be a button, since it's a "delete" route&mdash;to _look like_ a regular link. (The rest of the CSS to accomplish this is found in the Header Styles section, below).

The "main" rule sets the "background-color" of the \<main> element to something that will contrast clearly with the background in the rest of the \<body> element (which is to say, the \<header> and the \<footer>). Since the header and footer are dark in the default theme, we've made the main content background a very light gray. The "color" declaration in the "main" rule sets the default font color throughout the main content of the site&mdash;in this case, we used the same near-black gray as the header and footer background color. We've deliberately chosen near-black text on a near-white background for everything that goes in the \<main> element, because this combination is less stressful to read than either light text on a dark background, or pure black text on a white background.

```css
a:link,
a:visited,
header nav input[type="submit"] {
  color: #c00;           /* darker contrasting color; inactive links */
  font-weight: bold;
  text-decoration: none;
}

a:hover,
a:active,
header nav input[type="submit"]:hover,
header nav input[type="submit"]:active {
  color: #f22;          /* brighter contrasting color; active links */
}
```

The next two rules, which start with "a:link" and "a:hover", set the colors for the links. The first rule sets the appearance of inactive links; in the default theme, they appear as bold type, without any underline ("text-decoration: none"), in a brick-red color. The second rule changes the color of the link text to a bright, fire-engine red when the mouse passes over them and when they are clicked. The "input[type='submit']" selectors are included to make the text on the Logout button behave like regular link text, another part of styling it to _not_ look like a button.

If the theme requires different colors for links in the \<main> element than elsewhere on the page, you will have to add separate rules (eg., "main a:link", "main a:hover") for \<a> tags in the \<main> element. Look at the Design Styles section of the stylesheet for the [Old Glory](https://github.com/webdevjeffus/drop-in-css/blob/master/css/drop-in-og.css) theme for an example.

```css
header nav li {
  border-left: 3px solid #888;    /* this should match html background-color */
}
```

This rule creates the vertical bars that separate the links in the nav bar within the \<header> element.

```css
main table,
main th,
main td {
  border: 1px solid #222;     /* this should match main font color */
  background-color: #eee;     /* this should be lighter than main background-color */
}
```

As you probably guess, this rule sets the background color for any tables with the \<main> element, and puts a border around all table cells in the same color as the text within the main element.

```css
main section { border-bottom: 2px solid #888; }
  /* this should match html background-color */

main aside { background-color: #bbb; }
  /* this should be slightly darker than main background-color, eg: 25% gray */
```

These last two rules give visual clues to support the semantic organization of the content in your \<main> element. The first adds a border to the bottom edge of each \<section> element, and the second puts a contrasting background behind the text in any sidebars (coded in HTML as \<aside> elements). Some **drop-in.css** themes, like [Old Glory](https://github.com/webdevjeffus/drop-in-css/blob/master/css/drop-in-og.css), add a border around \<aside> elements as well.







# _Everything above this line is REVISED as of 3/25/16_
<hr>
### Everything below this line is old text, cloned from my prior repo, CSS for Sinatra.


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

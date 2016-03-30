_**Note (3/29/16):** Since this document was last updated, I have changed the way that **drop-in.css** loads normalize.css and fonts from Google Fonts. Previously, these resources had to be linked separately in the \<head> of the HTML document; now, they are imported automatically by **drop-in.css**, using the CSS @import command. At the moment, the "Google Font Links" and "Design Styles" sections of this document are out of date; they will be updated to reflect the implementation of @import commands within 24 hours. Thanks for your patience. &mdash;Jeff_

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
h1 { font-size: 2.25rem; }
h2 { font-size: 1.75rem; }
h3 { font-size: 1.4rem; }
h4 { font-size: 1.2rem; }
h5 { font-size: 1.2rem; }
h6 {
  font-size: 1rem;
  font-style: italic;
}
```

These rules set the font-size for all heading elements. \<h1>-\<h4> are styled as the display font in the Design Styles/Fonts subsection, below, while \<h5> and \<h6> will appear in the general font. Since \<h6> headings have the same font-size as the text in \<p> and other, similar elements, \<h6> headings will display as italic text, to make them more visually distinct.

```css
h1, h2, h3, h4, p { margin: 0 0 0.5rem; }
h5, h6 { margin: 0 0 0.2rem; }

li:last-child,
p:last-child { margin-bottom: 0rem; }
```

The first two rules in this group remove the top, right and left margin set for headings and paragraphs in normalize.css. They set bottom margins that insert a bit of whitespace between elements, and especially between paragraphs. The last rule ("li:last-child" and "p:last-child") removes the bottom margin from a paragraph or list item if it's the last element within the parent element (usually the \<main> element or a \<section> for a \<p>, or a \<ul> or \<ol> for a \<li>), since padding or margin on the parent element already inserts whitespace after the last element.

```css
header:after,
main:after,
section:after {
  content: "";
  display: table;
  clear: both;
}
```

This rule automatically applies a "clearfix" immediately after \<header>, \<main> and \<section> elements, since these elements are likely to contain elements that are floated left or right. A clearfix has no effect if nothing inside the element is floated, but it also doesn't hurt anything by being there.

```css
a,
header nav input[type="submit"] {
  font-weight: bold;
  text-decoration: none;
}
```

This rule overrides the default appearance of links in an HTML document, removing the underline, but making the link text display in a bold font. (The color of links is handled in the next section.)

#### Borders

```css
/* Borders */

header nav li { border-left: 3px solid; }
main section { border-bottom: 2px solid; }
main table { border: 2px solid; }
main th, main td { border: 1px solid; }
main input, main textarea, main button {  border: 1px solid; }
```

These rules set up the style and weight of the borders used by **drop-in.css**. It is necessary to declare them in the Utility Styles section, rather than in the Header or Main Styles section, because CSS requires the style attribute for all borders to be set before border-color declarations in the [Design Styles/Colors](#colors) section will be recognized.

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
The Colors sub-section of the Design Styles section is the _only_ place where colors are declared in **drop-in.css**. If you want to use a different color scheme and can't find an existing theme in the [**drop-in.css** themes](https://github.com/webdevjeffus/drop-in-css/blob/master/docs/themes.md) collection, you can replace the color specifications in this section line by line; the comments in the code will help you figure out what each line does, and what kind of color to use.

Again, if you need to add _more_ or _more specific_ rules for color styling, do so using classes, and save them in your **application.css** file.

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
header nav input[type="submit"] { color: #c00; }
  /* darker contrasting color; inactive links */

a:hover,
a:active,
header nav input[type="submit"]:hover,
header nav input[type="submit"]:active { color: #f22; }
  /* brighter contrasting color; active links */
```

The next two rules, which start with "a:link" and "a:hover", set the colors for the links. The first rule sets the color of inactive links to a brick-red color. The second rule changes the color of the link text to a bright, fire-engine red when the mouse passes over them and when they are clicked. The "input[type='submit']" selectors are included to make the text on the Logout button behave like regular link text, part of styling it to _not_ look like a button.

If the theme requires different colors for links in the \<main> element than elsewhere on the page, you will have to add separate rules (eg., "main a:link", "main a:hover") for \<a> tags in the \<main> element. Look at the Design Styles section of the stylesheet for the [Old Glory](https://github.com/webdevjeffus/drop-in-css/blob/master/css/drop-in-og.css) theme for an example.

```css
header nav li { border-color: #888; }   /* this should match html background-color */
```

This rule declares the color of the vertical bars that separate the links in the nav bar within the \<header> element. The width and style of this border was declared in the [Utility Styles](#utility-styles) section, above.

```css
main table,
main th,
main td { border-color: #222; }   /* this should match main font color */

main tr:nth-of-type(odd)  { background-color: #eee; }  /* lighter than main bg-color */
main tr:nth-of-type(even) { background-color: #ccc; }  /* darker than main bg-color */
}
```

The first of these rules sets the color of all borders in and around tables, with the width and style having been previously established in the [Utility Styles](#utility-styles). The second and third rules&mdash;with "main tr:nth-of-type" selectors&mdash;set the background of table rows to alternate between slightly lighter than the \<main> element background, and slightly darker.

```css
main section { border-color: #888; }
  /* this should match html background-color */

main aside { background-color: #bbb; }
  /* this should be slightly darker than main background-color, eg: 25% gray */
```

These rules use color to provide visual clues that support the semantic organization of the content in your \<main> element. The first adds a border to the bottom edge of each \<section> element, and the second puts a contrasting background behind the text in any sidebars (coded in HTML as \<aside> elements). Some **drop-in.css** themes, like [Old Glory](https://github.com/webdevjeffus/drop-in-css/blob/master/css/drop-in-og.css), add a border around \<aside> elements as well. Remember that rules setting the establish the width and style of any borders must be listed in the [Utility Styles](#utility-styles) section.

```css
main input,
main textarea,
main button {
  color: #222;                  /* matches main text color */
  border-color: #222;           /* matches main text color */
}

main input[type="submit"],
main button {
  background-color: #bbb;       /* matches aside bg-color */
  color: #222;                  /* matches main text color */
}
```

These rules declare the colors for form inputs appearing in the \<main> element. Again, border styles and widths must be set in the [Utility Styles](#utility-styles) section before the color declarations here will have any effect.


### Header Styles
The rules in the Header Styles section style a simple header that should appear on every page of the app. The styles are designed to create a large app title or logo in the display font at the left-hand end of the \<header> element, with an optional line of copy beneath it. Site navigation is handled by a horizontal row of nav links at the right-hand edge of the \<header>.

```css
/* HEADER STYLES *************************************************************/

header { padding: 1rem; }

header>h1,
header div { float: left; }

header h1 {
  line-height: 1;
  font-size: 4rem;
}

header p {
  font-size: 1.25rem;
  font-style: italic;
  margin-bottom: 0;
}
```

The first rule just sets a 1rem padding on all sides of the \<header>, to keep the type from bumping against the margins.

The second rule applies the left float that puts the app title at the left edge of the \<header>. The float needs to be applied either to the logo, which is coded as an \<h1> that is a direct child of the \<header> element ("header h1"), or to a \<div> that holds both the \<h1> _and_ the \<p> that holds the site's motto or slogan ("header div"). As mentioned in the instructions on the README page, if you don't have a \<p> element beneath your \<h1> logo, you don't need to wrap the \<h1> in a \<div>.

The "header h1" and "header p" rules just describe the appearance of the font in the logo and slogan. If you change the fonts, you may need to tweak these values to make the header look the way you want.

```css
header nav { float: right; }

header nav ul { list-style: none; }

header nav li {
  display: inline-block;
  padding: 0 0.8rem 0 1rem;
}
```

The next three rules set up the nav links. The "header nav" rule applies a right float to the entire \<nav> element, so that it is displayed at the right end of the \<header>, opposite the flush-left logo. The "header nav ul" rule removes the bullets that browsers apply to unordered lists by default. The "header nav li" rule sets the list items&mdash;which will be the links in the nav bar&mdash;to inline-block, which makes them display on a horizontal line, instead of stacked up vertically. It also applies padding to the right and left sides of the list items, to spread them out a bit, without adding any padding to their top or bottom. (The amount of left and right padding differs to allow for the thickness of the left border that separates the links.)

```css
header nav li:nth-last-of-type(1) { padding-right: 0;}

header nav li:nth-of-type(1) { border-left: none;}

header nav input[type="submit"] {
  overflow: visible;
  text-align: center;
  width: auto;
  border: none;
}
```

The next two rules handle the edge-cases in the nav-link list: the first of these removes the right padding from the last list item, so it's not double-spaced from the right edge of the header, and the second turns _off_ the left border we applied to the nav links in the [Utility Styles/Borders](#borders) section, so that the borders only appear _between_ links.

The final rule in the Header Styles section, applied to "header nav input[type='submit']", finishes the job of styling the Logout button to look like any other link, which we started in the Design Section. Altogether, to make a button look like a link, we need to set the background-color and font color the same as the links we're matching (we did this in the Colors subsection of the Design Styles section); set the overflow to visible and center-align the text; set the width to auto, so it conforms to the length of the text in the button-link, and get rid of the button border.

### Main Styles
In the Main Styles section, **drop-in**'s type-based selectors really pay off: they let you (or your web dev framework) create an unlimited number of pages, partials, and forms which look decent (maybe not great, but certainly decent) with absolutely zero time spent on styling. The Main Styles section handles \<section>, \<article>, and \<aside> elements first, then deals with lists, forms, and tables in separate subsections.

```css
/* MAIN STYLES ***************************************************************/

main {
  padding: 1rem;
}

main section {
  margin-top: 1rem;
  padding-bottom: 1rem;
}

main section:nth-of-type(1) {
  padding-top: 0;
}

main section:nth-last-of-type(1) {
  padding-bottom: 0;
  border: none;
}
```

As in the Header Styles section, the first rule simply puts 1rem of padding around the \<main> element, to keep the text and other elements off of the margins.

The next three rules style the \<section> elements. The "main section" rule adds 1rem of margin to the top and 1 rem of padding to the bottom of each \<section>, but none to the sides, since we don't want whitespace doubling up with the right- and left-padding on the \<main> element. The second "main section" rule, with the ":nth-of-type(1)" selector, removes the top padding from the first \<section> element, to avoid doubling the top padding inside the \<main> element. The ":nth-last-of-type" rule selects the _last_ \<section> within the \<main>, and does two things: first, it removes the bottom padding, again to avoid double-padding at the bottom of the \<main>; and second, it removes the border we assigned in the Design Styles/Colors subsection, that appears at the bottom of each \<section>.

```css
main article {
  width: 65%;
  float: left;
}

main aside {
  width: 30%;
  float: right;
  padding: 1rem;
  font-size: 0.8rem;
}
```

The next two rules in the Main Styles section style the \<article> and \<aside> elements. Articles form the main column of a main-column/sidebar layout, floated to the left and occupying 65% of the available width. Asides form the sidebar; they are floated to the right, and occupy 30% of the available width. This leaves 5% of the available width as a margin between the \<article> and its \<aside>.

The last two declarations in the "main aside" rule put 1rem of padding on all sides of the sidebar, and reduce the font-size by 20%, to make it more visually distinct from the text in the article. Also, remember that we gave \<aside> elements a contrasting background color in the Design Styles/Colors subsection.

#### Lists

```css
/* Lists */

main ul {
  margin: 0 1rem 1rem;
  list-style: none;
}

main ol { margin: 0 1rem 1rem 2rem; }

main li { margin: 0.5rem 0; }

```

The rules for lists put a bit of extra whitespace in and around both ordered (numbered) and unordered lists, to enhance readability and to make them stand out from ordinary \<p> elements. The "main ul" rule also removes the bullets that appear next to each list item in an unordered list by default.

#### Forms

The **drop-in** stylesheet has several rules that style form components, but each rule is fairly straightforward. Forms are one of the areas most likely to require additional, custom styling for each app, but the rules in **drop-in.css** will at least make your forms easily readable during development.

Note that the selectors for form elements don't actually include the "form" element in their selector. **Drop-in.css** finds them with the "main" selector instead, plus their specific tag, to avoid accidentally grabbing a button, search field, or other input in your header or footer.

```css
main label { font-weight: bold; }

main input,
main textarea {
  margin-bottom: 0.75rem;
  display: block;
  width: 100%;
}
```

The first two rules for form elements set things up so that most label-input pairs appear on together, label above input, with a bit of extra margin beneath to separate them from the next input in the form. The lable is set to be bold, to make it pop. Inputs are set to be "display: block" and "width: 100%" to render a wide text box, with room to accept several words of text before overflowing&mdash;a bit long for username and passwords, but a more readable default for text fields that need to accept several words, like streed addresses or URLs. Plan to add some more specific styling rules with classes before deploying the app.

```css
main input[type="date"],
main input[type="datetime"],
main input[type="datetime-local"],
main input[type="email"],
main input[type="month"],
main input[type="number"],
main input[type="password"],
main input[type="search"],
main input[type="tel"],
main input[type="text"],
main input[type="time"],
main input[type="week"],
main textarea { padding: 0 0.5rem; }

main textarea { height: 4.5rem; }
```

These first of these two rules puts a tiny bit of right and left padding inside input boxes, to keep the text from bumping the borders of the fields. The second sets the height of textareas; for most fonts, 4.5rem is enough vertical space to display three lines of text without scrolling.

```css
main input[type="checkbox"],
main input[type="radio"] {
  display: inline;
  width: 1.5rem;
  margin-right: 1.5rem;
}

main input[type="range"] {
  display: inline;
  width: 16rem;
  margin-left: 1rem;
}
```

These two rules handle oddball input fields&mdash;checkboxes, inputs and ranges&mdash;setting them to "display: inline" so they appear on the same line with their labels. The width declaration in each of these rules overrides the "width: 100%" we set for all input elements earlier in this section, and the margins handle horizontal spacing between the label and the input, and between lable-input pairs appearing on the same line.

By **drop-in** default, if you put several radio buttons, checkboxes, and/or ranges into your HTML in a row, they will all display on the same line, not wrapping to the next line until the first line is filled all the way across. If you want them to be arranged vertically, wrap each input element in its own \<div>. See the form section of [demo.html](https://github.com/webdevjeffus/drop-in-css/blob/master/views/demo.html) for working examples.

```css
main button,
main input[type="submit"] {
  margin: 0.5rem auto;
  width: 12rem;
  padding-top: 0.07rem;
}
```

This final rule in the Main Styes/Forms subsection sets the width of all buttons, such as form-submit buttons, and centers them from right to left within their parent element. It also adds a tiny bit of headroom in the form of padding, to help center text vertically within a button.

#### Tables

The last two rules in the Main Styles section of **drop-in.css** style tables within the \<main> element. Recall that we set the width and style for all table borders in the [Utility Styles/Borders](#borders) section, and the colors for table borders and backgrounds in the [Colors](#colors) subsection of Design Styles, above.

```css
/* Tables */

main table {
  width: 100%;
  margin-bottom: 1rem;
  border-collapse: collapse;
}

main th,
main td {
  padding: 0.25rem 0;
  text-align: center;
}
```

The first rule, for "main table", tells the browser to make tables the full width of the available space, with 1rem of whitespace beneath them. It also collapses the CSS's default double border for tables to more modern single lines. The rule for table cells (\<th> and \<td> elements) puts just a bit of top and bottom padding in each cell, and center-aligns the text within each cell.


### Footer Styles

There's just one rule in for **drop-in**'s \<footer> element.

```css
/* FOOTER STYLES */

footer {
  text-align: center;
  font-size: 0.8rem;
  padding: 1rem;
}
```

This rule centers all text; sets the font size of all elements to 80% of the size at which they are displayed in the \<main> element; and adds 1rem of padding to all sides of the footer. These rules will be applied to any headings (\<h1>-\<h6>), paragraphs, and other elements you include in footer, allowing a fair amount of flexibility in creating \<footer> content without needing custom styling.

<hr>

#### Licenses

The documentation in this repo is Copyright &copy; 2016 by Jeff George.

<a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/"><img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by-nc-sa/4.0/88x31.png" /></a><br /><span xmlns:dct="http://purl.org/dc/terms/" property="dct:title">Documentation for <b>Drop-In CSS</b></span> by
<a href="http://webdevjeff.us">Jeff George</a> is licensed under a <a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/">Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License</a>.

The code files in this repo, including **drop-in.css**, all **drop-in.css** themes, and all view files, may be used under the terms of the [MIT License](https://opensource.org/licenses/MIT).

# CSS Specificity and _drop-in.css_

**drop-in.css** is able to instantly style an HTML document without any classes or id's by taking advantage of the CSS principle of **specificity**. Simply put, the more specific the selector of a CSS rule, the more powerful that rule is. For a complete discussion of specificity, visit the [Mozilla Developer Network](https://developer.mozilla.org/en-US/docs/Web/CSS/Specificity) page on the subject. I'll cover just enough here to explain how and why **drop-in.css** works.

## Weighting selector types
CSS can use several kinds of selectors to target an element for styling, and each kind is assigned a weight. When more than one CSS rule targets a given element, the rule with the selector with the greatest weight is applied in preference to the others.

<table>
  <tr>
    <th>Selector type</th>
    <th>Weight</th>
  </tr>
  <tr>
    <td>Element tag (eg: &lt;h1&gt;, &lt;p&gt;, &lt;li&gt;)</td>
    <td>1</td>
  </tr>
  <tr>
    <td>Pseudo-element (eg: :before, :after)</td>
    <td>1</td>
  </tr>
  <tr>
    <td>Class (eg: .example-class)</td>
    <td>10</td>
  </tr>
  <tr>
    <td>Attribute (eg: [type="text"], [type="password"])</td>
    <td>10</td>
  </tr>
  <tr>
    <td>Pseudo-class (eg: :hover, :first-child)</td>
    <td>10</td>
  </tr>
  <tr>
    <td>ID (eg: #example-id)</td>
    <td>100</td>
  </tr>
</table>

Thus, a rule with a selector that includes a single element tag, such as "p", has a weight of 1. It will be overridden by any rule with greater selector weight, such as "main p" (weight: 2), ".example-class" (weight: 10), "main .example-class" (weight: 11), "form input\[type='text']" (weight: 12), or "#example-id" (weight: 100).

### The "ties go to the last rule" rule
When the weight of two rules is _exactly_ the same, the browser will apply the rule that appears _last_ in the stylesheets. Because of this, it's important to link the stylesheets in the proper order in the \<head> of your HTML file: **normalize.css**, then **drop-in.css**, then **application.css**. This way, in the few cases where a rule in **drop-in.css** might be equal in weight to a rule in **normalize.css**, the rule in **drop-in.css** will be the one applied.

## Specifity and _drop-in.css_
The magic of **drop-in.css** happens because it selects elements using only HTML tags, taking advantage of the CSS specifity rules and semantic HTML to tell the browser which similar rule to apply to each element.

Virtually all of the rules in **normalize.css** have single-tag selectors (weight: 1), while the rules in **drop-in.css** almost all use two or three tags in their selectors (weight: 2 or 3). At the very least, the selectors in **drop-in.css** use a high-level semantic element (\<header>, \<main>, or \<footer>) along with the tag for the element actually being targetted, such as \<h2>, \<p>, or \<li>. Thus, any time rules in both **normalize.css** and **drop-in.css** target the same element, the element will be styled according to the more heavily-weighted rule in **drop-in.css**. Also, the browser will know to style a given element differently if it appears in one part of the document or another (eg. "header h1" vs. "main h1").

## What about classes and id's?
If you make additions to the **drop-in.css** file, do _not_ use classes or id's as selectors. The point of **drop-in.css** is that it instantly styles HTML documents without the addition of any classes or id's to the mark-up. If you add styles that select by classes or id's, you defeat the purpose of **drop-in.css**.

When you need to create a CSS rule with a class selector, put it in your **application.css** file. If you use at least one class in the selector you write for any styles in your application.css folder, you can be sure they will trump the styles in both **drop-in.css** and **normalize.css**. Also, you will be sure that your customized version of **drop-in.css** will still work without selecting by class, so you can use it again on future projects.

For several reasons, you should avoid using id's as CSS selectors in all cases&mdash;reserve id's for use in your Javascript and jQuery code. Even if you need to style a single element, it's better to create a one-time-use class to select it. That way, you never have to worry about changes to your JS/jQ id selectors breaking your styling, or changes to your CSS class selectors breaking your code. You can read more about this in my blog on the subject, ["Relax! Don't do it!"](http://webdevjeff.us/blog/css-concepts.html).

## Drop-in-style specificity examples

Here are some examples that apply CSS's principle of specificity. I've limited the example to using _only_ element tags in the selectors, just as in **drop-in.css**.

```css
/* CSS Rules Examples */

/* Rule 1 - selector with one tag */
p { color: black; }

/* Rule 2 - selector with two tags */
main p { color: blue; }

/* Rule 3 - selector with three tags */
main aside p { color: green }

/* Rule 4 - selector with two tags, one of which is different than Rule 2 */
footer p { font-size: 75% }
```

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

<hr>

#### Licenses

This document is Copyright &copy; 2016 by Jeff George.

<a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/"><img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by-nc-sa/4.0/88x31.png" /></a><br /><span xmlns:dct="http://purl.org/dc/terms/" href="http://purl.org/dc/dcmitype/Text" property="dct:title" rel="dct:type">Documentation for <b>Drop-in CSS</b></span> by <a xmlns:cc="http://creativecommons.org/ns#" href="webdevjeffus.github.io/drop-in-css" property="cc:attributionName" rel="cc:attributionURL">Jeff George</a> is distributed under a <a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/">Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License</a>.

The code files in this repo, including **drop-in.css**, **index.html** and **layout.html**, may be used under the terms of the [MIT License](https://opensource.org/licenses/MIT).


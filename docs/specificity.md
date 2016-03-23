# _WORK IN PROGRESS - 3/23/19_

# CSS Specificity and _drop-in.css_

**drop-in.css** is able to instantly style an HTML document without any classes or id's by taking advantage of the CSS principle of **specifity**. Simply put, the more specific the selector of a CSS rule, the more powerful that rule is. For a complete discussion of specificity, visit the [Mozilla Developer Network](https://developer.mozilla.org/en-US/docs/Web/CSS/Specificity) page on the subject; I'll cover just enough here to explain how and why **drop-in.css** works.

## Weighting selector types
CSS can use several kinds of selectors to target an element for styling, and each kind is assigned a weight. When more than one CSS rule targets a given element, the one with the greatest weight is applied in preference to the others.

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

Thus, a rule with a selector that includes a single element tag, such as "p", has a weight of 1. It will be overridden by any rule with greater selector weight, such as "main p" (weight: 2), ".example-class" (weight: 10), "main .example-class" (weight: 11), or "#example-id" (weight: 100).

### Ties go to the last rule
When the weight of two rules is _exactly_ the same, the browser will apply the rule that appears _last_ in the stylesheets. Because of this, it's important to link the stylesheets in the proper order in the \<head> of your HTML file: **normalize.css**, then **drop-in.css**, then **application.css**. This way, in the few cases where **drop-in.css** actually does use a single-tag selector, it's rule will take precedence over any applicable rule in **normalize.css**.

## Specifity, semantics, and Drop-In CSS
The magic of **drop-in.css** happens because it selects elements using only HTML tags, taking advantage of the CSS specifity rules and semantic HTML to tell the browser which similar rule to apply to each element.

Virtually all of the rules in **normalize.css** have single-tag selectors (weight: 1), while the rules in **drop-in.css** almost all use two or three tags in their selectors (weight: 2 or 3). Thus, any time rules in both **normalize.css** and **drop-in.css** target the same element, the element will be styled according to the more heavily-weighted rule in **drop-in.css**.

Similarly,

The magic of **drop-in.css** happens because CSS lets you build selectors using multiple tags to create increasingly specific rules. CSS's principle of _specifity_ states that a rule with a _more specific_ selector always overrides a rule with a _less specific_ one. Simply put, the more tags named in a CSS selector, the more specific it is. A rule with two tags in its selector will override a rule built with only one tag, and a rule with three tags in its selector will trump them both. Here are some examples:

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

## Tags vs. classes vs. id's

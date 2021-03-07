# Web Accessibility

[w3.org](https://www.w3.org/WAI/tutorials/)

Best-practice guidance on implementing accessibility in different situations. They combine WCAG 2 success criteria and techniques from various conformance levels.

## 1. Page Structure

Use semantic HTML elements in combination with WAI-ARIA labels.

```html
<header role="banner">…</header>
<main role="main">…</main>
<nav role="navigation">…</nav>
<footer role="contentinfo">…</footer>
```

`aria-label` → Label region or element that will not appear visually on the page. *(ex: Main Navigation)*

`area-labelledby` → Point to an existing element by its (unique) id. The label of the region is the content of the referenced element. Every element can be a label this way. Labels should be short and descriptive. If a heading is present in the region, consider using it as the label. *(ex: regionheading)*

Nest headings by their rank. The most important heading has the rank 1 `h1`, the least important heading rank 6 `h6`. Skipping heading ranks can be confusing and should be avoided where possible.

Use different types of lists to group information according to its nature to provide orientation for users.

- Unordered lists are used when the order of the items is not relevant. Typically marked with a bullet.
  - `ul li`
- Ordered lists are used for sequential information. Typically marked with automatic enumeration by the browser.
  - `ol li`
- Description lists are groups of related terms and descriptions which are connected programmatically.
  - `dl dt dd dd dt dd`

## 2. Menus

Semantic markup conveys the menu structure to users. Menus coded semantically can easily adapt to different situations, such as small screen displays, screen magnification, and other assistive technology.

Convey the menu structure, typically by using a list. Such structural information allows assistive technologies to announce the number of items in the menu and provide corresponding navigation functionality.

`ul` for menu items and `ol` for sequence of menu items (steps).

***role=***  
`aria-current="page"` : attribute to indicate the current page in the menu  
`aria-haspopup="true"` : declares that a menu item has a submenu  
`aria-expanded="false"` : declares that the submenu is hidden  
`menubar` : represents a (usually horizontal) menu bar  
`menu` : represents a set of links or commands in a menu bar, used for nested menus  
`menuitem` : represents an individual menu item  
`separator` : represents a separator between two groups of menu items in a menu

## 3. Images

Image used to label other information (icon).
> [Telephone Icon] `alt="Telephone:"` 555 555-5555

Image used to supplement other information (embedded image).
> [Image of Dog] `alt="Dog with a bell attached to its collar"` Off-duty guide dog...

Image conveying succinct information (diagram or illustration).
> [Image of Twist Cap] `alt="Push the cap down and turn it clockwise"`

Image conveying an impression or emotion (fun).
> [Image of People Laughing] `alt="We're fun!"`

Image conveying file format (pdf icon).
> [PDF Icon] `alt="PDF"`

Image used as part of page design (border). Null alt value will hide content on screen readers.
> [Border Image] `alt=""`

Image as part of text link (thumbnail).
> [Boxart] `alt=""`

Image with adjacent text alternative (cited photo).
> [Image] `alt=""`

Image used for abiance (background).
> [Image] `alt=""`

Image used alone as a linked logo (logo).
> [Logo] `alt="Google Home"`

Logo image within link text.
> [Logo] `alt=""` Google

Icon image conveying information within link text.
> Google [External Link Icon] `alt="new window"`

Stand-alone icon image that has a function.
> [Print Icon] `alt="Print this page"`

Image used in a button.
> [Search Icon] `alt="Search"`

Styled text with decorative effect (image of text). Try to use CSS where possible.
> [Image of Text "Welcome to my site"] `alt="Welcome to my site."`

Image of text used as an unlinked logo (ESRB logo).
> [Github Universe] `alt="Github Universe"`

Multiple images conveying a single piece of information (star rating).
> [***--] `alt="3 out of 5 stars"`

### Alt Decision Tree

1. Does the image contain text?
    - No: Continue
    - Yes:
        - ...and the text is also present as real text nearby `alt=""`
        - ...and the text is only shown for visual effects `alt=""`
        - ...and the text has a specific function (icon) `alt="{function}"`
        - ...and the text in the image is not present otherwise `alt="{text}"`
2. Is the image used in a link or a button, and would it be hard or impossible to understand what the link or button does, if the image wasn't there?
    - No: Continue
    - Yes: `alt="{destination of the link or action taken}"`
3. Does the image contribute to the current page or context?
    - No: Continue
    - Yes:
        - ...and it's a simple graphic or photo `alt="{brief desc conveys meaning}"`
        - ...and it's a graph or complex piece of information `include info elsewhere on page`
        - ...and it shows content that is redundant to real text nearby `alt=""`
4. Is the image purely decorative or not intended for the user?
    - No: Unique use case. More research is needed.
    - Yes: `alt=""`

## Tables

Header cells must be marked up with `<th>`, and data cells with `<td>` to make tables accessible. For more complex tables, explicit associations may be needed using `scope`, `id`, and `headers` attributes.

- A caption functions like a heading for a table. Most screen readers announce the content of captions. Captions help users to find a table and understand what it’s about and decide if they want to read it. If the user uses “Tables Mode”, captions are the primary mechanism to identify tables. The caption is provided by the `<caption>` element.

- A `<table summary="">` conveys information about the organization of the data in a table and helps users navigate it. For example, if a table has an unusual structure (as in the examples below), information about what content can be found in which row or column can be provided to the user. A summary is usually only needed for complex tables.

```html
<!-- One Header -->
<table>
  <tr>
    <th>Date</th>
    <th>Event</th>
    <th>Venue</th>
  </tr>
  <tr>
    <td>12 February</td>
    <td>Waltz with Strauss</td>
    <td>Main Hall</td>
  </tr>
  […]
</table>
```

```html
<!-- Two Headers -->
<table>
  <caption>Delivery slots:</caption>
  <tr>
    <td></td>
    <th scope="col">Monday</th>
    <th scope="col">Tuesday</th>
    <th scope="col">Wednesday</th>
    <th scope="col">Thursday</th>
    <th scope="col">Friday</th>
  </tr>
  <tr>
    <th scope="row">09:00 - 11:00</th>
    <td>Closed</td>
    <td>Open</td>
    <td>Open</td>
    <td>Closed</td>
    <td>Closed</td>
  </tr>
  <tr>
    <th scope="row">11:00 - 13:00</th>
    <td>Open</td>
    <td>Open</td>
    <td>Closed</td>
    <td>Closed</td>
    <td>Closed</td>
  </tr>
  […]
</table>
```

```html
<!-- Irregular Header -->
<table>
  <caption>
    Poster availability
  </caption>
  <col>
  <col>
  <colgroup span="3"></colgroup>
  <thead>
    <tr>
      <th scope="col">Poster name</th>
      <th scope="col">Color</th>
      <th colspan="3" scope="colgroup">Sizes available</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="3" scope="rowgroup">Zodiac</th>
      <th scope="row">Full color</th>
      <td>A2</td>
      <td>A3</td>
      <td>A4</td>
    </tr>
    <tr>
      <th scope="row">Black and white</th>
      <td>A1</td>
      <td>A2</td>
      <td>A3</td>
    </tr>
    <tr>
      <th scope="row">Sepia</th>
      <td>A3</td>
      <td>A4</td>
      <td>A5</td>
    </tr>
  </tbody>
  <tbody>
    <tr>
      <th rowspan="2" scope="rowgroup">Angels</th>
      <th scope="row">Black and white</th>
      <td>A1</td>
      <td>A3</td>
      <td>A4</td>
    </tr>
    <tr>
      <th scope="row">Sepia</th>
      <td>A2</td>
      <td>A3</td>
      <td>A5</td>
    </tr>
  </tbody>
</table>
```

```html
<!-- Multi-level Headers -->
[…]
<td id="blank">&nbsp;</td>
<th id="co1" headers="blank">Example 1 Ltd</th>
<th id="co2" headers="blank">Example 2 Co</th>
[…]
<th id="c1" headers="blank">Contact</th>
[…]
```

## Forms

Associating labels explicitly:

```html
<label for="firstname" aria-label="First Name" />
```

Using aria-labelledby:

```html
<input type="text" name="search" aria-labelledby="searchbutton">
<button id="searchbutton" type="submit">Search</button>
```

The `<fieldset>` element provides a container for related form controls, and the `<legend>` element acts as a heading to identify the group.

```html
<fieldset>
<legend>Output format</legend>
  <div>
    <input type="radio" name="format" id="txt" value="txt" checked>
    <label for="txt">Text file</label>
  </div>
  <div>
    <input type="radio" name="format" id="csv" value="csv">
    <label for="csv">CSV file</label>
  </div>
  […]
</fieldset>
```

Associate additional instructions with a form field is to use aria-describedby. Information referenced by this attribute is made available to the users after the label and other information is announced.

```html
<label id="expLabel" for="expire">Expiration date:</label>
<span>
	<input type="text" name="expire" id="expire" aria-labelledby="expLabel" aria-describedby="expDesc">
	<span id="expDesc">MM/YYYY</span>
</span>
```

Label should also display “(required)”, to inform users that don’t use assistive technology or use older web browsers that do not support the HTML5 required attribute.

```html
<label for="name">Name (required): </label>
<input type="text" name="name" id="name" required aria-required="true">
```

HTML5 also provides input types for other data, including email, url, number, range, date, or time.

In general, client-side validation results in a better user experience and makes resolving validation errors more understandable. It can also reduce network and server load.

The HTML5 `pattern` attribute allows the use of regular expressions to specify custom formats for the input.

```html
<input type="text" id="license" placeholder="CCC XXXX 9999"
  pattern="[A-ZÖÄÜ]{1,3}( )[A-Z]{2,4}( )[0-9]{1,4}"
>
```

When a form is submitted, it is important that the user is notified whether the submission was successful or if errors occurred.

A common way to provide feedback is by using the main heading of the web page, usually, the most prominently displayed `<h1>` or `<`h2>` element.

```html
<h1>3 Errors – Billing Address</h1>
<h1>Thank you for submitting your order.</h1>
```

The `<title>` element of the web page can be useful to indicate successes and errors. In particular, screen reader users will receive this feedback immediately when the web page is loaded. This can be helpful when the main heading is located deeper within the content, for example, after the navigation menus.

```html
<title>3 Errors – Billing Address</title>
<title>Thank you for submitting your order.</title>
```

When errors occur, it is helpful to list them at the top of the page, before the form. The list should have a distinctive heading so that it is easy to identify. Each error listed should:

- Reference the label of the corresponding form control, to help the user recognize the control;
- Provide a concise description of the error in a way that is easy to understand by everyone;
- Provide an indication of how to correct mistakes, and remind users of any format requirements;
- Include an in-page link to the corresponding form control to make access easier for the users.

Sometimes, for example, when using AJAX techniques, the browser is not loading a new page but shows changes, such as form errors, dynamically on the page. The list of errors should be inserted into a prominent container on the top to inform the user in such a case. In addition to the advice above, this container should have the role attribute set to `alert` to make assistive technology users aware of this change.

## Carousels

As a collection of content items, carousels are typically best represented as unordered lists, using `<ul>` and `<li>`. Depending on the context, other elements can also be used.

```html
<!-- Carousel -->
<section class="carousel" aria-labelledby="carouselheading">
  <h3 id="carouselheading" class="visuallyhidden">Recent news</h3>
  <ul>
    <li class="slide">…</li>
    <li class="slide">…</li>
    <li class="slide">…</li>
    …
  </ul>
</section>

<!-- Carousel Item -->
<li class="slide" style="background-image: url('teddy1.jpg');">
  <article>
    <h4>Space Teddy production reaches all-time high</h4>
    <p>Teddies in Space Inc. has released outstanding numbers for the last solar year. The production of Space Teddies increased by 17%. The new version, scheduled to be released in a few months, will likely be the biggest Space Teddy release ever.</p>
    …
  </article>
</li>
```

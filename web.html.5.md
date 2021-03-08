# HTML 5

[dev.to](https://dev.to/vaibhavkhulbe/it-s-time-to-supercharge-your-html-skills-5b6k)

## APIs

`navigator.geolocation` [[docs]](https://developer.mozilla.org/en-US/docs/Web/API/Geolocation_API) prompts the user's browser asking them permission to access their location data.

```javascript
function getLocation() {
  // Check for the geolocation service
  if (navigator.geolocation) {
    navigator.geolocation.watchPosition(showPosition);
  } else {
    el.innerHTML = "Geolocation is not supported.";
  }
}
function showPosition(position) {
  el.innerHTML = "Latitude: " + position.coords.latitude +
  "<br>Longitude: " + position.coords.longitude;
}
```

`Worker()` [[docs]](https://developer.mozilla.org/en-US/docs/Web/API/Web_Workers_API/Using_web_workers) is an independent script running in the background without affecting the performance of the page while it's loading. 

```javascript
// 1. CHECK FOR WEB WORKER SUPPORT
if (typeof(Worker) !== "undefined") {
  // Supported!
} else {
  // Not supported :(
}

// 2. CREATING A WEB WORKER OBJECT
if (typeof(w) == "undefined") {
  w = new Worker("worker_file.js");
}

// 3. SEND A MESSAGE FROM WORKER
w.onmessage = function(event){
  document.getElementById("workerdiv").innerHTML = event.data;
};
```

`EventSource` [[docs]](https://developer.mozilla.org/en-US/docs/Web/API/Server-sent_events/Using_server-sent_events) is triggered when a web page automatically gets updates from a server. SSE stands for Server-Sent Events.

```javascript
// 1. CHECK SUPPORT
if(typeof(EventSource) !== "undefined") {
  // Supported
} else {
  // No server-sent events supported :(
}

// 2. RECIEVE EVENTS FROM SERVER
var source = new EventSource("myserver.php");
source.onmessage = function(event) {
  document.getElementById("serverresult").innerHTML += event.data + "<hr>";
};
```

`localStorage` and `sessionStorage` [[docs]](https://developer.mozilla.org/en-US/docs/Web/API/Web_Storage_API) can store data locally within the user's browser. The other option to go is to create cookies but web storage is better as it's more secure and you can store large amounts of data.

```javascript
// 1. CHECK SUPPORT
if (typeof(Storage) !== "undefined") {
  // supported!
} else {
  // No Web Storage support :(
}

// 2. USING LOCALSTORAGE

// Store
localStorage.setItem("name", "Vaibhav");

// Retrieve
document.getElementById("namediv").innerHTML = localStorage.getItem("name");

// 2. USING SESSIONSTORAGE
sessionStorage.setItem('myName', 'Vaibhav');

```

---

## Attributes

`accesskey` : global attribute which specifies a shortcut key to activate/focus an element

```html
<a href="..." accesskey="d">...</a>
```

`autofocus` : provides focus to the input element automatically by placing the cursor on it

```html
<input type="text" id="username" name="username" autofocus />
```

`contenteditable` : attribute that can be set on an element to make the content editable.

```html
<ul contenteditable="true">
  <li>1. Milk</li>
  <li>2. Bread</li>
  <li>3. Eggs</li>
</ul>
```

`data-*` : attribute used to store custom data private to the page or application

```html
 <div id="data-attr" data-custom-attr="Lorem ipsum" />
```

```javascript
document.getElementById('data-attr').dataset['custom-attr'];
```

`draggable` : global attribute which specifies whether an element is draggable or not

```html
<p draggable="true">...</p>
```

`hidden` : boolean attribute which specifies that an element is not yet, or is no longer, relevant.

```html
<p hidden>...</p>
```

`itemprop` : add properties to an item, easy to group with attr

```html
<div itemscope itemtype="http://schema.org/Movie">
  <h1 itemprop="name">Avatar</h1>
  <span>Director:
    <span itemprop="director">James Cameron</span>
    (born August 16, 1954)</span>
  <span itemprop="genre">Science fiction</span>
  <a href="../movies/avatar-theatrical-trailer.html"
    itemprop="trailer">Trailer</a>
</div>
```

`required` : mark an input field as mandatory

```html
<input type="text" id="username" name="username" required />
```

`spellcheck` : specifies whether the element is to have its spelling and grammar checked

```html
<p spellcheck="true">...</p>
```

`pattern` : specify a pattern using regex to validate an input

```html
<input pattern="^(?=.*\d)(?=.*[a-z])(?=.*[A-Z]).{6,20}$" />
```

---

## Event Attributes

`ondbclick` : fires on a mouse double-click on the element  
`onblur` : fires the moment that the element loses focus  
`oncanplay` : script to be run when a file is ready to start playing  
`oncopy` : fires when the user copies the content of an element  
`onerror` : script to be run when an error occurs  
`onload` : fires after the page is finished loading  
`onresize` : fires when the browser window is resized  
`onscroll` : script to be run when an element's scrollbar is being scrolled  
`onsearch` : fires when the user writes something in a search field  
`ontoggle` : fires when the user opens or closes the `<detail>` element  

---

## Semantic Tags

HTML tags we use should describe and convey the meaning of the underlying content. Semantic tags improve accessibility, seo, and readability of code.

### 1. Main Root

`<html>` : represents the root of an HTML document

```html
<html></html>
```

### 2. Document Metadata

*Metadata contains information about the page.*

`<base>` : specifies the base URL to use for all relative URLs

```html
<base href="https://example.com" />
```

`<head>` : contains machine-readable inforamation (metadata)

```html
<head>
  ...
</head>
```

`<link>` : specifies relationships between the current document and an external resource

```html
<link href="main.css" rel="stylesheet">
<link rel="icon" href="favicon.ico">
```

`<meta>` : metadata that cannot be represented by other HTML meta-related elements

```html
<meta charset="utf-8">
<meta http-equiv="refresh" content="3;url=https://www.mozilla.org">
```

`<style>` : contains style information for a document, or part of a document

```html
<style>
  p {
    color: red;
  }
</style>
```

`<title>` : defines the document's title, shown in browser title

```html
<title>Brandon</title>
```

### 3. Section Root

`<body>` : represents the content of an HTML document (only one per document)

```html
<body>
  <p>This is a paragraph</p>
</body>
```

### 4. Section Content

*Content sectioning elements allow you to organize the document content into logical pieces.*

`<address>` : provides contact information for a person or organization

```html
<address>
  <a href="tel:+15555555555">(555) 555-5555</a>
</address>
```

`<article>` : a self-contained composition in a document, page, application, or site, which is intended to be independently distributable or reusable

```html
<article>
  <h1>...</h1>
  <p>...</p>
</article>
```

`<aside>` : a portion of a document whose content is only indirectly related to the document's main content

```html
<p>
  <aside>...</aside>
</p>
```

`<footer>` : contains information about the author, copyright data, and/or links to related documents

```html
<footer>
...
</footer>
```

`<header>` : contains a group of introductory or navigational aids

```html
<header>
...
</header>
```

`<h1>...<h6>` : six levels of section headings

```html
<h1>...</h1>
<h2>...</h2>
<h3>...</h3>
<h4>...</h4>
<h5>...</h5>
<h6>...</h6>
```

`<main>` : the dominant content of the body or a document

```html
<main>
  <p>...</p>
  <p>...</p>
</main>
```

`<nav>` : a section of a page whose purpose is to provide navigation links

```html
<nav class="crumbs">
  <ol>
    <li class="crumb"><a href="#">Bikes</a></li>
    <li class="crumb"><a href="#">BMX</a></li>
    <li class="crumb">Jump Bike 3000</li>
  </ol>
</nav>
```

`<section>` : a generic standalone section of a document (doesn't have a more specific semantic element to represent it)

```html
<section>
...
</section>
```

### 5. Text Content

*Use HTML text content elements to organize blocks or sections of content placed between the opening `<body>` and closing `</body>` tags. Important for accessibility and SEO, these elements identify the purpose or structure of that content.*

`<block-quote>` : indicates that the enclosed text is an extended quotation

```html
<blockquote cite="source_url_of_quote">
  <p>...</p>
</blockquote>
```

`<dd>` : provides the description, definition, or value for the preceding term (`dt`) in a description list (`dl`)  
`<dl>` : represents a description list  
`<dt>` : a term in a description or definition list

```html
<dl>
  <dt>...</dt>
  <dd>...</dd>
</dl>
```

`<div>` : generic container for flow content

```html
<div>...</div>
```

`<figure>` : self-contained content, potentially with an optional caption  
`<figcaption>` : a caption or legend describing the contents of its parent `figure` element

```html
<figure>
  <img src="..." alt="...">
  <figcaption>...</figcaption>
</figure>
```

`<hr>` : a thematic break between paragraph-level elements

```html
<hr>
```

`<ol>` : an ordered list of items (numbered list)  
`<ul>` : an unordered list of items (bulleted list)  
`<li>` : an item in a list

```html
  <ol>
    <li>...</li>
    <li>...</li>
  </ol>
  
  <ul>
    <li>...</li>
    <li>...</li>
  </ul>
```

`<p>` : a paragraph

```html
<p>...</p>
```

`<pre>` : preformatted text (presented exactly as written in HTML)

```html
<pre>
  L          TE
    A       A
      C    V
       R A
       DOU
       LOU
      REUSE
</pre>
```

### 6. Inline Text Semantics

*Use the HTML inline text semantic to define the meaning, structure, or style of a word, line, or any arbitrary piece of text.*

`<a>` : a hyperlink known as an anchor

```html
 <a href="...">...</a>
```

`<abbr>` : an abbreviation or acronym

```html
<p>
  <abbr title="Cascading Style Sheets">CSS</abbr>
  <abbr title="HyperText Markup Language">HTML</abbr>
</p>
```

`<b>` : draw reader's attention to the element's contents

```html
<b>...</b>
```

`<bdi>` : treat the text it contains in isolation from its surrounding text

```html
<li><bdi class="name">Brandon</bdi>: 1st place</li>
```

`<bdo>` : overrides the current directionality of text

```html
<bdo dir="ltr">...</bdo>
```

`<br>` : line break in text (carriage-return) *DO NOT USE OUTSIDE OF `<p>` !*

```html
<p>
  ...,<br>
  ...,<br>
  ...
</p>
```

`<cite>` : describe a reference to a cited creative work, and must include the title of the work

```html
<cite><a href="...">...</a></cite>
```

`<code>` : a fragment of computer code

```html
<code>...</code>
```

`<data>` : links a given piece of content with a machine-readable translation - if the content is time- or date-related then the `<time>` element must be used

```html
<li><data value="999">...</data></li>
```

`<dfn>` : term being defined within the context of a definition phrase or sentence

```html
<p>A <dfn id="def-validator">validator</dfn> is a program that checks for syntax errors in code or documents.</p>
```

`<em>` : text that has stress emphasis

```html
<p>
  <em>...</em>
<p>
```

`<i>` : range of text that is set off from the normal text for some reason (ex. tehcnical terms, idiomatic text)

```html
<p>
  <i>...</i>
</p>
```

`<kbd>` : a span of inline text denoting textual user input from a keyboard, voice input, or any other text entry device

```html
<p>
  <kbd>Ctrl</kbd>
  ...
  <kbd>Alt</kbd>
  ...
  <kbd>Del</kbd>
</p>
```

`<mark>` : text which is marked or highlighted for reference or notation purporses

```html
<p>
  <mark>...</mark>
</p>
```

```css
mark {
  background-color: brightpink;
  color: #000000;
}
```

`<q>` : text is a short inline quotation (surrounded by "...")

```html
<p>
  <q cite="url">...</q>
</p>
```

`<s>` : text with a strikethrough

```html
<p>
  <s>...</s>
</p>
```

`<samp>` : text which represents sample (or quoted) output from a computer program

```html
<p>
  <samp>Keyboard not found <br>Press F1 to continue</samp>
</p>
```

`<small>` : side-comments and small print [*copyright, legal text*]

```html
<p>
  <small>...</small>
</p>
```

`<span>` : inline container for phrasing content, which does not inherently represent anything

```html
<p>Add the <span class="ingredient">basil</span>, <span class="ingredient">pine nuts</span> and <span class="ingredient">garlic</span> to a blender and blend into a paste.</p>
```

`<strong>` : contents have strong importance, seriousness, or urgency [*bold*]  

##### attributes: *_*

```html
<p>
  <strong>...</strong>
</p>
```

`<sub>` : inline text which should be displayed as subscript

```html
<p>
  <sub>...</sub>
</p>
```

`<sup>` : inline text which should be displayed as superscript

```html
<p>
  <sup>...</sup>
</p>
```

`<time>` : a specific period in time

```html
<p>
  <time datetime="2018-07-07">July 7</time>
  <time datetime="20:00">20:00</time>
  <time datetime="PT2H30M">2h 30m</time>
</p>
```

`<u>` : text which indicates that it has a non-textual annotation

> This element used to be called the __"Underline"__ element in older versions of HTML, and is still sometimes misused in this way. To underline text, you should instead apply a style that includes the CSS `text-decoration` property set to `underline`.

```html
<p>You could use this element to highlight <u>speling</u> mistakes, so the writer can <u>corect</u> them.</p>
```

`<var>` : name of a variable in a mathematical expression or a programming context

```html
<p>
  <var>firstName</var>
</p>
```

`<wbr>` : a word break opportunity (browser may optionally break a line)

```html
<p>
  <wbr>...</wbr>
</p>
```

### 7. Image and Multimedia

*HTML supports various multimedia resources such as images, audio, and video.*

`<area>` : defines an area inside an image map that has predefined clickable areas  
`<map>` : define an image map

```html
<map name="infographic">
  <area shape="rect" coords="184,6,253,27" href="..." />
  <area shape="circle" coords="130,136,60" href="..." />
</map>
<img usemap="#infographic" src="..." alt="..." />
```

`<audio>` : embed sound content into the document

```html
<audio controls src="...">
  Your browser does not support the <code>audio</code> element.
</audio>
```

`<img>` : embed an image into the document

```html
<img src="url" alt="..." >
```

`<track>` : child of `<audio>` and `<video>` used for subtitles

```html
<video controls src="...">
  <track default kind="captions" srclang="en" src="url.vtt" />
  Sorry, your browser doesn't support embedded videos.
</video>
```

`<video>` : embed video content into the document

```html
<video autoplay controls loop muted poster preload src>
  <source src="url.webm" type="video/webm">
  <source src="url.mp4" type="video/mp4">
  Sorry, your browser doesn't support embedded videos.
</video>
```

### 8. Embedded Content

*In addition to regular multimedia content, HTML can include a variety of other content, even if it's not always easy to interact with.*

`<embed>` : embed external content into the document

```html
<embed type="video/quicktime" src="url.mov" title="">
```

`<iframe>` : embed another HTML page into the current one

```html
<iframe src="url" title="..."></iframe>
```

`<object>` : an external resource

```html
<object type="application/pdf" data="url.pdf"></object>
```

`<picture>` : contains zero or more `<source>` elements and one `<img>` element to offer alternative versions of an image for different displays and devices

```html
<picture>
  <source srcset="url.jpg" media="(min-width: 800px)">
  <img src="url.jpg" alt="">
</picture>
```

`<portal>` : embed another HTML page into the current one for the purposes of allowing smoother navigation into new pages

> A `<portal>` is similar to an `<iframe>`. An `<iframe>` allows a separate browsing context to be embedded. However, the embedded content of a `<portal>` is more limited than that of an `<iframe>`. It cannot be interacted with, and therefore is not suitable for embedding widgets into a document. Instead, the `<portal>` acts as a preview of the content of another page. It can be navigated into therefore allowing for seamless transition to the embedded content.

```html
<portal src="url"></portal>
```

`<source>` : media resources for `<audio>`, `<picture>`, and `<video>` elements

```html
<video controls muted>
  <source src="url.webm" type="video/webm">
  <source src="url.mp4" type="video/mp4">
  This browser does not support the HTML5 video element.
</video>
```

### 9. SVG and MathML

*You can embed SVG and MathML content directly into HTML documents.*

`<svg>` : container that defines a new coordinate system and viewport - it is used as the outermost element of SVG documents, but it can also be used to embed an SVG fragment inside an SVG or HTML document

```html
<svg viewBox="0 0 300 100" xmlns="http://www.w3.org/2000/svg" stroke="red" fill="grey">
  <circle cx="50" cy="50" r="40" />
  <circle cx="150" cy="50" r="4" />

  <svg viewBox="0 0 10 10" x="200" width="100">
    <circle cx="5" cy="5" r="4" />
  </svg>
</svg>
```

`<math>` : MathML isntance which must not nest another `<math>` element

```html
<math>
  <mrow>
    <mrow>
      <msup>
        <mi>a</mi>
        <mn>2</mn>
      </msup>
      <mo>+</mo>
      <msup>
        <mi>b</mi>
        <mn>2</mn>
      </msup>
    </mrow>
    <mo>=</mo>
    <msup>
      <mi>c</mi>
      <mn>2</mn>
    </msup>
  </mrow>
  </math>
```

### 10. Scripting

*In order to create dynamic content and Web applications, HTML supports the use of scripting languages, most prominently JavaScript. Certain elements support this capability.*

`<canvas>` : draw graphics and animations with WebGL or Canvas Scripting API

```html
<canvas>
  An alternative text describing what your canvas displays.
</canvas>
```

```javascript
const canvas = document.querySelector('canvas');
const ctx = canvas.getContext('2d');
ctx.fillStyle = 'green';
ctx.fillRect(10, 10, 100, 100);
```

`<no-script>` : inserted if a script type on the page is unsupported or if scripting is currently turned off in the browser

```html
<noscript>
  <a href="url">...</a>
</noscript>
```

`<script>` : embed executable code or data; typically used to embed or refer to JavaScript code

```html
<!-- external -->
<script src="url.js"></script>

<!-- inline -->
<script>
  alert("...");
</script>
```

### 11. Demarcating Edits

*These elements let you provide indications that specific parts of the text have been altered.*

`<del>` : range of text that has been deleted from the document

```html
<del cite="url" datetime>...</del>
```

`<ins>` : range of text that has been added to the document

```html
<ins cite="url" datetime>...</ins>
```

### 12. Table Content

*The elements here are used to create and handle tabular data.*

`<caption>` : caption (or title) or a table

```html
<table>
  <caption>...</caption>
<table>
```

`<col>` : a column within a table  
`<col-group>` : a group of columns with a table

```html
<table>
  <colgroup>
    <col>
    <col span="#" class="...">
  </colgroup>
</table>
```

`<table>` : tabular data  
`<tr>` : a row of cells in a table  
`<thead>` : a set of rows defining the head of columns of the table  
`<th>` : a cell as a header of a group of table cells  
`<tbody>` : a set of table rows  
`<td>` : a cell that contains data  
`<tfoot>` : a set of rows summarizing the columns of the table

```html
<table>
  <thead>
    <tr>
      <th colspan="#">...</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>...</td>
      <td>...</td>
    </tr>
  </tbody>
  <tfoot>
    <tr>
      <th scope="row">...</th>
      <td>...</td>
    </tr>
  </tfoot>
</table>
```

### 13. Forms

*HTML provides a number of elements which can be used together to create forms which the user can fill out and submit to the Web site or application.*

`<button>` : clickable button

```html
<button type="button">...</button>
```

`<datalist>` : a control that provides `<option>` with recommendation  
`<optgroup>` : a grouping of `<option>` within a `<select>` element  
`<option>` : an item contained in `<select>`, `<optgroup>`, or `<datalist>`  
`<select>` : a control that provides `<option>`

```html
<!-- datalist -->
<datalist>
  <option value="...">
  <option value="...">
</datalist>

<!-- optgroup -->
<select>
  <optgroup label="...">
    <option value="...">...</option>
    <option value="...">...</option>
  </optgroup>
  <optgroup label="...">
    <option value="...">...</option>
    <option value="...">...</option>
  </optgroup>
</select>

<!-- select -->
<select>
  <option value="...">...</option>
  <option value="...">...</option>
</select>
```

`<fieldset>` : a group of several controls as well as lables with a web form  
`<legend>` : caption for the content of its parent `<fieldset>`

```html
<form>
  <fieldset>
    <legend>...</legend>

    <input>
    <input>
  </fieldset>
</form>
```

`<form>` : controls for submitting information  
`<input>` : control to accept data from a user  
`<label>` : a caption for an item

__Input Types:__ button, checkbox, color, date, datetime-local, email, file, hidden, image, month, number, password, radio, range, reset, search, submit, tel, text, time, url, week, 

```html
<form action="url" method="verb">
  <!-- label before -->
  <label for="id(a)">...</label>
  <input type="type" name="key-for-value" id="a">

  <!-- label after -->
  <input type="type" name="key-for-value" id="a">
  <label for="id(a)">...</label>

  <!-- label with nested input -->
  <label>...
    <input type="type" name="a">
  </label>
</form>
```

`<meter>` : a scalar value withina known range or a fractional value - __do not__ use to show `<progress>`

```html
<form>
  <meter min="#" max="#" low="#" high="#" optimum="#" value="#">
    at 50/100
  </meter>
<form>
```

`<output>` : container into which a site or app can inject the results of a calculation or outcome of a user action

```html
<form>
  <output for="id id..">...</output>
</form>
```

`<progress>` : indicator showing the completion progress of a task

```html
<progress max="#" value="#">...</progress>
```

`<textarea>` : a multi-line plain-text editing control

```html
<form>
  <textarea rows="#" cols="#">
    ...
  </textarea>
</form>
```

### 14. Interactive Elements

*HTML offers a selection of elements which help to create interactive user interface objects.*

`<details>` : a disclosure widget in which information is visible only when the widget is toggled into an open state  
`<summary>` : a summary, caption, or legend for `<details>`

```html
<details>
  <summary>...</summary>
    ...
</details>
```

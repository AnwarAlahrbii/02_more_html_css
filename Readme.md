
### CSS Selectors in Depth

#### CSS Selectors

1. **Element Tags** :white_check_mark:
1. **Classes & IDs** :white_check_mark:
1. Combinators
1. Attributes
1. Pseudo Classes

### Classes & IDs quick review

#### IDs

- An ID name is unique. It may only be used once on a Page
- An element may only have one ID

```html
<div id="extra-special"></div>
```

```css
#extra-special {
  ...
}
```
#### Classes

- Classes are reusable as many times as you want
- An element can have as many classes as your want

```html
<div class="big primary"></div>
```
```css
.primary {
  ...
}
.big {
  ...
}
```

#### Code Along
![code_along](https://media.git.generalassemb.ly/user/19273/files/40c4fc00-3de4-11e9-94f7-6f779d726056)
##### [Classes & IDs](starter_code/classes_and_ids/index.html)

### Combinators

#### Understanding the DOM

- The Document Object Model represents the page so that programs can change the document structure, style and content
- We can visualize our HTML as a DOM tree, sort of like a family tree visualizes the relationships between family members

#### DOM: A webpage family tree

- What are examples of siblings?
- What are examples of adjacent siblings?
- What is an example of div child?
- What is an example of a section descendant?
- What is an example of an ancestor?

![DOM tree](https://s3.amazonaws.com/media-p.slid.es/uploads/355464/images/5265506/pasted-from-clipboard.png)

#### CSS Combinations / Nested Selectors

- CSS combinations allow us to target elements on the page based on their relationship to one another
- Combinators always follow the page source order
- The target of the combinator selector is always the last element in the selector

#### Using CSS Combinators

- **Descendant** *space*: Applies to any matching descendants (**any number of levels below**) of the first selector
- **Child** `>`: Applies only to matching children (any **one level below** the first selector) of the first selector
- **General Siblings** `~`: Applies to any element that is a sibling of the first element, as long as it appears after the first element in the source order
- **Adjacent Siblings** `+`: Must be the **very next sibling** in the source order following the first selector

#### Combinators in Action

```css
/* targets paragraphs that are descendants of divs */

div p {
  color: red;
}

/* targets paragraphs that are direct children of sections */

section > p {
  color: blue;
}

/* targets paragraphs that are adjacent siblings of another paragraphs */

p + p {
  background-color: yellow;
}

/* targets paragraphs that are siblings of divs */

div ~ p {
  background-color: orange;
}
```

**HEADS UP:** It's always the **last** element that we're targeting

#### Code Along
![code_along](https://media.git.generalassemb.ly/user/19273/files/40c4fc00-3de4-11e9-94f7-6f779d726056)
##### [Using Combinators / Nested Selectors](starter_code/nested_selectors/index.html)

***

### Attributes

#### Attribute Selectors

- Attributes let us target elements by their attributes
- The main syntx for attributes is:
```css
[attribute="value"] {
  /* styles here */
}
```

#### Targeting Attributes

```css
/* Target the attribute that contains a value */

[title-="flower"] {
  /* styles for elements with title="flower" or title="Summer Flower" */

/* Target the attributes that start with a value */

[href^="http://"] {
  /* styles for anchors that link to external addresses */
}

/* Target the attribute that ends with a value */

[class$="-box"] {
  /* matches classes like large-box and small-box */
}
```

***


### Pseudo Classes

#### Pseudo Classes
- A CSS Pseudo-class is a keyword added to a selectors that specifies a special state of the selected element(s)
- For Example, when an element is being hovered over, or when it is the first or last element in it's parent

#### First-Child

```css
/* Selects any <p> that is the first element among its Siblings */

p:first-child {
  color: lime;
}

```

- The element matching the selector **must** be the first element inside its parent
- There's a corresponding last-children

#### First-of-type

```css
/* Selects any <p> that is the first element of its type among its Siblings */

p:first-of-type {
  color: red;
}

```
- Unlike the first-child, this element can be anywhere in the source order among its siblings so long as it is the first instance of that type of elements
- There are last-of-type and only-of-type as well

#### Not

```css
/* Selects any element that has a class of blue and it NOT a paragraph */

.blue:not(p) {
  color: blue;
}

```
- The not pseudo class can be used on its own or in combination with other Selectors

#### Hover

```css
/* Selects any <img> element when "hovered" */

.img:hover {
  border: 5px solid blue
}

```
- The hover pseudo class allows for powerful interactions without JavaScript!

#### Nth-child & Nth-of-type

```css
/* Selects the 2nd, 4th, 6th, ... div among any group of siblings */

div:nth-child(even) {
  color: lime;
}

/* Selects the 1st, 4th, 7th, 10th ... div among any group of siblings */

div:nth-child(3n+1) {
  color: lime;
}

```
- The value in the paren can be **even**, **odd**, or a formula in the form of **An+b**
- The formula is calculated with every value of n starting at 0. So (3*0)+1 = **1**, (3*1)+1=**4**, (3*2)+1=**7**, etc.
- To select just the 3rd element use`:nth-child(3)`

#### Code Along
![code_along](https://media.git.generalassemb.ly/user/19273/files/40c4fc00-3de4-11e9-94f7-6f779d726056)
##### [Attributes and Pseudo Classes](starter_code/attributes_and_pseudo_classes/index.html)

***

### Cascading & inheritance

#### Cascading & inheritance
- Many CSS properties inherit their values from their ancestors and most accept a value of **inherit**
- Properties can be overridden when you provide a rule that has more **specificity**
- Any rules that **are not specifically overridden** continue to be inherited

#### Specificity

Specificity is a calculation based on the selectors used. Each type of selector is weighted:

1. Inline Styles (highest)
1. IDs
1. Classes & attributes
1. Element Tags (lowest)

#### Calculating Specificity

```css
#main-nav > a.nav-item {
  background-color: red;
}
/*
inline - 0
id - 1
class - 1
element - 1
*/

header > nav .nav-item {
 background-color: blue;
}
/*
inline - 0
id - 0
class - 1
element - 2
*/

header nav#main-nav > a.nav-item {
  background-color: yellow;
}
/*
inline - 0
id - 1
class - 1
element - 3


WINNER
*/
```

#### When Specificity Matters

- When there are multiple rules that contradict one another, the specificity is calculated to determine which is applied
- For identically weighted rules, the last declaration for wins!
- Inline styles trump **almost** all others
- One exception is the special `!important` attribute

***

### Reseting CSS

- Due to browsers having their own styles by default, we can have a stylesheet to reset all browsers
- [CSS Reset](https://meyerweb.com/eric/tools/css/reset/)

```css
/* http://meyerweb.com/eric/tools/css/reset/
   v2.0 | 20110126
   License: none (public domain)
*/

html, body, div, span, applet, object, iframe,
h1, h2, h3, h4, h5, h6, p, blockquote, pre,
a, abbr, acronym, address, big, cite, code,
del, dfn, em, img, ins, kbd, q, s, samp,
small, strike, strong, sub, sup, tt, var,
b, u, i, center,
dl, dt, dd, ol, ul, li,
fieldset, form, label, legend,
table, caption, tbody, tfoot, thead, tr, th, td,
article, aside, canvas, details, embed,
figure, figcaption, footer, header, hgroup,
menu, nav, output, ruby, section, summary,
time, mark, audio, video {
	margin: 0;
	padding: 0;
	border: 0;
	font-size: 100%;
	font: inherit;
	vertical-align: baseline;
}
/* HTML5 display-role reset for older browsers */
article, aside, details, figcaption, figure,
footer, header, hgroup, menu, nav, section {
	display: block;
}
body {
	line-height: 1;
}
ol, ul {
	list-style: none;
}
blockquote, q {
	quotes: none;
}
blockquote:before, blockquote:after,
q:before, q:after {
	content: '';
	content: none;
}
table {
	border-collapse: collapse;
	border-spacing: 0;
}
```

***
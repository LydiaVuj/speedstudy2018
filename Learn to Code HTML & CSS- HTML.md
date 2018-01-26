#Learn to Code HTML & CSS

## Common HTML terms

1. Elements ```<a>```
2. Tags ```<div></div>```
3. Attributes - ```href/id/class```
4. Self-Closing Elements:
<br> <embed> <hr> <img> <input> <link> <meta> <param> <source> <wbr>

## Common CSS Terms

1. Selectors - ```p{....}```
2. Properties 
```
p {
    color: ...;
    font-size: ...;
    } 
```
3. Values
```
 p {
  color: orange;
  font-size: 16px;
}
```
* Type selectors- targeting the element type
* Class selectors - targeting based on ```class``` attribute
* ID selectors - targeting only one unique element based on ```id``` attribute

## Referencing CSS
```
<head>
  <link rel="stylesheet" href="main.css">
</head>
```

## CSS Resets
* CSS resets take every common HTML element with a predefined style and provide one unified style for all browsers. These resets generally involve removing any sizing, margins, paddings, or additional styles and toning these values down. Because CSS cascades from top to bottom—more on that soon—our reset needs to be at the very top of our style sheet. Doing so ensures that those styles are read first and that all of the different web browsers are working from a common baseline.


# Getting to Know HTML

## Identifying Divisions & Spans

* Divisions, or <div>s, and <span>s are HTML elements that act as containers solely for styling purposes
* Block vs. Inline Elements
    
 **Block-level elements** begin on a new line, stacking one on top of the other, and occupy any available width. Block-level elements may be nested inside one another and may wrap inline-level elements. We’ll most commonly see block-level elements used for larger pieces of content, such as paragraphs.

**Inline-level** elements do not begin on a new line. They fall into the normal flow of a document, lining up one after the other, and only maintain the width of their content. Inline-level elements may be nested inside one another; however, they cannot wrap block-level elements. We’ll usually see inline-level elements with smaller pieces of content, such as a few words.

* A ```<div>``` is a block-level element that is commonly used to identify large groupings of content, and which helps to build a web page’s layout and design. A ```<span>```, on the other hand, is an inline-level element commonly used to identify smaller groupings of text within a block-level element.

## Using Text-Based Elements

* ***Headings*** Headings are block-level elements, and they come in six different rankings, ```<h1>``` through  ```<h6>```. Headings help to quickly break up content and establish hierarchy, and they are key identifiers for users reading a page. They also help search engines to index and determine the content on a page

* ***Paragraphs*** paragraphs are defined using the ```<p>``` block-level element. Paragraphs can appear one after the other, adding information to a page as desired.
    
* ***Bold Text with Strong*** There are two elements that will bold text for us: the ```<strong>``` and ```<b>``` elements.The ```<strong```> element is semantically used to give strong importance to text, and is thus the most popular option for bolding text. The ```<b>``` element, on the other hand, semantically means to stylistically offset text, which isn’t always the best choice for text deserving prominent attention. We have to gauge the significance of the text we wish to set as bold and to choose an element accordingly.
    
* ***Italicize Text with Emphasis*** The ```<em>``` element is used semantically to place a stressed emphasis on text; it is thus the most popular option for italicizing text. The other option, the ```<i>``` element, is used semantically to convey text in an alternative voice or tone, almost as if it were placed in quotation marks.
    
## Building Structure

* ***Header*** The ```<header>```element, like it sounds, is used to identify the top of a page, article, section, or other segment of a page. In general, the ```<header>``` element may include a heading, introductory text, and even navigation
    
* ***Navigation*** The ```<nav>``` element identifies a section of major navigational links on a page. The <nav> element should be reserved for primary navigation sections only, such as global navigation, a table of contents, previous/next links, or other noteworthy groups of navigational links.
    
* ***Article*** The ```<article>``` element is used to identify a section of independent, self-contained content that may be independently distributed or reused. We’ll often use the ```<article>``` element to mark up blog posts, newspaper articles, user-submitted content, and the like.
    
* ***Section*** The ```<section>``` element is used to identify a thematic grouping of content, which generally, but not always, includes a heading. The grouping of content within the <section> element may be generic in nature, but it’s useful to identify all of the content as related.
    
* ***Deciding Between ```<article>, <section>, or <div>``` Elements*** If the content adds to the document outline and it can be independently redistributed or syndicated, use the <article> element.
If the content adds to the document outline and represents a thematic group of content, use the ```<section>``` element. 
    
* ***Aside*** The ```<aside>``` element holds content, such as sidebars, inserts, or brief explanations, that is tangentially related to the content surrounding it. 
    
* ***Footer*** The ```<footer>``` element identifies the closing or end of a page, article, section, or other segment of a page. Generally the <footer> element is found at the bottom of its parent. Content within the ```<footer>``` element should be relative information and should not diverge from the document or section it is included within.
    
## Creating Hyperlinks

* Hyperlinks are established using the anchor, ```<a>```, inline-level element. In order to create a link from one page (or resource) to another, the href attribute, known as a hyperlink reference, is required. The href attribute value identifies the destination of the link.

* ***Wrapping Block-Level Elements with Anchors*** By nature the anchor element, ```<a>```, is an inline element, and, according to web standards, inline-level elements may not wrap block-level elements. With the introduction of HTML5, however, anchor elements specifically have permission to wrap either block-, inline-, or any other level elements. This is a break from the standard convention, but it’s permissible in order to enable entire blocks of content on a page to become links
    
* ***Relative & Absolute Paths*** Links pointing to other pages of the same website will have a _relative path_, which does not include the domain (.com, .org, .edu, etc.) in the href attribute value. Because the link is pointing to another page on the same website, the href attribute value needs to include only the filename of the page being linked to: about.html, for example.

Should the page being linked to reside within a different directory, or folder, the href attribute value needs to reflect this as well. Say the about.html page resides within the pages directory; the relative path would then be pages/about.html.

Linking to other websites outside of the current one requires an _absolute path_, where the href attribute value must include the full domain. A link to Google would need the href attribute value of http://google.com, starting with http and including the domain, .com in this case

* ***Linking to an Email Address*** To create an email link, the href attribute value needs to start with mailto: followed by the email address to which the email should be sent. To create an email link to shay@awesome.com, for example, the href attribute value would be mailto:shay@awesome.com.

Additionally, subject, body text, and other information for the email may be populated. To add a subject line, we’ll include the subject= parameter after the email address. The first parameter following the email address must begin with a question mark, ?, to bind it to the hyperlink path. Multiple words within a subject line require that spaces be encoded using %20.

Adding body text works in the same way as adding the subject, this time using the body= parameter in the href attribute value. Because we are binding one parameter to another we need to use the ampersand, &, to separate the two. As with the subject, spaces must be encoded using %20, and line breaks must be encoded using %0A.

Altogether, a link to shay@awesome.com with the subject of “Reaching Out” and body text of “How are you” would require an href attribute value of mailto:shay@awesome.com?subject=Reaching%20Out&body=How%20are%20you.

* ***Opening Links in a New Window*** To trigger the action of opening a link in a new window, use the target attribute with a value of _blank_. The target attribute determines exactly where the link will be displayed, and the _blank_ value specifies a new window.
Exm: ```<a href="http://shayhowe.com/" target="_blank">Shay Howe</a>```

* ***Linking to Parts of the Same Page*** Using the “Back to top” link as an example, we can place an id attribute value of top on the <body> element. Now we can create an anchor element with an href attribute value of #top, pound sign and all, to link to the beginning of the <body> element.
    ```<body id="top">
  ...
  <a href="#top">Back to top</a>
  ...
</body>
```

# Getting to Know CSS

## The Cascade

* Within CSS, all styles cascade from the top of a style sheet to the bottom, allowing different styles to be added or overwritten as the style sheet progresses. The cascade also works with ***properties*** inside individual selectors. 

* Every selector (the type, class, and ID ) in CSS has a specificity weight. A selector’s specificity weight, along with its placement in the cascade, identifies how its styles will be rendered.

_Specifity Weight_
1. The type selector has the lowest specificity weight and holds a point value of 0-0-1.
2. The class selector has a medium specificity weight and holds a point value of 0-1-0. 
3. The ID selector has a high specificity weight and holds a point value of 1-0-0

* As we can see, specificity points are calculated using three columns. The first column counts ID selectors, the second column counts class selectors, and the third column counts type selectors.

* The higher the specificity weight of a selector, the more superiority the selector is given when a styling conflict occurs.

## Combining Selectors

* When selectors are combined they should be read from right to left. The selector farthest to the right, directly before the opening curly bracket, is known as the key selector. The key selector identifies exactly which element the styles will be applied to. Any selector to the left of the key selector will serve as a prequalifier.

_Specificity Within Combined Selectors_
 * When selectors are combined, so are the specificity weights of the individual selectors. These combined specificity weights can be calculated by counting each different type of selector within a combined selector.
 
 Example: 
 The second selector, .hotdog p.mustard, had two class selectors and one type selector. Combined, the selector has a specificity point value of 0-2-1. The 0 in the first column is for zero ID selectors, the 2 in the second column is for two class selectors, and the 1 in the last column is for one type selector.
 
 ## Layering Styles with Multiple Classes
 
 * One way to keep the specificity weights of our selectors low is to be as modular as possible, sharing similar styles from element to element. And one way to be as modular as possible is to layer on different styles by using multiple classes.
 
 * Let’s take a look at buttons, for example. Say we want all of our buttons to have a font size of 16 pixels, but we want the background color of our buttons to vary depending on where the buttons are used. We can create a few classes and layer them on an element as necessary to apply the desired styles.
 
 HTML
 
 ```
 <a class="btn btn-danger">...</a>
<a class="btn btn-success">...</a>
```

CSS

```
.btn {
  font-size: 16px;
}
.btn-danger {
  background: red;
}
.btn-success {
  background: green;
}
```

## css-property-values
***color***
four primary ways to represent sRGB colors within CSS: keywords, hexadecimal notation, and RGB and HSL values.

_Keyword Colors_
Keyword color values are names (such as red, green, or blue) that map to a given color. These keyword names and their corresponding colors are determined by the CSS specification.

_Hexadecimal Colors_
Hexadecimal color values consist of a pound, or hash, #, followed by a three- or six- character figure. The figures use the numbers 0 through 9 and the letters a through f, upper or lower case. These values map to the red, green, and blue color channels.

_RGB & RGBa Colors_
The function accepts three comma-separated values, each of which is an integer from 0 to 255. A value of 0 would be pure black; a value of 255 would be pure white.

_HSL & HSLa Colors_
HSL color values are stated using the hsl() function, which stands for hue, saturation, and lightness. Within the parentheses, the function accepts three comma-separated values, much like rgb().

The first value, the hue, is a unitless number from 0 to 360. The numbers 0 through 360 represent the color wheel, and the value identifies the degree of a color on the color wheel.

The second and third values, the saturation and lightness, are percentage values from 0 to 100%. The saturation value identifies how saturated with color the hue is, with 0 being grayscale and 100% being fully saturated. The lightness identifies how dark or light the hue value is, with 0 being completely black and 100% being completely white.

***Lenght***
Length values come in two different forms, absolute and relative, each of which uses different units of measurement.

_Absolute Lengths_
Absolute length values are the simplest length values, as they are fixed to a physical measurement, such as inches, centimeters, or millimeters. The most popular absolute unit of measurement is known as the pixel and is represented by the px unit notation.

_Relative Lengths_
In addition to absolute length values, there are also relative length values. Relative length values are a little more complicated, as they are not fixed units of measurement; they rely on the length of another measurement.

* Percentages - Percentage lengths are defined in relation to the length of another object. For example, to set the width of an element to 50%, we have to know the width of its parent element, the element it is nested within, and then identify 50% of the parent element’s width.

* Em - The em unit is represented by the em unit notation, and its length is calculated based on an element’s font size.
A single em unit is equivalent to an element’s font size. So, for example, if an element has a font size of 14 pixels and a width set to 5em, the width would equal 70 pixels (14 pixels multiplied by 5).

When a font size is not explicitly stated for an element, the em unit will be relative to the font size of the closest parent element with a stated font size.

# Opening the Box Model

***Display***

* Every element has a default display property value; however, as with all other property values, that value may be overwritten. There are quite a few values for the display property, but the most common are block, inline, inline-block, and none.
1. A value of block will make that element a block-level element.
2.A value of inline will make that element an inline-level element.
3.inline-block value. Using this value will allow an element to behave as a block-level element, accepting all box model properties (which we’ll cover soon). However, the element will be displayed in line with other elements, and it will not begin on a new line by default.
4. A value of none -  will completely hide an element and render the page as if that element doesn’t exist. Any elements nested within this element will also be hidden.

## What Is the Box Model?

* According to the box model concept, every element on a page is a rectangular box and may have width, height, padding, borders, and margins.

* The core of the box is defined by the width and height of an element, which may be determined by the display property, by the contents of the element, or by specified width and height properties. padding and then border expand the dimensions of the box outward from the element’s width and height. Lastly, any margin we have specified will follow the border.

_Width & Height_
Every element has default width and height. That width and height may be 0 pixels, but browsers, by default, will render every element with size. Depending on how an element is displayed, the default width and height may be adequate. If an element is key to the layout of a page, it may require specified width and height property values. In this case, the property values for non-inline elements may be specified.

1. Width - The default width of an element depends on its display value. Block-level elements have a default width of 100%, consuming the entire horizontal space available. Inline and inline-block elements expand and contract horizontally to accommodate their content. Inline-level elements cannot have a fixed size, thus the width and height properties are only relevant to non-inline elements. To set a specific width for a non-inline element, use the width property:

2. Height - The default height of an element is determined by its content. An element will expand and contract vertically as necessary to accommodate its content. To set a specific height for a non-inline element, use the height property:

_Margin & Padding_
Depending on the element, browsers may apply default margins and padding to an element to help with legibility and clarity. We will generally see this with text-based elements. The default margins and padding for these elements may differ from browser to browser and element to element.

1.Margin - The margin property allows us to set the amount of space that surrounds an element. Margins for an element fall ***outside*** of any border and are completely transparent in color. Margins can be used to help position elements in a particular place on a page or to provide breathing room, keeping all other elements a safe distance away.

2.Padding - The padding property is very similar to the margin property; however, it falls ***inside*** of an element’s border, should an element have a border. The padding property is used to provide spacing directly within an element. 

* *Margin & Padding on Inline-Level Elements*
Inline-level elements are affected a bit differently than block and inline-block elements when it comes to margins and padding. Margins only work horizontally—left and right—on inline-level elements. Padding works on all four sides of inline-level elements; however, the vertical padding—the top and bottom—may bleed into the lines above and below an element.

Margins and padding work like normal for block and inline-block elements.

* *Margin & Padding Declarations* 
 * The margin and padding properties come in both longhand and shorthand form. When using the shorthand margin property to set the same value for all four sides of an element, we specify one value.  `margin: 20px;`

To set one value for the top and bottom and another value for the left and right sides of an element, specify two values: top and bottom first, then left and right. Here we are placing margins of 10 pixels on the top and bottom of a <div> and margins of 20 pixels on the left and right `margin: 10px 20px;`
  
To set unique values for all four sides of an element, specify those values in the order of top, right, bottom, and left, moving clockwise. `margin: 10px 20px 0 15px;`

* With longhand, we can set the value for one side at a time using unique properties. Each property name (in this case margin or padding) is followed by a dash and the side of the box to which the value is to be applied: top, right, bottom, or left. For example, the padding-left property accepts only one value and will set the left padding for that element; the margin-top property accepts only one value and will set the top margin for that element:
`
margin-top: 10px;
  padding-left: 6px;
 `
* Colors* - For margins, we see the background color of the parent element, and for padding, we see the background color of the element the padding is applied to.

_Borders_

* Borders fall between the padding and margin, providing an outline around an element. The border property requires three values: width, style, and color. 
- Shorthand values for the border property are stated in that order—width, style, color. 
-In longhand, these three values can be broken up into the border-width, border-style, and border-color properties. These longhand properties are useful for changing, or overwriting, a single border value.

* Borders Style - The most common style values are solid, double, dashed, dotted, and none, but there are several others to choose from.
`border: 6px solid #949599;`

_Individual Border Sides_
As with the margin and padding properties, borders can be placed on one side of an element at a time if we’d like. Doing so requires new properties: border-top, border-right, border-bottom, and border-left.

_Border Radius_
- Property which enables us to round the corners of an element
- The border-radius property accepts length units, including percentages and pixels, that identify the radius by which the corners of an element are to be rounded. A single value will round all four corners of an element equally; two values will round the top-left/bottom-right and top-right/bottom-left corners in that order; four values will round the top-left, top-right, bottom-right, and bottom-left corners in that order.

* ****Box Sizing***

The box model may, however, be changed to support different calculations. CSS3 introduced the box-sizing property, which allows us to change exactly how the box model works and how an element’s size is calculated. The property accepts three primary values—content-box, padding-box, and border-box—each of which has a slightly different impact on how the box size is calculated.

_Content Box_
The content-box value is the default value, leaving the box model as an additive design. If we don’t use the box-sizing property, this will be the default value for all elements. The size of an element begins with the width and height properties, and then any padding, border, or margin property values are added on from there

_Padding Box_
The padding-box value alters the box model by including any padding property values within the width and height of an element. When using the padding-box value, if an element has a width of 400 pixels and a padding of 20 pixels around every side, the actual width will remain 400 pixels. As any padding values increase, the content size within an element shrinks proportionately.

**As the CSS specification has evolved, the padding-box value for the box-sizing property has been deprecated and should not be used.**

_Border Box_
The border-box value alters the box model so that any border or padding property values are included within the width and height of an element. When using the border-box value, if an element has a width of 400 pixels, a padding of 20 pixels around every side, and a border of 10 pixels around every side, the actual width will remain 400 pixels.
If we add a margin, those values will need to be added to calculate the full box size. No matter which box-sizing property value is used, any margin values will need to be added to calculate the full size of the element.

* ***Picking a Box Size***

Generally speaking, the best box-sizing value to use is border-box. The border-box value makes our math much, much easier. If we want an element to be 400 pixels wide, it is, and it will remain 400 pixels wide no matter what padding or border values we add to it.


















 









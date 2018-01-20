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








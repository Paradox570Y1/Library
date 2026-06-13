A **semantic tag** in HTML is an element that clearly describes its meaning in both the structure of the document and its content. These tags make the webpage more understandable to both humans and machines (like search engines and screen readers).

`<header>, <footer>, <article>, <section>, <main>`
Use these for better structure and SEO.
#SEO
- The full form of **SEO** is **Search Engine Optimization**.
- It refers to the practice of optimizing a website or web content to improve its visibility and ranking on search engine results pages (SERPs).

#Header
**Role**: The `<header>` tag represents the introductory content or a set of navigational links for a section or the entire webpage. It is typically used to contain the logo, navigation bar, introductory text, or any content that is generally placed at the top of a webpage or a specific section.

#footer
**Role**: The `<footer>` tag defines the footer of a page or section. It contains information about the page or the website, such as copyright notices, contact information, social media links, or any other relevant details that should appear at the bottom.

#article
**Role**: The `<article>` tag represents a self-contained piece of content that could stand alone or be distributed independently, such as a blog post, news article, or forum post. It should be able to make sense by itself, even if it is removed from the context of the webpage(e.g., blog posts, news articles).

```html
<article>
  <h2>Breaking News: New Tech Innovations</h2>
  <p>Today, several new tech innovations were unveiled at the tech conference...</p>
</article>
```
**Explanation**: The `<article>` element contains a headline (`<h2>`) and content (`<p>`), which can be viewed independently of other content.

#section
**Role**: The `<section>` tag represents a thematic grouping of content within a document, typically with a heading (`<h1>` to `<h6>`). It divides a page into sections or areas, each containing a specific topic or functionality.


#main
**Role**: The `<main>` tag represents the main content of the document, excluding content that is repeated across pages such as headers, footers, or navigation. It is intended to contain content that is directly related to or expands on the central topic of the page.

**Common Use**: Used to wrap the main content of the page, such as articles, blogs, or other major sections of the content that are central to the page's purpose.

```html
<main>
  <h1>Welcome to Our Website</h1>
  <p>This is the central content of the website...</p>
</main>
```
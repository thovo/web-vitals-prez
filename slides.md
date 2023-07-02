---
theme: default
background: https://source.unsplash.com/collection/94734566/1920x1080
class: text-center
highlighter: shiki
lineNumbers: false
info: |
  ## Slidev Starter Template
  Presentation slides for developers.

  Learn more at [Sli.dev](https://sli.dev)
drawings:
  persist: false
transition: slide-left
title: Top core web vitals recommendation for 2023
---

# Top core web vitals recommendation for 2023

Explain to you like you are 5 years old(I tried but maybe we should fix at 22 years old)

<!--
The last comment block of each slide will be treated as slide notes. It will be visible and editable in Presenter Mode along with the slide. [Read more in the docs](https://sli.dev/guide/syntax.html#notes)
-->

---

# You don't need to stay through this presentation

- If you are busy, you just need to read through these links:
    - [Our top Core Web Vitals recommendations for 2023](https://web.dev/top-cwv-2023/)
    - [Top Core Web Vitals Recommendations for 2023 — Barry Pollard — We Love Speed 2023](https://www.youtube.com/watch?v=fJrKeh-Np8c&ab_channel=WeLoveSpeed)
- If you stay and go through these next slides, I will try to answer you 3 questions: What is it?/Why should we do it?/How to do it? :
    - Largest Contentful Paint(LCP)
    - Cumulative Layout Shift(CLS)
    - First Input Delay(FID)

---
layout: image-left

image: ./images/lcp.svg

class: right-content
---
# LCP - What?

- The Largest Contentful Paint (LCP) metric reports the render time of **the largest image or text block visible within the viewport**, relative to **when the page first started loading**.
- *Simple explanation for a kid*: When you first time see your crush, the largest impression(*content*) may be his/her eyes(*image*) or his/her voice(*text*). The first impression may impact your feeling(*your user*) forever.

---
layout: two-cols
---
# LCP - Example - Ekino site in mobile view

Question: Do you know what is the LCP part ? 

Answer: 

<div v-click>
  The blue part which is an image is considered as the current LCP.
</div>

::right::
<div class="container">
  <img src="images/lcp-ekino-mobile.png" class="w-9/12 object-contain"/>
</div>

---
layout: two-cols
---

# LCP - Elements to be considered

- <span class="inline-code">img</span> elements
- <span class="inline-code">image</span> elements inside an <span class="inline-code">svg</span> element
- <span class="inline-code">video</span> elements with a poster image (the poster image load time is used)
- An element with a background image loaded via the <span class="inline-code">url()</span> function (as opposed to a CSS gradient)
- Block-level elements containing text nodes or other inline-level text elements children.

::right::

<div class="h-100 w-100 flex justify-center items-center flex-col m-2 p-5 rounded bg-green-500 bg-opacity-50 font-sans text-2xl text-gray-500">
  <p>Not every element has been equal considered, but every element will have the opportunity to be considered</p>
  <p class="italic font-bold">Not John F.Kennedy</p>
</div>

<style>
.inline-code {
  @apply text-red-500 dark:text-red-400 bg-gray-100 p-1 rounded font-sans bg-opacity-50;
}
</style>

---
layout: two-cols
---

# LCP - Elements to be ignored

- Elements with an opacity of 0, that are invisible to the user
- Elements that cover the full viewport, that are likely considered as background rather than content
- Placeholder images or other images with a low entropy, that likely do not reflect the true content of the page

::right::

<div class="h-100 w-100 flex justify-center items-center flex-col m-2 p-5 rounded bg-green-500 bg-opacity-50 font-sans text-2xl text-gray-500">
  <p>Not every element has been equal considered, but every element will have the opportunity to be considered</p>
  <p class="italic font-bold">Not John F.Kennedy</p>
</div>

---
layout: image

image: ./images/alexander-mils-lCPhGxs7pww-unsplash.jpg

---

# LCP/CLS/FID - Why?
<div class="bg-opacity-50 bg-light-600 text-dark-500 p-2 mb-2 rounded">

Cases studies:
- [Carpe improved **LCP by 52%** and **CLS by 41%**:**10% increase in traffic**, **5% increase conversion rate**, and **15% increase in revenue**.](https://performance.shopify.com/blogs/blog/how-carpe-achieved-record-breaking-sales-by-focusing-on-performance-optimization)
- [Sunday Citizen improve **25% in LCP** and **61% in CLS**:**4% decrease in bounce rate** and over **6% increase in conversion**.](https://performance.shopify.com/blogs/blog/how-sunday-citizen-improved-conversions-by-focusing-on-performance)
- [Groupe Renault improve **1 second improvement**: **14% point decrease in bounce rate**, and **13% increase in conversions**.](https://web.dev/renault/)
- [Swappie improved **LCP by 55%**, **CLS by 91%** and **FID by 90%**: **42% increase in mobile revenue** and a **10% point increase in relative mobile conversion rate**.](https://web.dev/swappie/)

For more cases studies, read [here](https://wpostats.com/?sjid=15479569239720511772-EU)

</div>
<div class="citation bg-light-600 text-dark-500 text-md p-1 rounded font-sans bg-opacity-50">
  Photo by <a href="https://unsplash.com/@alexandermils?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Alexander Mils</a> on <a href="https://unsplash.com/fr/s/photos/increase-money?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Unsplash</a>
</div>

---
layout: image-right

image: ./images/how.png
---

# LCP - How ?

- Ensure the LCP resource is discoverable from the HTML source
- Ensure the LCP resource is prioritized
- Use a CDN to optimize document and resource TTFB

---

# LCP - Ensure the LCP resource is discoverable from the HTML source

> According to the 2022 Web Almanac by HTTP Archive, 72% of mobile pages have an image as their LCP element 
> -- <cite>[Our top Core Web Vitals recommendations for 2023][1]</cite>

Make sure your image got discoverable by user's browser
- Load the image using an <span class="inline-code">img</span> element with the <span class="inline-code">src</span> or <span class="inline-code">srcset</span> attribute.
- Prefer server-side rendering (SSR) over client-side rendering (CSR)
- If your image needs to be referenced from an external CSS or JS file, you can still include it in the HTML source via a <span class="inline-code"><link rel="preload"></span> tag

```html
<link rel="preload" href="an-image-800w.jpg" as="image">
<img
  srcset="an-image-480w.jpg 480w, an-image-800w.jpg 800w"
  src="an-image-800w.jpg"
  alt="An image" />
```

[1]: https://web.dev/top-cwv-2023/
<style>
.inline-code {
  @apply text-red-500 dark:text-red-400 bg-gray-100 p-1 rounded font-sans bg-opacity-50;
}
</style>

---

# LCP - Ensure the LCP resource is prioritized

Even we already applied the code in previous slide, our LCP image may not be loaded faster than other resources, so how should we make it get more prioritized

- Add <span class="inline-code">fetchpriority="high"</span> to the <span class="inline-code">img</span> tag of your LCP image. 
- Never set <span class="inline-code">loading="lazy"</span> on the <span class="inline-code">img</span> tag of your LCP image.
- Defer non-critical resources when possible.

```html
<link rel="preload" href="an-image-800w.jpg" as="image" fetchpriority="high">
<img
  srcset="an-image-480w.jpg 480w, an-image-800w.jpg 800w"
  src="an-image-800w.jpg"
  fetchpriority="high"
  alt="An image" />
<ul class="carousel">
    <img src="img/carousel-1.jpg" fetchpriority="high">
    <img src="img/carousel-2.jpg" fetchpriority="low">
    <img src="img/carousel-3.jpg" fetchpriority="low">
    <img src="img/carousel-4.jpg" fetchpriority="low">
</ul>
```

<style>
.inline-code {
  @apply text-red-500 dark:text-red-400 bg-gray-100 p-1 rounded font-sans bg-opacity-50;
}
</style>

---

# LCP - Use a CDN to optimize document and resource TTFB

We make the resources discoverable and prioritized. Now we need to deliver theses resources as fast as possible. The browser will not do anything until it received the first byte of the initial HTML document response, or we can call it Time to First Byte (TTFB). To do it, we serve the content through the CDN:

- Serve your content as geographically close to your users as possible
- Cache that content so recently-requested content can be served again quickly.
- CDN can host not only static assets but also HTML documents(included also dynamical generated one)

---
layout: image-left

image: ./images/cls.svg

class: right-content
---
# CLS - What?

- Cumulative Layout Shift (CLS) is an important, user-centric metric for measuring **visual stability** because it helps quantify how often users experience unexpected layout shifts—a low CLS helps ensure that the page is delightful.
- *Simple explanation for a kid*: When you throw a ball(*a user action*) to your friend but he ducks(*layout shift*) and the ball hit your crush(*wrong action*). This will not be a happy ending(*bad user experience*).

---

# CLS - Example - Layout shift makes wrong click

A screencast illustrating how layout instability can negatively affect users.

<div class="container flex justify-center">
  <video autoplay="" controls="" height="400" loop="" muted="" width="500">
    <source type="video/webm; codecs=vp8" src=" images/layout-instability2.webm">
  </video>
</div>

<div class="citation bg-light-600 text-dark-500 text-md p-1 rounded font-sans bg-opacity-50">
 Video from <a href="https://web.dev/cls/">Web.dev Cumulative Layout Shift (CLS)</a>
</div>

---
layout: image-right

image: ./images/how2.png
---

# CLS - How ?

- Set explicit sizes on any content loaded from the page
- Ensure pages are eligible for bfcache
- Avoid animations/transitions that use layout-inducing CSS properties

--- 

# CLS - Set explicit sizes on any content loaded from the page

> According to HTTP Archive, 72% of pages have at least one unsized image 
> -- <cite>[Our top Core Web Vitals recommendations for 2023][1]</cite>

To fix layout shifts caused by unsized images/videos/third-party ads is to explicitly set width and height attributes (or equivalent CSS properties). If we don't know the real height of the content, make a container with min-height may help to reduce a little layout shift to an acceptable tolerant.

```html
<img
  src="an-image-800w.jpg" width="800" height="600"
  alt="A big image may cause layout shift" />
<video width="1600" height="900"></video>
<div class="ad-container" style="min-height: 500px">
  Your ad goes here
</div>
```

[1]: https://web.dev/top-cwv-2023/#set-explicit-sizes-on-any-content-loaded-from-the-page


---

# CLS - Ensure pages are eligible for bfcache

Back/forward cache (or bfcache) is a browser optimization that enables instant back and forward navigation.

> bfcache is an in-memory cache that stores a complete snapshot of a page (including the JavaScript heap) as the user is navigating away. With the entire page in memory, the browser can quickly and easily restore it if the user decides to return.
> -- <cite>[Back/forward cache][1]</cite>

As a site owner, you should always check your site to be eligible for bfcache, and if not, read the reason and find a way to optimize it. Unless your site contain sensitive information(as bank information, transaction, user account), you should strive to have bfcache active.

[1]: https://web.dev/bfcache/

---

# CLS - Example between with and without bfcache

<Youtube id="cuPsdRckkF0" width="800" height="400"/>

---

# CLS - Avoid animations/transitions that use layout-inducing CSS properties

When element got animated, you may not notice but it can be a reason for layout shift. Animate or transition any CSS property that requires the browser to update the page layout will cause layout shift.

```css
span {
  margin: 10px;
  padding: 10px;
  position: absolute;
  top: 10px;
  left: 10px;
  right: 10px;
  bottom: 10px;
}
```

Layout shift will also happen with element bring out of the document flow like element with <span class="inline-code">position: absolute</span>. Always prefer to use <span class="inline-code">transform</span> property.

You can read more in 
[Avoid non-composited animations](https://developer.chrome.com/docs/lighthouse/performance/non-composited-animations/)

<style>
.inline-code {
  @apply text-red-500 dark:text-red-400 bg-gray-100 p-1 rounded font-sans bg-opacity-50;
}
</style>

---
layout: image-left

image: ./images/fid.svg

class: right-content
---
# FID - What?

- First Input Delay (FID) is a Core Web Vitals metric that **captures a user's first impression of a site's interactivity and responsiveness**. It measures the time from when a user first interacts with a page to the time when the browser is actually able to respond to that interaction.
- *Simple explanation for a kid*: When your mother(*your user*) ask your father(*your site*) a question about why did he come home late, if your father(*your site*) can't response quick enough, someone will have harsh time.

---
layout: image-right

image: ./images/how3.png
---

# FID - How?

- Avoid or break up long tasks
- Avoid unnecessary JavaScript
- Avoid large rendering updates

---

# FID - Avoid or break up long tasks

Don't block the main thread. And if you can't avoid long task, it is better to break it up to many smaller tasks.

> When tasks stretch beyond a certain point—50 milliseconds to be exact—they're classified as long tasks.
> -- <cite>[Optimize long tasks][1]</cite>

<img src="images/break-up-small-tasks.avif" width="600"/>

By breaking up into smaller tasks, you stop blocking the main thread so the user can interact normally.

[1]: https://web.dev/optimize-long-tasks/

---

# FID - Avoid unnecessary JavaScript

A large JS file may have a lot of unused function, or wait to be used. How should we deliver a better file?

- Use any coverage tool to find out unused code, remove it to save time
- The unused code may be not really "unused" or we can mark it as waiting to be used, use code splitting into several bundles to require only when we need

--- 

# FID - Avoid large rendering updates

When large rendering updates happen, they can interfere with your website's ability to respond to user inputs. Some advices:

- Avoid using requestAnimationFrame() for doing any non-visual work.
- Keep your DOM size small.
- Use CSS containment. 

```html
<article>
  <h2>Heading of a nice article</h2>
  <p>Content here.</p>
</article>
<article>
  <h2>Another heading of another article</h2>
  <p>More content here.</p>
</article>
```

```css
article {
  contain: content;
}
```

---
layout: image

image: ./images/questions.jpg
---

# Questions ?

<div class="citation bg-light-600 text-dark-500 text-md p-1 rounded font-sans bg-opacity-50">
  Photo by <a href="https://unsplash.com/@two_tees?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Matt Walsh</a> on <a href="https://unsplash.com/fr/s/photos/questions?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Unsplash</a>
</div>


---
layout: image

image: ./images/thank-you.jpg
---

# Thank you for your attention !

<div class="citation bg-light-600 text-dark-500 text-md p-1 rounded font-sans bg-opacity-50">
  Photo by <a href="https://unsplash.com/de/@wilhelmgunkel?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Wilhelm Gunkel</a> on <a href="https://unsplash.com/fr/s/photos/thanks?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Unsplash</a>
</div>

---

# Preferences

- [Our top Core Web Vitals recommendations for 2023](https://web.dev/top-cwv-2023/)
- [Optimize Largest Contentful Paint](https://web.dev/optimize-lcp/)
- [Optimizing resource loading with the Fetch Priority API](https://web.dev/fetch-priority/)
- [Cumulative Layout Shift (CLS)](https://web.dev/cls/)
- [Optimize Cumulative Layout Shift](https://web.dev/optimize-cls/)
- [Back/forward cache](https://web.dev/bfcache/)
- [Optimize First Input Delay](https://web.dev/optimize-fid/)
- [Optimize long tasks](https://web.dev/optimize-long-tasks/)
- [CSS containment](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Containment)
- [Web Vitals](https://web.dev/vitals/#core-web-vitals)
- [Dynamic LCP Priority: Learning from Past Visits](https://philipwalton.com/articles/dynamic-lcp-priority/)
- [Cases studies](https://wpostats.com/?sjid=15479569239720511772-EU)
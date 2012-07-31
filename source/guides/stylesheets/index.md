---
title: Stylesheets
side_content: >
  <a href="https://github.com/hybridgroup/betterfrontend/issues"
  class="create-issue" target="_blank">Create
  an issue →</a>
  <h1><a href="#toc_0">Stylesheets</a></h1>
  <ul>
    <li><a href="">General Guidelines</a></li>
  </ul>
---

<div class="alert-box">
  This guide needs help with formatting.
</div>
<div class="alert-box">
  Table of Contents is not organized and maybe needs to be split into different
  files.
</div>

# Stylesheets 

The stylesheet layer deals with CSS, Scss, and tools like Compass.

It deals with the visual code required to make web-apps look the way
they do.

Because the stylesheet layer uses many different tools, it makes sense
to call them stylesheets instead of CSS for the distinction of it being
many tools of an ecosystem.

* Style General Guidelines
* Stylesheet Format
  * Selector Naming
  * Selector Naming Avoid Markup
  * Selector Order
  * Definition Order
* Architecture, Abstraction, Foresight
  * Architecture
  * Abstraction
    * Abstraction Technique
    * Using vendor libraries
  * Foresight
* Scss
  * Scss Beginner
  * Scss Advanced

## Stylesheet General Guidelines

Consistency is absolutely key with stylesheets. Because you don't have a
framework available for testing, the only thing you can rely upon is
consistency and best-practices to have a maintainable stylesheet. At the
root, it starts with how you lay out your code.

These problems are even worse when you work in a team that has multiple
people that do work on the front-end layer. So, everyone should commit
to a guideline like the following.

As a general rule, Scss is considered manditory for front-end
development. It brings the power of programming to css, and it requires
no additional understanding to get started. Just change your extensions
to `.css.scss`

### Avoid using IDs to style content

IDs sound like a great idea but they end up causing issues due to the
evolution of the stylesheets, and the "css point value system."

* IDs mess up selectors and definitions because they have a very high
  point value compared to classes. So IDs get priority. (Very brittle
  stylesheets).
* Being unable to reuse them usually leads to frustration situations.

Make your life easy and just use classes to style everything. You'll
thank yourself later when you don't have to put `important!` somewhere
in your stylesheets.

IDs are still great for javascript hooks, put them in the HTML for
Javascript but don't use it for the stylesheet layer.

### Stylesheet Format 

A collection of best-practices recommended for formatting Css, Scss, and Compass.



#### Selector Naming

Use semantically appropriate names. If you aren't semantic with your
naming then you end up with extremely brittle classes.

For example:

```css
.redbox {
  background-color: red;
}
```

Instead, it would be better to do the following:

```css
.error {
  background-color: red;
}
```

Some tips for naming:

* **Clarity** Expected behavior or style should be obvious.
* **Semantic** Think of markup and classes like objects. What an object
  is matters more than what it looks like.

#### Avoid using Markup Elements in Naming Selectors

It's considered best-practice to avoid using markup elements when naming
your selectors.

For example:

``` css
em.important {
  font-style: italic;
}
```

vs

``` css
.important {
  font-style: italic;
}
```

By using element names in your stylesheet you end up coupling markup
with presentation. Fact is, markup is markup and it should only be made
a concern on the markup layer. By creating this distinction we never
have to worry about the element a class is associated with. This leads
to more maintainability and less of a chance of breaking selectors. The
markup layer is going to evolve as time goes by, that means more
elements will be more semantic as the spec evolves. By decoupling
classes from the markup layer we're able to upgrade our markup layer
without worrying about breaking the stylesheet layer.

#### Selector Order 

Alphabetizing your selectors is the recommended way to go. By doing this
you create expectations and consistency. If you're worried about two
things being at opposite ends of the file, then it's recommended to
prefix the classes so this isn't an issue.

``` css
.about {
  background: black;
}

.explosion {
  background: red;
}

.l-container {
  width: 940px;
}

.l-header {
  text-align: center;
}

.logo {
  text-indent: -9999px;
}

.zoo {
  display: inline-block;
}
```

#### Multiple Selector Style *Recommended*

```css
.about,
.explosions,
.hero {
  background-color: #000;
}
```

This allows you to quickly skim over what's being affected.

#### Multiple Selector Style *Not recommended*

```css
.about, .explosions, .hero {
  background-color: #000;
}
```

This suffers readability.

#### Selector Specifity

Try to use the least specific selector as possible, the less code, the
better you can maintain your stylesheet layer.


#### Try to namespace everything

By namespacing everything you avoid getting into cascade hell.

#### Definition Order (A) *Recommended*

Alphabetizing your definitions gives you consistency. It's recommended
that you do this so you always know where to expect definitions.

``` css
.selector {
  background: none;
  display: inline-block;
  height: 30px;
  margin: 10px;
  padding: 10px;
  position: relative;
  width: 30px;
  z-index: 2;
}
```

#### Definition Order (B) *Not recommended*

Put together definitions that are related in terms of what they do.
Because this is subjective, this is not recommended. This can lead to
lack of consistency in projects and that reduces efficiency.

``` css
.selector {
  background: none;
  display: inline-block;
  height: 30px;
  width: 30px;
  padding: 10px;
  margin: 0px;
  position: relative;
  z-index: 2;
}
```

#### Definition Order with SCSS

Outside of the actual definition order, SCSS brings us more that can go
inside of the selector, this is the preferred method of spacing.

```scss
.hero {
  @extend .icons-heroplace;
  @extend .callout;

  @include +pie-clearfix;

  height: 10px;
  width: 10px;
  &.active {
    @extend .icons-heroplace_active;
  }
}
```

The guideline here is:

* Put `@extend` at the top
* Blank space between major different types of definitions (`@extend`,
  `@include`, and `css definitions`).
* If using `&` don't worry about a newline since the visual relationship
  means it's referencing the parent selector.

### Putting all the recommended styles together

Here's the grand readability of all our recommendations put together:

```scss
.about {
  color: $color-red;
}

.hero {
  @extend .icons-heroplace;
  @extend .callout;

  @include +pie-clearfix;

  height: 10px;
  width: 10px;
  &.active {
    @extend .icons-heroplace_active;
  }

  .contact {
    background-color: $color-black;
  }
}

.hi, 
.monkey,
.there, {
  @extend .big-box;

  a {
    color: $color-green;
  }
}

```

### Maintainability, Semantics, Abstraction

The expectation that anything style related is in the stylesheet is
important. Some key things to be in mind of:

#### Abstraction

Abstraction allows your code to be more maintainable and understandable
to you as a human.

##### Abstraction Technique #1

Let's say you have a bunch of classes like the following:

``` css
.icon-email {
  @extend .icons-misc;

  height: 16px;
  text-indent: -9999px;
  width: 17px;
}

.icon-facebook {
  @extend .icons-fb;
  
  height: 16px;
  text-indent: -9999px;
  width: 17px;
}

.icon-tumblr {
  @extend .icons-tumblr;

  height: 16px;
  text-indent: -9999px;
  width: 17px;
}

.icon-twitter {
  @extend .icons-twitter;

  height: 16px;
  text-indent: -9999px;
  width: 17px;
}

```

That's a lot of repetition that we can abstract out.

Here's a solution, abstract it out into a common class and `@extend` from
it.

```scss
.icon-common {
  height: 16px;
  text-indent: -9999px;
  width: 17px;
}

.icon-email {
  @extend .icon-common;
  @extend .icons-misc;
}

.icon-facebook {
  @extend .icon-common;
  @extend .icons-fb;
}

.icon-tumblr {
  @extend .icon-common;
  @extend .icons-tumblr;
}

.icon-twitter {
  @extend .icon-common;
  @extend .icons-twitter;
}
```

**Note** In Sass 3.2 they're introducing placeholder selectors. It
brings this exact functionality without generating extra markup in your
stylesheets during compile time. 
https://gist.github.com/1562442


#### Using vendor'd libraries

Try to `@extend` vendor'd stylesheets into your main stylesheets for
classes so you don't pollute the `Markup` layer with extraneous classes.

### Scss

#### Scss Beginner
##### Variables

Variables are easy.

``` scss
$color-black: #111;
$common-width: 940px;

body {
  color: $color-black;
  width: $common-width;
}
```

Turns into this when compiled:

```css
body {
  color: #111;
  width: 940px;
}
```

Simple!

##### Nesting

``` scss
.products {
  width: 100px;

  .product {
    background-color: #000;

    a {
      color: #fff;
    }
  }
}
```

Turns into

```css
.products {
  width: 100px;
}
.products .product {
  background-color: #000;
}
.products .product a{
  color: #fff;
}

Easy!
```

##### Mixins

Browser engines all have their different ways of implementing
definitions (ugh, it's so annoying). So we have to do things like this
usually:

```css
 .box {
  -webkit-border-radius: 5px;
  -moz-border-radius: 5px;
  -ms-border-radius: 5px;
  -0-border-radius: 5px;
  border-radius: 5px;
 }
```

Sass let's us solve that by doing the following:

```scss
@mixin border-radius($radius) {
  -webkit-border-radius: $radius;
  -moz-border-radius: $radius;
  -ms-border-radius: $radius;
  -0-border-radius: $radius;
  border-radius: $radius;
}

.box {
  @include border-radius(5px);
}
```
Side note: [Compass](http://compass-style.org) Provides a lot of these
mixins. Check it out. Also considered manditory for projects.

##### @extend

Extend allows us to reuse portions of our code without duplicating it in
the stylesheet. It just adds the current scope to the original selector.

Take the following example:

```scss
.borders {
  border: 1px solid red;
  padding: 10px;
}

.products {
  @extend .borders;

  background-color: #000;
}

.box {
  @extend .borders;

  padding: 20px;
}
```

Which turns into the following css

```css
.borders, .products, .box {
  border: 1px solid red;
  padding: 10px;
}

.products {
  background-color: #000;
}

.box {
  padding: 20px;
}
```

**Note** In Sass 3.2 they're introducing placeholder selectors. It
brings this exact functionality without generating extra markup in your
stylesheets during compile time. 
https://gist.github.com/1562442

##### Referencing parent selector &

```scss
.product {
  background-color: #000;
  &.old {
    background-color: gray;
  }
}
```

Turns into 

```css
.product {
  background-color: #000;
}
.product.old {
  background-color: gray;
}
```

#### Scss Advanced

##### Logic

**If**
**Else**
**Then**
**For**
**While**


## Directory Structure 

**Debate** **Issue** **In-Development**

https://github.com/hybridgroup/betterfrontend/issues/4

What is the most efficient directory structure that enables proper
expectation and consistency?

```
app/
  assets/
    stylesheets/
      ui/
      layouts/
```

### UI

UI is anything related to a formatted structure of an interface consumed
by a user.

For example: The [Media Object](http://www.stubbornella.org/content/2010/06/25/the-media-object-saves-hundreds-of-lines-of-code/)


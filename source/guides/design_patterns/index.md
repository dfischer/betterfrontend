---
title: Design patterns
side_content: >
  <h1><a href="#toc_0">Design Patterns</a></h1>
  <ul>
    <li><a href="#toc_1">Active Navigation Item</a></li>
    <li><a href="#toc_2">Sprites</a></li>
    <li><a href="#toc_3">Decoupling Markup from Stylesheets</a></li>
    <li><a href="#toc_4">Making the box-model Easy</a></li>
    <li><a href="#toc_5">Designing for Retina</a></li>
    <li><a href="#toc_5">Carousels</a></li>
    <li><a href="#toc_6">Breadcrumbs</a></li>
  </ul>
---

<div class="alert-box">
  This guide needs help with formatting.
</div>
<div class="alert-box">
  Table of Contents is not organized and maybe needs to be split into different
  files.
</div>

# [Design Patterns](#toc_0)

Design patterns in front-end development are common strategies used to
solve certain problems. 

## [Active Navigation Item](#toc_1)

It's common to highlight the currently active link in a series of
navigation links.

For example:

![Active Navigation Example Screenshot](/images/screenshots/active-navigation.jpg)

There's two main ways to implement this.

* Use pure CSS.
* Use a helper method provided by a language to mark current page.

Using a helper method is possibly easier and more standard, however it
depends upon a programming language. 

However, using a pure CSS method can be just as fine.

### CSS Method

If you browse the www.betterfrontend.com source could, you'll see that
it uses the CSS method.

In the example we use `page_classes` to automatically put a contextual
class on the `body` element based on the current page's name. E.g,
`guides`.

Here's the implementation:

DOM structure

```
:::haml
%body{:class => page_classes}
  .page-wrapper
    %header.page-header{:role => "banner"}
      = link_to(image_tag('logo.png'), '/', :class => 'brand')
      %nav.page-nav
        %ul.nav-links
          %li.nav-link-item.guides= link_to "Guides", '/guides/'
          %li.nav-link-item.debates= link_to "Debates", '/debates/'
          %li.nav-link-item.events= link_to "Events", '/events/'
          %li.nav-link-item.about= link_to "About", '/about/'
```

```
:::scss
body {
  // Make main navigation items active if current
  @each $section in guides, debates, events, about {
    &.#{$section} .page-nav .nav-link-item.#{$section} {
      a {
        color: #000;
      }
    }
  }
}
```
  

### Helper Method

Using a helper method to set an element's active class based on current
path is another way to do it. 

<div class="alert-box">
  Need an example of a helper method based on path.
</div>


## [Sprites](#toc_2)

<div class="alert-box">
  This is a planned design pattern. <a href="https://github.com/hybridgroup/betterfrontend#contributing">Learn how to contribute</a>.
</div>

## [Decoupling Markup from Stylesheets](#toc_3)

It's very common to see people coupling elements with their stylesheets.

For example:

```
:::haml
%div.products
  %div.product
    %span.title Product Title

  %form.new
    %label.title
```

*Don't like how the classes are named? [Take a look at our debates.](https://github.com/hybridgroup/betterfrontend/blob/master/debates.md)*

```
:::scss
div.products {
  
  div.product {
    span.title {
    }
  }

  form {
    label {
    }
  }
}
```

When you do this, you force yourself to update at least 2 files to make
one change. This coupling is bad for maintainability. 

We recommend using *only* classes in stylesheets. This allows you to
evolve the markup layer as it makes sense. The only exception to this
rule is when the markup provided is absolutely semantically accurate. As
a side note, this means we're able to evolve our markup layer as more
standards are implemented.

For example taken from above

```
:::haml
%div.products
  %div.product
    %span.title Product Title

  %form.new
    %label.title
```

```
:::scss
.products {
  .new {
    .title {
    }
  }

  .product {
    .title {
    }
  }
}
```

This decouples stylesheets from the markup layer which brings us more
maintainability. Great!

If you disagree, [create an issue](https://github.com/hybridgroup/betterfrontend/issues/new).

### Another decoupling example that adds semantics

Take an example of a list of things. For example:

```
:::haml
.products
  %ul
    %li= link_to 'product 1'
    %li= link_to 'product 2'
    %li= link_to 'product 3'
    %li= link_to 'product 4'
```

Usually people will style the above like the following:

```
:::scss
.products {
  ul {
    li {
     // styles
    }
  }
}
```

Instead of relying on the markup structure, do the following for a more
maintainable stylesheet and markup layer:

```
:::haml
%ul.products
  %li.product= link_to 'product 1'
  %li.product= link_to 'product 2'
  %li.product= link_to 'product 3'
  %li.product= link_to 'product 4'
```

```
:::scss
.products {
  .product {
   // styles
  }
}
```

This gives us better readability on the stylesheet layer and decouples
the markup from the classes allowing for more maintainable stylesheets.

## [Making the box-model easy](#toc_4)

Isn't it annoying that width and padding are additional to the total
width of the element? You know it's made layouts a pain every now and
then. Luckily, there's a widely supported fix now.

```
:::scss
/* apply a natural box layout model to all elements */
* { -moz-box-sizing: border-box; -webkit-box-sizing: border-box; box-sizing: border-box; }
```

It's extremely safe to use, and even though the `*` selector is used,
performance isn't an issue. For more details check out the [Paul Irish's
post](http://paulirish.com/2012/box-sizing-border-box-ftw/).

## [Designing for Retina](#toc_5)

Since retina is going to become more of a standard, it's now time to
seriously think about how it affects our displays. Retina (Apple
branded) is effetively double the pixel density of a normal display.
That means if you view a photo at double resolution it'll look pretty
awful.

We need to serve higher quality assets. However, does it make sense to
serve higher quality assets to resolutions that can't tell the difference?

The [Clear Eyes](https://github.com/superacidjax/clear_eyes) library aims to fix this problem.

## [Carousels](#toc_6)

Recommended plugins for carousels:

<div class="alert-box">
  This is a planned design pattern. <a href="https://github.com/hybridgroup/betterfrontend#contributing">Learn how to contribute</a>.
</div>


## [Breadcrumbs](#toc_6)

Breadcrumbs are an easy way to show a path to the current page in linear
structure.

Here's a method of implementing it in Ruby and Haml.

```
:::ruby
def bread_crumbs
  @bread_crumbs ||= []
end

def add_crumb(url, caption)
  bread_crumbs << {:url => url, :caption => caption}
end
```

```
:::scss
%ul.breadcrumb
  %li.crumb
    = link_to 'Home', root_path
    %span.crumb-divider /
  - bread_crumbs.each do |crumb|
    %li.crumb
      %a{:href => crumb[:url]}= crumb[:caption]
      %span.crumb-divider /
```

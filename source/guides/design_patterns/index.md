---
title: Design patterns
---

<div class="alert-box">
  This guide needs help with formatting.
</div>
<div class="alert-box">
  Table of Contents is not organized and maybe needs to be split into different
  files.
</div>

# Design Patterns

Design patterns in front-end development are common strategies used to
solve certain problems. 

## Active Navigation Item

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

If you browse the www.betterfrontend.com source code, you'll see that
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


## Sprites

<div class="alert-box">
  This is a planned design pattern. <a href="https://github.com/hybridgroup/betterfrontend#contributing">Learn how to contribute</a>.
</div>


## Making the box-model easy

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

## Designing for Retina

Since retina is going to become more of a standard, it's now time to
seriously think about how it affects our displays. Retina (Apple
branded) is effetively double the pixel density of a normal display.
That means if you view a photo at double resolution it'll look pretty
awful.

We need to serve higher quality assets. However, does it make sense to
serve higher quality assets to resolutions that can't tell the difference?

The [Clear Eyes](https://github.com/superacidjax/clear_eyes) library aims to fix this problem.

## Carousels

Recommended plugins for carousels:

<div class="alert-box">
  This is a planned design pattern. <a href="https://github.com/hybridgroup/betterfrontend#contributing">Learn how to contribute</a>.
</div>


## Breadcrumbs

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

## Dynamic Table of Contents

We use a dynamic table of contents on the site. Since a Table of
Contents is essentially presentational as opposed to content we're able
to leverage Javascript to implement our Table of Contents.

Our DOM structure is as follows:

```
:::haml
#js-toc.toc
  %h1#js-toc-heading.toc-heading
    Guides
  %ul#js-toc-items
```

Pretty simple. As a best practice we add **javascript only** hooks to
avoid unexpected changes on the Stylesheet layer and to also have optial
performance on the Javascript layer.

We then implement the following jQuery to get it done.

```
:::javascript
$("article.post").each(function() {
  var article = $(this);
  var toc = $("#js-toc");
  var toc_items = $("#js-toc-items");
  var toc_heading_link = $("#js-toc-heading-link");

  article.find('h1').each(function() {
    var current_id = $(this).attr('id');
    var content = $(this).html();
    var anchor = '<a href="#' + current_id + '"> '+ content +' </a>';

    $(this).html(anchor);
  });

  article.find('h2').each(function() {
    var current_id = $(this).attr('id');
    var content = $(this).html();
    var anchor = '<a href="#' + current_id + '"> '+ content +' </a>';

    $(this).html(anchor);

    toc_items.append('<li><a href="#' + current_id + '">' + content + '</a></li>');
  });

  $("#js-toc").append(toc_items);
});
```

What we get here is an automatically generated table of contents that is
inserted into the `#js-toc-items` container. For each `<h2>` on the site
we append a `<li>` with the proper contents.

We've also done something a bit extra. If you noticed, we also set a
link for every `<h2>` in the **Article** pointing to that `<h2>`'s name.
That way every `<h2>` on the site can act as a link to itself. We have
extra styling in place to make that show an anchor icon. Hover over a
`<h2>` to see what we're talking about.

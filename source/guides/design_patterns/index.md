# Decoupling Markup from Stylesheets

It's very common to see people coupling elements with their stylesheets.

For example:

```haml
%div.products
  %div.product
    %span.title Product Title

  %form.new
    %label.title
```

*Don't like how the classes are named? [Take a look at our debates.](https://github.com/hybridgroup/betterfrontend/blob/master/debates.md)*

```scss
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

```haml
%div.products
  %div.product
    %span.title Product Title

  %form.new
    %label.title
```

```scss
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

# Another decoupling example that adds semantics

Take an example of a list of things. For example:

```haml
.products
  %ul
    %li= link_to 'product 1'
    %li= link_to 'product 2'
    %li= link_to 'product 3'
    %li= link_to 'product 4'
```

Usually people will style the above like the following:

```scss
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

```haml
%ul.products
  %li.product= link_to 'product 1'
  %li.product= link_to 'product 2'
  %li.product= link_to 'product 3'
  %li.product= link_to 'product 4'
```

```scss
.products {
  .product {
   // styles
  }
}
```

This gives us better readability on the stylesheet layer and decouples
the markup from the classes allowing for more maintainable stylesheets.

# Making the box-model easy

Isn't it annoying that width and padding are additional to the total
width of the element? You know it's made layouts a pain every now and
then. Luckily, there's a widely supported fix now.

```scss
/* apply a natural box layout model to all elements */
* { -moz-box-sizing: border-box; -webkit-box-sizing: border-box; box-sizing: border-box; }
```

It's extremely safe to use, and even though the `*` selector is used,
performance isn't an issue. For more details check out the [Paul Irish's
post](http://paulirish.com/2012/box-sizing-border-box-ftw/)

# Designing for Retina

Since retina is going to become more of a standard, it's now time to
seriously think about how it affects our displays. Retina (Apple
branded) is effetively double the pixel density of a normal display.
That means if you view a photo at double resolution it'll look pretty
awful.

We need to serve higher quality assets. However, does it make sense to
serve higher quality assets to resolutions that can't tell the difference?

The [Clear Eyes](https://github.com/superacidjax/clear_eyes?utm_source=rubyweekly&utm_medium=email) library aims to fix this problem.

# Carousels

Recommended plugins for carousels:


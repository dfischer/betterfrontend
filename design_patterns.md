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

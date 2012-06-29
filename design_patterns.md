# Decoupling Markup from Stylesheets

It's very common to see people coupling elements with their stylesheets.

For example:

```haml
%div.products
  %div.product
    %span.title Product Title

  %form.product-new
    %label.title
```

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
```

```scss
```

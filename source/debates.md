# Debates

This file contains debates that are going on within the community that
argue for a specific best-practice.

## Nesting, Decoupling, & Cascading

<div class="alert-box">
  Need more pro's & con's
</div>

Our ultimate focus is maintainability. Given the following, which is
easier to maintain?

Taking the following Markup:

```
:::haml
.products
  %article.product
    %h1.title
    %p.description
    %span.price
    %a.add

  %form.new
    %input.title
```

```
:::scss
.products {
  .new {
    .title {
    }
  }

  .product {
    .add {
    }

    .description {
    }

    .price {
    }

    .title {
    }
  }
}
```

This version exhibits one-word semantics scoped to a noun. Overall very
easy to read. It also offers interesting/advanced selector ability
whenever you want to travel outside of the namespace, as there are
probably a lot of elements using these one-word names.

Example: `.new` A ui interface that highlights on the page all elements
related to creating a new object.

Pros:

* Readability
* Cascading potential
* Namespacing removes conflict / unnessecary changes.

Cons:

* Potentially violates [inception rule](http://thesassway.com/beginner/the-inception-rule).
* Potentially hard to search for specific style through editor. There
  may be more than one `.new` in `products.css.scss` 

vs.

```
:::haml
.products
  %article.product
    %h1.product-title
    %p.product-description
    %span.product-price
    %a.product-add

  %form.product-new
    %input.product-title
```

```
:::scss
.products {
  .product {
    .product-add {
    }

    .product-description {
    }

    .product-price {
    }

    .product-title {
    }
  }

  .product-new {
    .product-new-title {
    }
  }
}
```

This version exhibits extreme verbosity. This can be nice on one hand,
but on the other, it can be really annoying. This is a double edged
sword.

Pros:
* Each class can exist out of the scope therefore helping inception
  rule.
* Can easily find style with cmd+f
* Verbosity?

Cons:
* Can't target common selectors if needed. E.g, all .title's on page.
* Verbosity?

Which is easier to maintain for the developer? They both have their own
implications.

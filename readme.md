# #betterfrontend is a movement to improve Front-End Development

Website coming soon for more information. (will be at
http://www.betterfrontend.com)

Official twitter: twitter.com/betterfrontend

This repository will serve as a style guide for tools and libraries that are
used in front-end development.

A major problem with front-end development is that it doesn't have a
clear definition of what it is in itself, and the skills that are used
don't have much documentation. As a result, the learning curve is *too
damn high* and it's diffilcult to find best practices on how to do
things better. 

The goal of this repository is to help alievate the definition problems
and provide style guides as well as general best practices.

The following things will be defined:

* Front-End Development
* Tools used with Front-End Development
* How to work on the Stylesheet layer effectively (CSS, Scss).
* How to work on the HTML layer effectively (Html, Haml, erb, mustache).
* How to work on the front-end layer of a web-application framework
  effectively.

## What is Front-End Development?

Front-End Development is programming the visual layer of a
web-application. Ruby apps like Hulu, Github, and Kanbanpad look the way
they do *because* of front-end development. A front-end developer is
just as nessecary as a back-end developer, despite this nessecity;
front-end development has a severe lack of attention and care. This
leads to huge problems for our community and we need to fix it.

Front-end development requires *masterful* use of HTML & CSS. This is
due to the complexity of frameworks like Ruby on Rails. This repository
shall serve as a guideline of how to reach that level of mastery.

## Stylesheet Layer

The stylesheet layer deals with CSS, Scss, and tools like Compass.

It deals with the visual code required to make web-apps look the way
they do.

Because the stylesheet layer uses many different tools, it makes sense
to call them stylesheets instead of CSS for the distinction of it being
many tools of an ecosystem.

### Stylesheet General Guidelines

Consistency is absolutely key with stylesheets. Because you don't have a
framework available for testing, the only thing you can rely upon is
consistency and best-practices to have a maintainable stylesheet. At the
root, it starts with how you lay out your code.

These problems are even worse when you work in a team that has multiple
people that do work on the front-end layer. So, everyone should commit
to a guideline like the following.

### Stylesheet Format 

A collection of best-practices recommended for formatting Css, Scss, and Compass.

#### Selector Naming

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

### Maintainability / Semantics

The expectation that anything style related is in the stylesheet is
important. Some key things to be in mind of:

#### Using vendor'd libraries

Try to `@extend` vendor'd stylesheets into your main stylesheets for
classes so you don't pollute the `Markup` layer with extraneous classes.

## Markup Layer

The Markup layer deals with HTML, Haml, Mustache, and similar tools to
create markup.

This layer acts as the semantic relationship to the content it serves.
Stylistically, it should have no bearing.

## Libraries

Here are some libraries that are commonly used for front-end
development. This is going to be opinionated. We can't recommend
everything, we want to recommend something that fits the majority so we
can see consistency across projects.

### Sass *necessary*
### Compass *necessary*
### Blueprint *not recommended*
### Bootstrap *complicated*

Bootstrap is an amazing idea. However, it has some pitfalls that
everyone should be aware of. First of all, as a number one, it
completely violates semantics and modern HTML5 spec.

Especially when using a grid system in a basic way, you expose yourself
to habits that lead to unmaintainable sylesheets.

The best way to solve this is to use `@extend` to keep your stylesheets
semantic and maintainable. However, because of how Bootstrap uses it's
CSS3 selectors you can't do this by just using `@import bootstrap` 

The problem:

I want to maintain a semantic stylesheet structure. So I put
`bootstrap.css` into `vendor/stylesheets/bootstrap.css.scss` and then I
`@import bootstrap` in `application.css.scss`

From there I want a specific class to have a `.span4` e.g:

```css
  .header {
    @extend .span4
  }
```

In general this would work, however due to bootstrap using something
like `[class*="span"]` it breaks this strategy to maintain a clean
stylesheet. So basically, you're forced to having to put .span4, .rows
all over your *Markup* layer and that goes against our #1 guideline of
keeping a clear separation between your markup layer and presentation
layer.

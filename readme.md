# #betterfrontend is a movement to improve Front-End Development

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

# What is Front-End Development?

Front-End Development is programming the visual layer of a
web-application. Ruby apps like Hulu, Github, and Kanbanpad look the way
they do *because* of front-end development. A front-end developer is
just as nessecary as a back-end developer, despite this nessecity;
front-end development has a severe lack of attention and care. This
leads to huge problems for our community and we need to fix it.

Front-end development requires *masterful* use of HTML & CSS. This is
due to the complexity of frameworks like Ruby on Rails. This repository
shall serve as a guideline of how to reach that level of mastery.

# Stylesheet Layer

The stylesheet layer deals with CSS, Scss, and tools like Compass.

It deals with the visual code required to make web-apps look the way
they do.

Because the stylesheet layer uses many different tools, it makes sense
to call them stylesheets instead of CSS for the distinction of it being
many tools of an ecosystem.

## Stylesheet General Guidelines

Consistency is absolutely key with stylesheets. Because you don't have a
framework available for testing, the only thing you can rely upon is
consistency and best-practices to have a maintainable stylesheet. At the
root, it starts with how you lay out your code.

These problems are even worse when you work in a team that has multiple
people that do work on the front-end layer. So, everyone should commit
to a guideline like the following.

## Stylesheet Format 

A collection of best-practices recommended for formatting Css, Scss, and Compass.

### Order

``` css
.selector {
  background: none;
  display: inline-block;
  position: relative;
  z-index: 2;
}
```

Alphabetizing your definitions gives you consistency. It's recommended
that you do this so you always know where to expect definitions.

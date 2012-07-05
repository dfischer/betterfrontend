# #betterfrontend is a movement to improve Front-End Development

Front-end development sucks, and #betterfrontend is a movement by the
community to make it better.

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
  effectively (Rails focused for now).
 
----

**If you disagree with anything in this document. PLEASE file an issue
so we can improve the community as a whole. This is a movement of
collaboration and refinement.**

**Our mission is to make front-end development better for you, your
team, and everyone else.**

## Table of Contents

* [What is Front-End Development?](https://github.com/hybridgroup/betterfrontend#what-is-front-end-development)
* [Stylesheets](https://github.com/hybridgroup/betterfrontend/blob/master/stylesheets.md)
* [Markup](https://github.com/hybridgroup/betterfrontend/blob/master/markup.md)
* [Design Patterns](https://github.com/hybridgroup/betterfrontend/blob/master/design_patterns.md)
* [Libraries](https://github.com/hybridgroup/betterfrontend/blob/master/libraries.md)
* [Rails](https://github.com/hybridgroup/betterfrontend/blob/master/rails.md)
* [Debates](https://github.com/hybridgroup/betterfrontend/blob/master/debates.md)

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


## Front-End Development depends upon 3 core concepts.

Architecture, Abstraction, and Foresight.



## Architecture
Architecture is how all the pieces of the front-end layer fit together. It’s the grand scope of everything you are developing. It includes semantics, organization, abstraction, and foresight.

## Abstraction
Abstraction is making your code semantic and understandable to humans. A browser only really  cares about the definitions you give it. Like `:border-left`. The classes you put those definitions in are irrelevant to the browser. However, to you as a human, those classes mean everything. By abstracting concepts properly, you’re able to create a living world in your code that’s easy to understand. For example, .pacman, .comment, .post. That’s a simple level of abstraction and proper use of semantics. You could abstract things even further in CSS if you had variables, functions, expressions, and other traditional programming methods. When you follow this mentality you become efficient because the entire code base is easier to understand and read.

## Foresight
Foresight is simply being mindful of the future and the growth of the application. The HTML & CSS layer does not have a toolkit for testing. That means you have to be mindful of repercussions when making any modifications to the code. This is absolutely critical and a unique problem for the front-end. With the back-end layer you can make changes to your code and have confidence that your tests will tell you when you break something. The front-end layer doesn’t have a tool for this. If you break the html or styling, you may never know until it’s too late. That’s a really bad situation. So the only way you can avoid that is with a good architecture in place that is mindful of foresight.



# Contributors

In order of commit history:

* Daniel Fischer - [web](http://www.danielfischer.com),
  [twitter](http://www.twitter.com/dfischer)

# Inspiration & References

Inspiration & references that have triggered the text. These are in no
particular order and may or may not be in agreement with
'#betterfrontend'. The point is that they have contributed to the idea one
way or another.

In no particular order: 

* http://www.adobe.com/devnet/html5/articles/semantic-markup.html
* http://yellowshoe.com.au/standards/
* http://awardwinningfjords.com/2010/07/30/style-guides-using-sass-extend.html
* https://github.com/styleguide/css
* https://speakerdeck.com/u/bermonpainter/p/css-pre-processors-stylus-less-sass
* http://smacss.com/
* https://github.com/dennishall/CSS-Style-Guide
* http://www.stubbornella.org/content/2011/09/06/style-headings-using-html5-sections/
* http://www.markdotto.com/2012/03/02/stop-the-cascade/
* http://coding.smashingmagazine.com/2012/04/20/decoupling-html-from-css/

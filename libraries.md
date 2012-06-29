
## Libraries

Here are some libraries that are commonly used for front-end
development. This is going to be opinionated. We can't recommend
everything, we want to recommend something that fits the majority so we
can see consistency across projects.

### Sass *necessary*
### Compass *necessary*

#### Sprites

Use sprites whenever possible.

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

### KSS
https://github.com/kneath/kss


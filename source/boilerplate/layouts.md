---
title: Boilerplate
---

# Main application layout

The main layout of an application should be called,
`application.html.haml`


We don't recommend using any other name for the "main" layout due to
consistency. Frameworks like Ruby on Rails already default to using
"application" for anything top-level, we should respect the same
convention on the front-end layer. Now this may be biased to Ruby on
Rails but what real alternatives do we have? `site.css.scss?` It seems
that it's better to just bend towards consistency sake and always follow
the convention of `application.html.haml` and thusly
`application.css.scss`.


## application.html.haml

    :::haml
    !!! 5
    / paulirish.com/2008/conditional-stylesheets-vs-css-hacks-answer-neither/
    /[if lt IE 7] <html class="no-js lt-ie9 lt-ie8 lt-ie7" lang="en">
    /[if IE 7] <html class="no-js lt-ie9 lt-ie8" lang="en">
    /[if IE 8] <html class="no-js lt-ie9" lang="en">
    / Consider adding a manifest.appcache: h5bp.com/d/Offline
    / [if gt IE 8]><!
    %html.no-js{:lang => "en"}
      / <![endif]
      %head
        %meta{:charset => "utf-8"}/
        %meta{:content => "IE=edge,chrome=1", "http-equiv" => "X-UA-Compatible"}/
        // page_title should be a method for creating a page title
        %title= page_title || "Betterfrontend Application Layout"
        %meta{:content => "", :name => "description"}/
        / Mobile viewport optimized: h5bp.com/viewport
        %meta{:content => "width=device-width, initial-scale=1.0", :name => "viewport"}/
        / Place favicon.ico and apple-touch-icon.png in the root directory: mathiasbynens.be/notes/touch-icons
        = stylesheet_link_tag "application"
        / More ideas for your <head> here: h5bp.com/d/head-Tips
        /
          All JavaScript at the bottom, except this Modernizr build.
          Modernizr enables HTML5 elements &amp; feature detects for optimal performance.
          Create your own custom Modernizr build: www.modernizr.com/download/
        = javascript_include_tag 'top/modernizr.foundation'
      /
        Page classes should be a method that outputs logical classes
        for the current page to hook into
      %body{:class => page_classes}
        /
          Prompt IE 6 users to install Chrome Frame. Remove this if you support IE 6.
          chromium.org/developers/how-tos/chrome-frame-getting-started
        /[if lt IE 7] <p class=chromeframe>Your browser is <em>ancient!</em> <a href="http://browsehappy.com/">Upgrade to a different browser</a> or <a href="http://www.google.com/chromeframe/?redirect=true">install Google Chrome Frame</a> to experience this site.</p>
        %header.page-header{:role => "banner"}
        %div.page-content{:role => "main"}
          = yield
        %footer.page-footer{:role => "contentinfo"}
        / JavaScript at the bottom for fast page loading
        = javascript_include_tag  "application"
        / end scripts
        /
          Asynchronous Google Analytics snippet. Change UA-XXXXX-X to be your site's ID.
          mathiasbynens.be/notes/async-analytics-snippet
        :javascript
          var _gaq=[['_setAccount','UA-XXXXX-X'],['_trackPageview']];
          (function(d,t){var g=d.createElement(t),s=d.getElementsByTagName(t)[0];
          g.src=('https:'==location.protocol?'//ssl':'//www')+'.google-analytics.com/ga.js';
          s.parentNode.insertBefore(g,s)}(document,'script'));

### Refactored for brevity & partials

With the power of partials we can factor this out a bit more. The
following example is using Haml and a partial helper.

#### `application.html.haml`

    :::haml
    !!! 5
    /[if lt IE 7] <html class="no-js lt-ie9 lt-ie8 lt-ie7" lang="en">
    /[if IE 7] <html class="no-js lt-ie9 lt-ie8" lang="en">
    /[if IE 8] <html class="no-js lt-ie9" lang="en">
    / [if gt IE 8]><!
    %html.no-js{:lang => "en"}
      / <![endif]
      = partial 'layouts/head'

      %body{:class => page_classes}
        %header.page-header{:role => "banner"}

        %div.page-content{:role => "main"}
          %article.post
            = yield

        %footer.page-footer{:role => "contentinfo"}
          = partial "layouts/footer"

#### `layouts/_head.html.haml`

    :::haml
    %head
      %meta{:charset => "utf-8"}/
      %meta{:content => "IE=edge,chrome=1", "http-equiv" => "X-UA-Compatible"}/
      %title= page_title
      %meta{:content => "A community effort to standardize Front-End Development.", :name => "description"}/
      %meta{:content => "width=device-width, initial-scale=1.0", :name => "viewport"}/
      = stylesheet_link_tag "application"
      = javascript_include_tag 'top/modernizr.foundation'


#### `layouts/_footer.html.haml`

    :::haml
    .footer-content
      // footer content here

    / JavaScript at the bottom for fast page loading
    = javascript_include_tag  "application"
    / end scripts
    :javascript
      hljs.initHighlightingOnLoad();
    /
      Asynchronous Google Analytics snippet. Change UA-XXXXX-X to be your site's ID.
      mathiasbynens.be/notes/async-analytics-snippet
    :javascript
      var _gaq=[['_setAccount','UA-XXXXX-X'],['_trackPageview']];
      (function(d,t){var g=d.createElement(t),s=d.getElementsByTagName(t)[0];
      g.src=('https:'==location.protocol?'//ssl':'//www')+'.google-analytics.com/ga.js';
      s.parentNode.insertBefore(g,s)}(document,'script'));

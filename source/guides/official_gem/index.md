---
title: Official Gem
---

<div class="alert-box">
  This is a behavior spec for work-in-progress.
</div>

The Betterfrontend Gem is a suite of Ruby-focused best-practices.

# Betterfrontend Gem

## Navigation

Navigation items (picture).

Defaults to a horizontal layout.

```
:::haml
= navigation do
  = item 'Guides', '/guides'
  = item 'Debates', '/debates'
  = item 'Events', '/events'
  = item 'About', '/about'
```

### Vertical Layout

```
:::haml
= navigation direction: :vertical do
  = item 'Guides', '/guides'
  = item 'Debates', '/debates'
  = item 'Events', '/events'
  = item 'About', '/about'
```

## Media Block

Media blocks are very common UI elements. For example, Facebook feeds.

```
:::haml
= media_for @user do |m|
  = m.image :avatar
  = m.heading :name
  = m.nested_media_for @jon do |nm|
    = nm.image :avatar
    = nm.heading :name
  = m.nested_media_for @bob do |nm|
    = nm.image :avatar
    = nm.heading :name
```

## Breadcrumbs

```
:::haml
= breadcrumbs do
  = crumb 'Downloads', '/downloads'
  = crumb_divider
  = crumb 'Gems', '/gems'
  = crumb 'BFE', '/bfe'
```

## Carousel

<div class="alert-box">
  Idea. Should this be included?
</div>


More ideas to be had at:
http://developer.yahoo.com/ypatterns/everything.html

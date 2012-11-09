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
  = navigation_item 'Guides', '/guides'
  = navigation_item 'Debates', '/debates'
  = navigation_item 'Events', '/events'
  = navigation_item 'About', '/about'
```

### Vertical Layout

```
:::haml
= navigation direction: :vertical do
  = navigation_item 'Guides', '/guides'
  = navigation_item 'Debates', '/debates'
  = navigation_item 'Events', '/events'
  = navigation_item 'About', '/about'
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

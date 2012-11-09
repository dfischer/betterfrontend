---
title: Official Gem
---

<div class="alert-box">
  This is a behavior spec for work-in-progress.
</div>

The Betterfrontend Gem is a suite of Ruby-focused best-practices.

# Betterfrontend Gem

## Navigation

```
:::haml
= navigation do
  = navigation_item 'Guides', '/guides'
  = navigation_item 'Debates', '/debates'
  = navigation_item 'Events', '/events'
  = navigation_item 'About', '/about'
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

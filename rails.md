## Working in the Rails view

### Handling state and logic through the stylesheet

It's best practice to handle as much logic as you can through the
stylesheet. Once you shift perspectives a bit, you'll realize that it's
really easy to do this.

Take the following idea:

bq. If the user is on a login page, they get a different background
color.

Here's the wrong implementation:

```haml
- if user_signed_in? || admin_signed_in?
  - else
    %body#login
```

First off, use as little conditionals as possible in your views. Second
of all, you can scope all the logic through a state helper.

```haml
%body{:class => "forest #{stylesheet-user-state} #{stylesheet-current-page}", :id => ""}
```

Which outputs

```html
<body class='user new is-logged-out'>
```

Using this technique you keep the logic out of the Markup layer, and
you're able to hook into specific logic points in the Stylesheet layer.


# [Betterfrontend](http://www.betterfrontend.com)

Front-End Development lacks consistency. Betterfrontend is a
community-driven project to bring best-practices and consistency to
Front-End Development.

Secondarily, Betterfrontend will be a repository of tutorials to reduce
the learning curve of becoming a front-end developer.

The guides are viewable at
[www.betterfrontend.com](http://www.betterfrontend.com).

You can also [follow @betterfrontend on Twitter](https://twitter.com/betterfrontend).

The entire web-development community is encouraged to contribute to
these guides. It's easy to contribute.

## Contributing

You can contribute in many ways. Just having a voice is a contribution
so shout about betterfrontend on Twitter, or [create an issue](https://github.com/hybridgroup/betterfrontend/issues) 
about things that annoy you with front-end-development.

If you're feeling particularly involved, you can [fork the project](https://github.com/hybridgroup/betterfrontend/fork_select).

The site and docs are built using [middleman](http://middlemanapp.com/)
to make developing a static site easy.

Simply check out your forked repository and then run `bundle install`
and you can run the site locally by typing `middleman` in the root
directory.

Now you can edit the site & docs!

When you're ready to contribute back, simply create a pull-request back
to the main repository and we'll review it.

## How It's Deployed

The @betterfrontend site is deployed on GitHub pages.

The recommended folder structure is as follows:

```
betterfrontend/
  main-repo/
  betterfrontend-pages/

```

The `main-repo/` folder is where you're currently reading this and has
all the source/doc files for the site. When the site is ready to be
built we `middleman build` which outputs to `betterfrontend-pages/`
which is an orphaned branch that is deployed to GitHub.

You probably don't need to know this as a contributor but knowledge is
power!

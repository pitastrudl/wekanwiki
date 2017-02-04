# Style guide

We follow the [meteor style guide](https://guide.meteor.com/code-style.html#javascript).

Please read the meteor style guide before making any significant contribution.

# General tips for getting started (for new developers)

- Install Wekan fork from source to your computer.
- Read Wekan fork source code.
- Ask questions at our [Rocket.Chat][rocket_chat]. You can ask anything, we are here to help.
- Read Meteor documentation.
- Keep list of your contributions on your personal website.
- Keep track of time it takes to implement each part of a feature, so you can estimate what time it would take to implement similar feature. After implementing feature, review your estimate was it correct, make improvements to your process and estimates, also keeping enough time allocated in estimate if something is harder to implement. Employers look for coders with proven track record.
- Work and concentrate on one issue at a time and finish it, before moving to other issue.
- You can ask for comments from others, but usually those feature requests are clearly defined how they should work. You can place those Settings options there where it seems most logical for you.
- You are free to select what feature to work on.
- Main point is to be friendly to those commenting of your code, and incorporate those suggestions that make most sense.

# Installation

Wekan is made with [Meteor](https://www.meteor.com). Thus the easiest way to
start hacking is by installing the framework, cloning the git repository, and
launching the application:

```bash
$ curl https://install.meteor.com/ | sh # Installs Meteor on Mac or Linux
```

It's possible to run the normal `meteor run` after cloning the repo to your local machine but some features may not work.

The proper way to install Wekan for testing is by [installing from source](https://github.com/wefork/wekan/wiki/Install-from-source).

As for any Meteor application, Wekan is automatically refreshed when you change
any file of the source code, just play with it to see how it behaves!

# Build Pipeline

- Templates are written in [JADE](https://naltatis.github.io/jade-syntax-docs/) instead of plain HTML.
- CSS is written in the [Stylus](http://stylus-lang.com/) precompiler, and
- Meteor templates are created as BlazeLayout templates.
- Eslint for linting.
- Instead of the allow/deny paradigm a lot of the `collections` defined in the project use `mutations` to define what kinds of operations are allowed.

For further details look for the 'feature summaries' in the Wiki (still in progress) otherwise go through the git history and see how old features were built. Might I suggest the Start and Due date feature [wefork#26](https://github.com/wefork/wekan/pull/26)

# Translations

If adding new features, please also support the internationalization features built in. Refer to the [Translations](https://github.com/wefork/wekan/wiki/Translations) wiki page. 

# Directory Structure Details

TODO

[rocket_chat]: https://chat.indie.host/channel/wekan
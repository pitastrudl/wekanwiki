# Style guide

We follow the [meteor style guide](https://guide.meteor.com/code-style.html#javascript).

Please read the meteor style guide before making any significant contribution.

# Tips for new developers

## Getting Started

- Try [Docker environment for Wekan development](https://github.com/wekan/wekan-dev).
- Or install [Wekan from source](https://github.com/wekan/wekan/wiki/Install-and-Update#install-manually-from-source) to your computer.
  - If that doesn't work, try installing it via the [[virtual appliance|virtual-appliance]]
- Ask questions at [![Wekan chat][vanila_badge]][vanila_chat]
  -  We used to be at ~~[Rocket.Chat][rocket_chat]~~ but that's been discontinued.
- You can ask anything, we are here to help. But also consult the sources that are already available.
  - Look through old [pull requests](https://github.com/wekan/wekan/pulls)
  - Read Wekan source code.
  - Read Meteor documentation.

## Preventing Travis CI lint errors before submitting pull requests

- Eslint for linting. To prevent Travis CI lint errors, you can test for lint errors with "npm run lint"
- If you want automatic fixes to that code file you can copy code to [jsbeautifer website](http://jsbeautifier.org) with settings Indent with 2 spaces (topmost dropdown), [X] Space before conditional: "if(x)" / "if (x)", [X] Use JSLint-happy formatting tweaks.

## Pull Request Workflow (Please read before submitting PR's)

- Use the [feature branch](https://www.atlassian.com/git/tutorials/comparing-workflows#feature-branch-workflow) workflow.
  - create a PR from your feature-branch to `wekan/devel` directly so that you can continue your work without interruption.
- Keep your local forks updated with this repo by setting your `git upstream` value as described [here](https://robots.thoughtbot.com/keeping-a-github-fork-updated).
  - before submitting a PR make sure you `rebase` your local branch as described [here](http://push.cwcon.org/learn/stay-updated#on_your_computer_routine_tasks)
  - If you accidentally mess around on your `devel` branch, follow these steps [here](http://push.cwcon.org/learn/stay-updated#oops_i_was_messing_around_on_) to clean it up.

## Choosing issues to work on

- You are free to select what feature to work on.
  - Leave a comment on an issue saying that you're working on it, and give updates as needed.
  - Work and concentrate on one issue at a time and finish it, before moving to other issue.
- Keep list of your contributions on your personal website.
- Keep track of time it takes to implement each part of a feature, so you can estimate what time it would take to implement similar feature. After implementing feature, review your estimate was it correct, make improvements to your process and estimates, also keeping enough time allocated in estimate if something is harder to implement. Employers look for coders with proven track record.
- You can ask for comments from others, but usually those feature requests are clearly defined how they should work. You can place those Settings options there where it seems most logical for you.

Main point is to be friendly to those commenting of your code, and incorporate those suggestions that make most sense.

# Build Pipeline


- Templates are written in [JADE](https://naltatis.github.io/jade-syntax-docs/) instead of plain HTML.
- CSS is written in the [Stylus](http://stylus-lang.com/) precompiler, and
- Meteor templates are created as BlazeLayout templates.
- Instead of the allow/deny paradigm a lot of the `collections` defined in the project use `mutations` to define what kinds of operations are allowed.

For further details look for the 'feature summaries' in the Wiki (still in progress) otherwise go through the git history and see how old features were built. Might I suggest the Start and Due date feature [wefork#26](https://github.com/wefork/wekan/pull/26)

# Translations

If adding new features, please also support the internationalization features built in. Refer to the [[Translations]] wiki page. 

# Export From Trello

It's possible to import your existing boards from Trello. Instructions [[here|migrating-from-trello]]

# Directory Structure Details

TODO

[![Wekan chat][vanila_badge]][vanila_chat]


[rocket_chat]: https://chat.indie.host/channel/wekan
[vanila_badge]: https://vanila.io/img/join-chat-button2.png
[vanila_chat]: https://chat.vanila.io/channel/wekan
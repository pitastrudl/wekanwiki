# Style guide

We follow the [meteor style guide](https://guide.meteor.com/code-style.html#javascript).

Please read the meteor style guide before making any significant contribution.

# Tips for new developers

## Finding code

There is find.sh script that ignores generated directories, finds code in subdirectories, and paginates with less. For example, finding how search cards is implemented:
```
cd wekan
./find.sh js-search
```
When you run this, you see .jade template files where is search input box, and .js files where is the search code. CSS is in .styl files.

## Getting Started

- Currently Wekan development is done mainly at Ubuntu 16.04 64bit, but building Wekan does work on any Debian 9 64bit or Ubuntu 14.04 64bit or newer.
- Install [Wekan from source](https://github.com/wekan/wekan) with rebuild-wekan.sh script, with options 1 to install dependencies and 2 to rebuild source, to your Linux computer (Debian 9 or Ubuntu 14.04 or newer), or try installing it via the [[virtual appliance|virtual-appliance]]
- You can use for example [Visual Studio Code](https://code.visualstudio.com/) for editing code, it has Meteor.js etc plugins 
- When changing database schema, [migrations can be used](https://github.com/wekan/wekan/blob/master/server/migrations.js).
- [Excellent example how pull requests are improved and integrated, and not needed commits removed](https://github.com/wekan/wekan/pull/1470)
- Ask questions at [![Wekan chat][vanila_badge]][vanila_chat]
  -  We used to be at ~~[Rocket.Chat][rocket_chat]~~ but that's been discontinued.
- You can ask anything, we are here to help. But also consult the sources that are already available.
  - Look through old [pull requests](https://github.com/wekan/wekan/pulls)
  - Read Wekan source code, you can use some git history viewer GUI like gitk
  - Read [Meteor documentation](https://docs.meteor.com/) for [Meteor version](https://github.com/wekan/wekan/blob/master/.meteor/release) in use, other versions mentioned at [Dockerfile](https://github.com/wekan/wekan/blob/master/Dockerfile)
- Docker up-to-date way: You can  clone wekan/wekan repo and update docker-compose.yml file ROOT_URL etc as documented at https://github.com/wekan/wekan-mongodb commented docker-compose.yml file, install docker, and build from source with docker with "docker-compose up -d --build"
- Docker not up-to-date way: [Docker environment for Wekan development](https://github.com/wekan/wekan-dev). 

## Pull Request Workflow (Please read before submitting PR's)

- If package is available on meteor https://atmospherejs.com `meteor add packagename` or https://www.npmjs.com `meteor npm install packagename` then it's enough to add package that way, and there is no need to clone repo in [rebuild-wekan.sh](https://github.com/wekan/wekan-maintainer/tree/master/releases) script.
- When doing pull requests, only add additions and changes to English at wekan/i18n/en.i18n.json . Other translations are done at [https://www.transifex.com/wekan/wekan](https://www.transifex.com/wekan/wekan).
- If you have fix to some existing pull request, add your fix as comment. Do not post new pull request.
- For new features add new pull request, if there is none already.
- remove all console.log statements
- [Fix all lint errors and warnings](https://github.com/wekan/wekan/wiki/Developer-Documentation#preventing-travis-ci-lint-errors-before-submitting-pull-requests)
- [Add Snap settings to code](https://github.com/wekan/wekan/wiki/Adding-new-Snap-settings-to-code) so that feature is default disabled, and can be enabled with Snap commands
- [Add Snap settings to wiki](https://github.com/wekan/wekan-snap/wiki/Supported-settings-keys)
- Add settings also to [Dockerfile](https://github.com/wekan/wekan/blob/edge/Dockerfile)
- [Make your pull request to edge branch](https://github.com/wekan/wekan/wiki/Developer-Documentation#pull-request-workflow-please-read-before-submitting-prs).
- Use the [feature branch](https://www.atlassian.com/git/tutorials/comparing-workflows#feature-branch-workflow) workflow.
  - create a PR from your feature-branch to `wekan/edge` directly so that you can continue your work without interruption.
- Keep your local forks updated with this repo by setting your `git upstream` value as described [here](https://robots.thoughtbot.com/keeping-a-github-fork-updated).
  - before submitting a PR make sure you `rebase` your local branch as described [here](http://push.cwcon.org/learn/stay-updated#on_your_computer_routine_tasks)
  - If you accidentally mess around on your `edge` branch, follow these steps [here](http://push.cwcon.org/learn/stay-updated#oops_i_was_messing_around_on_) to clean it up. Note: currently there is only master branch, not devel or edge branches.
  - [Here is how to remove commits from pull request](https://stackoverflow.com/questions/36168839/how-to-remove-commits-from-pull-request)

## Preventing Travis CI lint errors before submitting pull requests

- NOTE: Travis is currently broken and always shows warnings and errors like variables not defined or not used, so if your code works, ignore Travis.
- Eslint for linting. To prevent Travis CI lint errors, you can test for lint errors by installing `npm install eslint` and running it with `npm run lint` and trying automatic fixing with `eslint --fix filename.js`
- There is also probably not-currently-working as of 2018-05-05 [jsbeautifer website](http://jsbeautifier.org) with settings Indent with 2 spaces (topmost dropdown), [X] Space before conditional: "if(x)" / "if (x)", [X] Use JSLint-happy formatting tweaks.

## Choosing issues to work on

- You are free to select what feature to work on.
  - Leave a comment on an issue saying that you're working on it, and give updates as needed.
  - Work and concentrate on one issue at a time and finish it, before moving to other issue.
- Keep list of your contributions on your personal website.
- Keep track of time it takes to implement each part of a feature, so you can estimate what time it would take to implement similar feature. After implementing feature, review your estimate was it correct, make improvements to your process and estimates, also keeping enough time allocated in estimate if something is harder to implement. Employers look for coders with proven track record.
- You can ask for comments from others, but usually those feature requests are clearly defined how they should work. You can place those Settings options there where it seems most logical for you.

Main point is to be friendly to those commenting of your code, and incorporate those suggestions that make most sense.

# Build Pipeline

- Templates are written in [JADE](https://naltatis.github.io/jade-syntax-docs/) instead of plain HTML. Also see [HTML to JADE converter](http://html2jade.org/).
- CSS is written in the [Stylus](http://stylus-lang.com/) precompiler - see [Stylus to CSS converter](https://mikethedj4.github.io/Stylus2CSS/), and
- Meteor templates are created as BlazeLayout templates.
- Instead of the allow/deny paradigm a lot of the `collections` defined in the project use `mutations` to define what kinds of operations are allowed.

For further details look for the 'feature summaries' in the Wiki (still in progress) otherwise go through the git history and see how old features were built. Might I suggest the Start and Due date feature [wefork#26](https://github.com/wefork/wekan/pull/26)

# Translations

If adding new features, please also support the internationalization features built in. Refer to the [[Translations]] wiki page. 

# Export From Trello

It's possible to import your existing boards from Trello. Instructions [[here|migrating-from-trello]]

# Directory Structure Details

[Directory Structure](https://github.com/wekan/wekan/wiki/Directory-Structure)

# Chat

[![Wekan chat][vanila_badge]][vanila_chat]


[rocket_chat]: https://chat.indie.host/channel/wekan
[vanila_badge]: https://vanila.io/img/join-chat-button2.png
[vanila_chat]: https://community.vanila.io/wekan
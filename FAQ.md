> **»The only stupid question is the one that is not asked.«**  
> *– Hull, E., K. Jackson, et al. (2005).*

## What Wekan is not?
* Not a single Company: It has always been [Open Source](https://en.wikipedia.org/wiki/Open-source_software) and [Free software](https://en.wikipedia.org/wiki/Free_software). Most of the work is done at free time. There is [Commercial Support](https://wekan.team) and [Hosting](https://github.com/wekan/wekan/wiki/Platforms) provided by various companies.
* Not a single Product: There are some missing features, and [more features are added all the time](https://blog.wekan.team). There are [Features of many use cases](https://github.com/wekan/wekan/wiki/Features)
* Not a Startup: We have no exit plan. Wekan is still mostly done at free time, by developers scratching their itch and needing Wekan for their own use cases, so when some support us with [Commercial Support or Bounties](https://wekan.team) it just increases speed of adding new features.
* Not have hired departments: There is no hired marketing team/hired development team/hired QA team. Wekan is tested by it's users. Bugs and feature requests are submitted to [GitHub issues](https://github.com/wekan/wekan/issues).

## What is Wekan?
Wekan is an open-source and free software _[kanban board][kanban]_ that lets you organize things in cards, and cards in lists. More info at [Readme][].

[readme]: https://github.com/wekan/wekan/blob/master/README.md
[kanban]: https://en.wikipedia.org/wiki/Kanban_board

## What is Wekan Team?
[Wekan team](https://github.com/wekan/wekan/wiki/Team) is small amount of contributors from all around the world donating their free time and servers. There is no benevolent dictator. Every Wekan team member is free to choose what to contribute and when. We can not force anybody to implement anything.

## When new version of Wekan will be released? When my pull request will be tested, commented or merged?

Depends on free time of xet7. Usually:
* Fastest: multiple times a day. Sometimes this is 3 releases per day.
* Slowest: Once a month.
* One release contains anything from one typo fix to many major features and bugfixes.

## What Wekan version number means?

* Every release has release date and release number.
* Every release increments release number by 0.01. This practice started 2017-03-05 at v0.12. Before it release number was much more compicated like v0.11.1-rc2. After v0.99 comes v1.00, v1.01, v1.02, etc.
* Version number is only incrementing number. Wekan has been in production use for a long time already, so v1.00 is not about being production ready.
* Wekan still has bugs, like any other software. So this is not about being bug free.
* Wekan will keep changing, and providing migrations from old to newest version. In that sense, Wekan has been LTS release as long as it's been maintained already. There have been many fixes to make migrations possible, and adding more fixes will continue.
* Development happens in devel branch. When release is made, devel branch is merged to master and friend branches.

# Features

## Will my feature request be implemented?

There are alternative ways to have your feature implemented:

a) [Commercial Support or Bounties](https://wekan.team)

b) Pay someone from your company or some other developer to code feature and submit as pull request

c) Develop feature yourself and submit it as pull requests to devel [Wekan repo](https://github.com/wekan/wekan) branch.

[According to Open Hub](https://www.openhub.net/p/wekan), Wekan code is only about 10500 lines without Meteor.js framework and NPM modules, so it's very small when comparing to other software, and quite logically organized. With git history viewer like gitk it's possible to see how different features are implemented.

For Sandstorm-specific features, have the feature enabled in Sandstorm by using environment variable isSandstorm = true like is at wekan/sandstorm.js .

In wiki there is [Developer Documentation](https://github.com/wekan/wekan/wiki/Developer-Documentation).

## Will you accept my pull request?
We totally rely on pull requests for new features and bug fixes. If your pull request works, it's very likely to be accepted by xet7.

## How can I contribute to Wekan?
We’re glad you’re interested in helping the Wekan project! We welcome bug reports, enhancement ideas, and pull requests, in our GitHub bug tracker. Have a look at the [[Contributing notes|developer-documentation]] for more information how you can help improve and enhance Wekan. We are working to make it possible to have bounties for features. We welcome sponsors.

## Are there any tests?
There are near to zero tests, because nobody has contributed tests as pull request.

## Is there a plugin system?
No. It's not possible in web browser to a) Install npm modules inside Docker or b) Install code afterwards on Sandstorm, because application code is read-only and signed. All features in code are built in, and all data related to features is stored on MongoDB.

## Can Wekan be rewritten in another programming language?

Yes. There are following 2 options, depending do you have time or money:

1. Time: You can do the rewrite, and add pull request to Wekan devel branch that implements all of Wekan current functionality in another programming language, including same MIT license, Trello Import, Wekan Import/Export with attachments from all versions of Wekan, migrations from all versions of Wekan MongoDB schema to all other databases, support for same [REST API](https://github.com/wekan/wekan/wiki/REST-API) compatibility, all the same [Platforms](https://github.com/wekan/wekan/wiki/Platforms) support Wekan already has, exactly same look, all of Wekan's bugs fixed and feature requests implemented, scalable multi-layer secure GDPR compliant architecture design and implementation, encrypted database support, 100% test coverage of features, Coverity Scanned security, fully developer and end user documentation for all platforms, and well commented code.

2. Money: 5 year of programming time for new version of Wekan. It is calculated this way: Effort used before adding current Wekan to GitHub is likely minimum 2 years, and after adding Wekan to GitHub, current version of Wekan is [3 years of effort](https://www.openhub.net/p/wekan) that includes [2 years of programming time](https://www.openhub.net/p/730403/contributors/3137056998714607) by xet7, so that makes total 5 years that was used to implement current version of Wekan, so I expect that same would be needed for rewrite. Monthly salary needs to be enough, so I can pay my bills and loans and live normal life with enough time to rest from coding, please contact x@xet7.org for more details.

# History

## Weren't you called Libreboard before?
Yes, Libreboard was the old project name, which superseded the even older project name Metrello. As the original name suggests, Metrello was a Trello clone built with Meteor. It used a lot of the original assets from Trello and even the name was very similar. When the project turned more mature and gained more interest by the community, this was obviously a [problem]. To get its own identity and due to a DMCA from Trello, efforts started to [redesign] Metrello, which also included to find a new name and so Maxime Quandalle came up with “OpenBoard”, to underline the open source nature of the project. Unfortunately the com domain was already taken and so she replaced the Open with Libre, which stands for free (as in freedom) in many Latin derived languages.

After renaming it to Libreboard, a [new logo] was designed and the project continued to live on as Libreboard. Unfortunately it turned out, that the new logo was apparently ripped-off from a [concept] published at Dribbble, and so a new logo had to be found. There were a lot of [ideas from the community][logo-ticket], and at the end Maxime [proposed][wekan-proposal] a completely new name, Wekan, together with a design proposal for a new logo.

## What was Wekan fork / Wefork?
After 2016-09-02 there were no pull requests reviewed and integrated for nearly 2 months. At 2016-10-20 Wekan community created fork and started merging many bugfixes and new features into Wefork. 2017-01-29 Wekan author mquandalle gave access to Wekan and at 2017-01-31 xet7 started merging Wefork back to Wekan. 2017-02-08 All of Wefork is now merged and moved back to official Wekan. Wefork will not accept any new issues and pull requests. All development happens on Wekan. [Wefork announcement and merging back](https://github.com/wekan/wekan/issues/640#issuecomment-276383458), more info: [Team](https://github.com/wekan/wekan/wiki/Team)

## What is the difference between Wekan and Trello?
The main difference between the two is that Wekan is completely open source and available under the permissive MIT license. That makes it possible to host it on your own server (or your company's or organization's server) and you keep the full control over all data. No need to fear it will disappear some day, like a commercial service like Trello could.  
Additionally the long term goal is to have features that are not available on Trello or other alternatives, making Wekan flexible and suitable for complex project organizations.

## Why does Wekan look so different now compared to < v0.9?
Wekan started as a just for fun project to explore meteor and its features and the initial version had a lot of the Trello assets (CSS, Images, Fonts) in it and copied a lot of its design. Due to an DMCA takedown notice and obviously to get its own identity, the old design was dropped after v0.8 and a new UI was developed

See the related tickets [#92] and [#97] for more information.

[#92]: https://github.com/wekan/wekan/issues/92
[#97]: https://github.com/wekan/wekan/issues/97

# Etiquette

## Why am I called a troll?
* You want a feature, but you add thumbs down emoji reactions
* You are adding image reactions
* You want priorities changed. Current priorities are:
  * [High priority](https://github.com/wekan/wekan/issues?q=is%3Aissue+is%3Aopen+label%3AHigh-priority): security issues and high severity bugs
  * Medium priority: Import/Export
  * Others. Actual roadmap will be updated later.
* You write that you are providing constructive criticism
* You think that free software includes free implemented features
* You are adding something other than:
  * Thumbs up reactions to existing posts
  * Feature specs
  * Technical details
  * Links to related documentation
  * Links to example code to get a feature implemented
  * Pull requests

## Why am I called a spammer?
* You are adding new comments that have only content like:
  * +1
  * +1 I can confirm this
  * +1 It would be great to have this
  * +1 This is the only feature for preventing my company to move to Wekan
* You are adding something other than:
  * Thumbs up reactions to existing posts
  * Feature specs
  * Technical details
  * Links to related documentation
  * Links to example code to get a feature implemented
  * Pull requests

## What you should do if you see a troll or a spammer?
Add only one link to this FAQ. Do not in any way comment or feed the trolls.

[problem]: https://github.com/wekan/wekan/issues/92
[redesign]: https://github.com/wekan/wekan/issues/94
[new logo]: https://github.com/wekan/wekan/issues/64#issuecomment-69005150
[concept]: https://dribbble.com/shots/746215-Pigeon
[logo-ticket]: https://github.com/wekan/wekan/issues/64#issuecomment-74357809
[wekan-proposal]: https://github.com/wekan/wekan/issues/64#issuecomment-135221046

---

# Sandstorm

## What Sandstorm is not anymore?
Not a Company, Not a Startup, Not a Product with Enterprise version. Everything is now [Open Source](https://en.wikipedia.org/wiki/Open-source_software) and [Free software](https://en.wikipedia.org/wiki/Free_software).

## What is Sandstorm?
[Sandstorm](https://sandstorm.io) is a open-source and free software security audited platform with grains, logging, admin settings, server clustering and App Market. App Market has Wekan as installable App. SSO options like LDAP, passwordless email, SAML, GitHub and Google Auth are already available on Sandstorm. Sandstorm is preferred platform for Wekan, as it would take a lot of work to reimplement everything in standalone Wekan. 

## How can you contribute to Sandstorm?
See [Sandstorm website about contributing pull requests](https://sandstorm.io) and [returning to Open Source community roots, including donation info](https://sandstorm.io/news/2017-02-06-sandstorm-returning-to-community-roots).


> **»The only stupid question is the one that is not asked.«**  
> *– Hull, E., K. Jackson, et al. (2005).*

## What Wekan is not?

* Not a Company: It's all [Open Source](https://en.wikipedia.org/wiki/Open-source_software) and [Free software](https://en.wikipedia.org/wiki/Free_software)
* Not a Product: There are missing features.
* Not a Startup: We have zero budget. We have no exit plan. We have no investors.
* Not have hired departments: There is no hired marketing team/hired development team/hired QA team

## Why am I called a troll?
You want a feature, but you add thumbs down emoji reactions. You are adding image reactions. You want priorities changed (we don't have priorities). You are providing contructive criticism. You think that free software includes free implemented features. You are adding something other thumbs up reactions to existing posts, feature specs, technical details, code etc info related to really getting a feature implemented.

## Why am I called a spammer?
You are adding new comments that have only content like "+1", "+1 I can confirm this", "+1 It would be great to have this", "+1 This is the only feature for preventing for my company to move to Wekan". You are adding something other than thumbs up reactions to existing posts, feature specs, technical details, code etc info related to really getting a feature implemented.

## What you should do if you see a troll or a spammer?
Add only one link to this FAQ. Do not in any way comment or feed the trolls.

## Will my feature request be implemented?
Being popular feature request does not mean that feature will be implemented. It just means that nobody has needed that feature so much to even try to implement it themselves and submit pull request, or find some depeloper and pay him/her to implement it and submit pull request.

## Do you accept sponsors to pay for features?
Yes. But there have been no monetary sponsors yet at least for me, xet7, and I don't know about others.

## What is Wekan?
As already explained in detail in our [Readme][], Wekan is an open-source _[kanban board][kanban]_ that lets you organize things in cards, and cards in lists.

[readme]: https://github.com/wekan/wekan/blob/master/README.md
[kanban]: https://en.wikipedia.org/wiki/Kanban_board

## What is Wekan Team?
Wekan team is small amount of contributors from around the world donating their free time, servers etc. There is no benevolent dictator. Every Wekan team member is free to choose what to contribute and when. We can not force anybody to implement anything.

## Will you accept my pull request?
We totally rely on pull requests for new features and bug fixes. If your pull request works, it's very likely to be accepted by xet7.

## Are there any tests?
There are near to zero tests, because nobody has contributed tests as pull request.

## Is there a plugin system?

No. It's not possible in web browser to a) Install npm modules inside Docker or b) Install code afterwards on Sandstorm, because application code is read-only and signed. All features in code is built in, and all data related to features is stored on MongoDB.

## Weren't you called Libreboard before?
Yes, Libreboard was the old project name, which superseded the even older project name Metrello. As the original name suggests, Metrello was a Trello clone built with Meteor. It used a lot of the original assets from Trello and even the name was very similar. When the project turned more mature and gained more interest by the community, this was obviously a [problem]. To get it's own identity and due to a DMCA from Trello, efforts started to [redesign] Metrello, which also included to find a new name and so Maxime Quandalle came up with “OpenBoard”, to underline the open source nature of the project. Unfortunately the com domain was already taken and so she replaced the Open with Libre, which stands for free (as in freedom) in many Latin derived languages.

After renaming it to Libreboard, a [new logo] was designed and the project continued to live on as Libreboard. Unfortunately it turned out, that the new logo was apparently ripped-off from a [concept] published at Dribbble, and so a new logo had to be found. There were a lot of [ideas from the community][logo-ticket], and at the end Maxime [proposed][wekan-proposal] a completely new name, Wekan, together with a design proposal for a new logo.

[problem]: https://github.com/wekan/wekan/issues/92
[redesign]: https://github.com/wekan/wekan/issues/94
[new logo]: https://github.com/wekan/wekan/issues/64#issuecomment-69005150
[concept]: https://dribbble.com/shots/746215-Pigeon
[logo-ticket]: https://github.com/wekan/wekan/issues/64#issuecomment-74357809
[wekan-proposal]: https://github.com/wekan/wekan/issues/64#issuecomment-135221046

## What was Wekan fork / Wefork?
After 2016-09-02 there were no pull requests reviewed and integrated for nearly 2 months. At 2016-10-20 Wekan community created fork and started merging many bugfixes and new features into Wefork. 2017-01-29 Wekan author mquandalle gave access to Wekan and at 2017-01-31 xet7 started merging Wefork back to Wekan. 2017-02-08 News: All of Wefork is now merged and moved back to official Wekan. Wefork will not accept any new issues and pull requests. All development happens on Wekan. [Wefork announcement and merging back][https://github.com/wekan/wekan/issues/640#issuecomment-276383458], more info: [Team](https://github.com/wekan/wekan/wiki/Team)

## What is the difference between Wekan and Trello?
The main difference between the two is that Wekan is completely open source and available under the permissive MIT license. That makes it possible to host it on your own server (or your company's or organization's server) and you keep the full control over all data. No need to fear it will disappear some day, like a commercial service like Trello could.  
Additionally the long term goal is to have features that are not available on Trello or other alternative, making Wekan flexible and suitable for complex project organizations.

## Why does Wekan looks so different now compared to < v0.9?
Wekan started as a just for fun project to explore meteor and it's features and the initial version had a lot of the Trello assets (CSS, Images, Fonts) in it and copied a lot of it's design. Due to an DMCA takedown notice and obviously to get its own identity, the old design was dropped after v0.8 and a new UI was developed

See the related tickets [#92] and [#97] for more information.

[#92]: https://github.com/wekan/wekan/issues/92
[#97]: https://github.com/wekan/wekan/issues/97

## How can I contribute to Wekan?
We’re glad you’re interested in helping the Wekan project! We welcome bug reports, enhancement ideas, and pull requests, in our GitHub bug tracker. Have a look at the [[Contributing notes|developer-documentation]] for more information how you can help improve and enhance Wekan.
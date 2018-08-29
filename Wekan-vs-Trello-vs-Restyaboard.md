Anyone, please feel free correct if there is anything wrong or outdated info below. Comparison below is based on info found at Restya website, and xet7's current info about Wekan, but because all these are actively developed then this comparison most likely goes outdated soon.


Features | Wekan | Trello | Restyaboard
------------ | ------------- | ------------- | -------------
Price | Free and Open Source, MIT license. Free for Commercial Use. | Free, Monthly payment, Annual Subscription, Quote-based | Open Core
Hosting | Self-host or SaaS provider | SaaS | Self-host

## Basic features: Board

Features | Wekan | Trello | Restyaboard
------------ | ------------- | ------------- | -------------
Activities fetch | WebSocket | WebSocket | Polling (Better, for easy scaling)
Multiple language | Yes | Yes | Yes
Keyboard shortcuts | Yes | Yes | Yes
Boards | Yes | Yes | Yes
Closed boards listing | Yes, at Recycle Bin | Yes | Yes
Starred boards listing | No, starred and non-starred at All Boards | No | Yes
Add board with predefined templates | Import Board from Trello or Wekan | No | Yes
Board stats | [Yes](https://github.com/wekan/wekan/wiki/Features#stats) | No | Yes
Board - Add members | Yes | Yes | Yes
Board - Remove members | Yes | Yes | Yes
Close board | Yes, move to Recycle Bin | Yes | Yes
Subscribe board | Yes | Yes | Yes
Copy board | Export / Import board | Yes | Yes
Starred board | Yes | Yes | Yes
Unstarred board | Yes | Yes | Yes
Swimlanes | Yes | External [Chrome Add-On](https://chrome.google.com/webstore/detail/swimlanes-for-trello/lhgcmlaedabaaaihmfdkldejjjmialgl) and [Firefox Add-On](https://addons.mozilla.org/en-US/firefox/addon/swimlanes-for-trello/) | No
Board text list view | No | No | Yes
Board calendar view | Yes | Yes | Yes
Board sync with google calendar | No | Yes | Yes

## Basic features: Lists

Features | Wekan | Trello | Restyaboard
------------ | ------------- | ------------- | -------------
Create list | Yes | Yes | Yes
List color | No | No | Yes
Copy list | No | Yes | Yes
Move list | No. Only at same board with dragging. | Yes | Yes
Subscribe list | Yes | Yes | Yes
Remove list | Yes | Yes | Yes
Move all cards in this list | No. Only multiselect-drag to the same board. | Yes | Yes
Archive all cards in this list | No | Yes | Yes
Archive this list | Yes. Move list to Recycle Bin. | Yes | Yes
Show attachments in list | No. Only on card. | No | Yes

## Basic features: Cards

Features | Wekan | Trello | Restyaboard
------------ | ------------- | ------------- | -------------
Filter cards | Yes, also with Regex | Yes | Yes
Archived items | Yes, at Recycle Bin | Yes | Yes
Card stickers | No | Yes | No
Card labels | Yes | Yes | Yes
Card labels color change | Yes | Yes | Yes
Cards | Yes | Yes | Yes
Create cards | Yes | Yes | Yes
Instant add card | No | No | $ Yes
Add cards & reply via Email | No | Yes | Yes
Multiple card view | No | No | Yes
Expandable card view | No | No | Yes
Card ID display	| No | No | Yes
Card color on card list | No | No | Yes
Card action on card list | Only multiple selection and WIP Limit | Yes | No
Card - Set due date | Yes | Yes | Yes
Card - Add members | Yes | Yes | Yes
Card - Remove members | Yes | Yes | Yes
Card - Add labels | Yes | Yes | Yes
Card - Add checklist | Yes | Yes | Yes
Card - Add attachment | Yes | Yes | Yes
Move card | Yes | Yes | Yes
Copy card | Yes | Yes | Yes
Subscribe card | Yes | Yes | Yes
Archive card | Yes, move to Recycle Bin | Yes | Yes
Vote card | No | Yes | Yes
Share card | No | Yes | Yes
Print card | No | Yes | No
Add comment on card | Yes | Yes
Reply comment on card | No | No | Yes
Remove comment on card | Yes | Yes | Yes
Nested comments | No | No | Yes
Card resizable view | No | No | Yes
Show attachments in card | Yes. Also images in slideshow. | Yes | Yes
Card history filtering | No | No | Yes
Button to delete all archived items | [Not yet](https://github.com/wekan/wekan/issues/1625) | No | Yes

## Basic features: Checklists

Features | Wekan | Trello | Restyaboard
------------ | ------------- | ------------- | -------------
Checklist - Add item | Yes | Yes | Yes
Checklist - Remove item | Yes | Yes | Yes
Checklist - Convert to card | No | Yes | Yes
Checklist - Mention member | No | Yes | Yes
Checklist - Select emoji | No | Yes | Yes

## Basic features: Search

Features | Wekan | Trello | Restyaboard
------------ | ------------- | ------------- | -------------
Search | On same board, also with regex. And add linked card search from any board. | Yes | $ Yes
Save search | No | Yes | No

## Basic features: Organizations

Features | Wekan | Trello | Restyaboard
------------ | ------------- | ------------- | -------------
Organizations list on profile | No | Yes | Yes
Organizations | [Not yet](https://github.com/wekan/wekan/issues/802) | Yes | Yes
Change organization on board | [Not yet](https://github.com/wekan/wekan/issues/802#issuecomment-416474860) | Yes | Yes
Organizations - Add members | No | Yes | Yes
Organizations - Remove members | No | Yes | Yes
Organizations - Members change permissions | No | Yes | Yes
Create organization with types | No | Yes | No
Organizations - Sorting list | No | No | Yes
Organizations - Activities list | No | Yes | Yes
Organizations settings | No | Yes | Yes
Organizations visibility | No | Yes | Yes
Organizations - Membership restrictions | No | Yes | Yes
Organizations - Board creation restrictions | No | Yes | Yes
Remove organization | No | Yes | Yes

## Basic features: Offline

Features | Wekan | Trello | Restyaboard
------------ | ------------- | ------------- | -------------
Offline sync - use without internet | No. You can install Wekan to your own computer and use it locally. | No | Yes

## Basic features: Diff, Revisions and Undo

Features | Wekan | Trello | Restyaboard
------------ | ------------- | ------------- | -------------
Undo from activities | No | No | Yes

## Basic features: JSON API

Features | Wekan | Trello | Restyaboard
------------ | ------------- | ------------- | -------------
API explorer | No | No | Yes
Developer applications | Yes, using REST API | Yes | Yes
Authorized OAuth applications | No, REST API is password login for admin | Yes | Yes
Webhooks | Yes | Yes | Yes
Zapier (IFTTT like workflow automation with 500+ websites) | Yes | Yes | $ Yes
Integrated IFTTT | [Not yet](https://github.com/wekan/wekan/issues/1160) | No | No

## Basic features: Email and Notifications

Features | Wekan | Trello | Restyaboard
------------ | ------------- | ------------- | -------------
Email-to-board settings | No, requires your code to use REST API | Yes | Yes
Email templates management | No | No | Yes
Notifications settings | No | Yes | Yes
Disable desktop notification | No desktop notifications | No | Yes
User configuration to change default subscription on cards and boards | No | No | Yes
Card notification & highlight | No | No | Yes
Notification for card overdue | No | Yes | Yes

## Basic features: Settings

Features | Wekan | Trello | Restyaboard
------------ | ------------- | ------------- | -------------
Additional settings | No in Web UI, most settings at CLI | Yes | Yes (Basic only)
Profile	| Yes | Yes | Yes
Add a new email address | Register / Invite | Yes | No
Roles management | [Not yet](https://github.com/wekan/wekan/issues/1861) | No | Yes
Settings management | Only some at Web UI, most settings at CLI | No | Yes
Users management | Standalone Admin Panel: Yes edit, no add/remove user. | No? | Yes
Permanently delete your entire account forever?	| No | Yes | Yes (Admin can delete)

## Apps for productivity: Login

Features | Wekan | Trello | Restyaboard
------------ | ------------- | ------------- | -------------
Login with username or email | Yes | Yes | Yes
LDAP login | Standalone: [Not yet](https://github.com/wekan/wekan/pull/1826). Sandstorm: Yes. | No | $ Yes
SAML login | Standalone: Rocket.Chat SAML => Wekan App [OAuth2](https://github.com/wekan/wekan/wiki/OAuth2). Sandstorm: Yes | No | No
Google login | Yes, [OAuth2](https://github.com/wekan/wekan/wiki/OAuth2) | Yes | No
GitHub login | Standalone: Yes, [OAuth2](https://github.com/wekan/wekan/wiki/OAuth2). Sandstorm: Yes. | No | No
Passwordless email login | Standalone: No. Sandstorm: Yes. | No | No

## Apps for productivity: Import / Export

Features | Wekan | Trello | Restyaboard
------------ | ------------- | ------------- | -------------
Import board from Trello | Yes | No | Yes
Import board from Wekan | Yes | No | Yes
Import from GitHub | No | No | $ Yes
Export board to Wekan JSON, includes attachments | Yes | No | ?
Export board to CSV | [Not yet](https://github.com/wekan/wekan/pull/413) | $ Yes | $ Yes
Export JSON card | No | Yes | No
Export CSV card | No | No | Yes
Change visibility | Yes | Yes | Yes
Change visibility in boards listing | No | No | Yes
Activities difference between previous version | No | No | Yes
Change background | Color only | Color and image | Color and image
Change background - custom | No | $ Gold or Business Class Only | Yes
Background image from flickr | No | No | Yes
Productivity beats | No | No | Yes (Alpha)
Show attachments in board | No (not at All Boards view, only on Cards) | No | Yes

## Apps for productivity

Features | Wekan | Trello | Restyaboard
------------ | ------------- | ------------- | -------------
Apps (Power-ups) | All integrated in, no separate plugin/app  install | Yes | Yes
Custom Field App | [Yes](https://github.com/wekan/wekan/wiki/Custom-Fields) | Yes | $ Yes
Estimated Time Custom Field App | No | No | $ Yes
Analytics | [Magento integration](https://github.com/wekan/wekan-snap/wiki/Supported-settings-keys) | No | No
Hide card additional information | Yes, card and board activities | Yes, card activities | Yes, card activities
Board Gantt view | No | No | $ Yes
Activities listing | No, only at board | No | Yes
Introduction video | No | No | Yes
List sorting by due date | No | No | Yes
Home screen | No | No | Yes
Apps Integration | All integrated in | Yes | Yes
Chat | No. You could use Rocket.Chat etc. | No | $ Yes
Dashboard Charts | No | No | $ Yes
Hide Card Created Date App | No | No | Yes
Hide Card ID App | No | No | Yes
Canned Response App | No | No | $ Yes
Auto Archive Expired Cards App | No | No | $ Yes
Support Desk | No | No | $ Yes
Card Template App | Copy Checklist Template to Multiple Cards | Yes | $ Yes
Slack | [Yes](https://github.com/wekan/wekan/wiki/Outgoing-Webhook-to-Discord) | Yes |  $ Yes
Amazon Echo | No | No | $ Yes
Collaborate/TogetherJS | [Not yet](https://github.com/wekan/wekan/wiki/Friend) | No | Yes
Gmail Add-on | No | Yes | Yes
Hangouts Chat bot | No | Yes | $ Yes
Print board | No | No | $ Yes

## Apps for productivity: Checklist Templates

Features | Wekan | Trello | Restyaboard
------------ | ------------- | ------------- | -------------
Website QA Checklist | No | No | $ Yes
SEO Checklist | No | No | $ Yes

## Apps for productivity: Mobile Apps

Features | Wekan | Trello | Restyaboard
------------ | ------------- | ------------- | -------------
iOS Mobile App | [Not yet](https://github.com/wekan/wekan/wiki/Friend) | Yes | Yes
Android Mobile App | [Not yet](https://github.com/wekan/wekan/wiki/Friend) | Yes | No
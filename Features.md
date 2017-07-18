# Current

### Kanban

* Boards: List of all your public and private boards, board shortcuts at top of page
* Members: Invite new member, permissions Admin/Normal/Comment only, drag-drop member to assign to task
* Lists: Add, archive and restore archived, delete list.
* Cards: Description, Customizable Labels, Checklists, Attachment images and files, Comments. Arhive and restore archived card. Delete card.
* Multi-selection => Checkmark select cards => drag-drop all selected to some list
* [Markdown in card description and comments](https://github.com/wekan/wekan/issues/1038)
* Filtered views
* [International Date Formatting for Due Date according to language](https://github.com/wekan/wekan/issues/838)

### Authentication, Admin Panel, SMTP Settings

* Source and Docker platforms: [Admin Panel](https://github.com/wekan/wekan/blob/devel/CHANGELOG.md#v0111-rc2-2017-03-05-wekan-prerelease): Self-registration, or change to invite-only and inviting users to boards. SMTP Settings.
* Sandstorm Platform: Admin: LDAP, passwordless email, SAML, GitHub and Google Auth. Add and remove users. SMTP Settings. Wekan, Rocket.Chat, etc apps available with one click install.

### Import

* Import Trello board: Text, labels, images, comments, checklists. Not imported yet: stickers, etc.
* [Import Wekan board](https://github.com/wekan/wekan/pull/1117): Text, labels, images, comments, checklists.

### Export

* Export Wekan board: [Export menu item above the board archive item, when you click the sandwich bar icon on the top right](https://github.com/wekan/wekan/pull/1059). If Export menu is not visible, you can change [Export menu to be visible by setting yourself as board admin in MongoDB](https://github.com/wekan/wekan/issues/1060).

### Working with big boards

* [JSON tools, copying files to clipboard](https://github.com/wekan/wekan/issues/610#issuecomment-310862951)

### API

* [REST API](https://github.com/wekan/wekan/issues/1037)

### Webhooks

* [Outgoing Webhooks](https://github.com/wekan/wekan/pull/1119)

### Cleanup

* [Wekan database cleanup script](https://github.com/wekan/wekan-cleanup)
* [Docker cleanup](https://github.com/wekan/wekan/issues/985)

### Stats

* [Daily export of Wekan changes as JSON to Logstash and
ElasticSearch / Kibana (ELK)](https://github.com/wekan/wekan-logstash)
* [Statistics Python script for Wekan Dashboard](https://github.com/wekan/wekan-stats)
* [Console, file, and zulip logger on database changes](https://github.com/wekan/wekan/pull/1010) with [fix to replace console.log by winston logger](https://github.com/wekan/wekan/pull/1033)

### Versions of Meteor and Node

* Upgraded to [Meteor 1.4](https://github.com/wekan/wekan/pull/957) and [Node v4](https://github.com/wekan/wekan/issues/788) on [meteor-1.4 branch](https://github.com/wekan/wekan/tree/meteor-1.4)

# Already merged, will be at next version

* [Changelog](https://github.com/wekan/wekan/blob/devel/CHANGELOG.md)

# Wishes for pull requests

### Existing pull requests, cleanup/cherry-picking/new pull requests welcome

* [Export/Import Excel TSV/CSV data](https://github.com/wekan/wekan/pull/413)
* [Move/Clone Board/List](https://github.com/wekan/wekan/pull/446) and [Move or copy cards from one board to another](https://github.com/wekan/wekan/issues/797) that [needs help in implementation](https://github.com/wekan/wekan/issues/979)
* [Replace CollectionFS with meteor-file-collection](https://github.com/wekan/wekan/pull/875)

### Wishes for API pull requests

* [Using API to script Email to board/card, notifications on cards to email, etc](https://github.com/wekan/wekan/issues/794)

### Wishes for Admin Panel

* [SMTP test, show possible errors on that test webpage](https://github.com/wekan/wekan/issues/949)
* [Teams/Organizations](https://github.com/wekan/wekan/issues/802) including Add/Modify/Remove Teams/Users/Passwords and Private/Public Team settings
* [Themes](https://github.com/wekan/wekan/issues/781) and making custom apps with Themes

### Wishes for Boards

* [Custom fields](https://github.com/wekan/wekan/issues/807)
* [Children/Related cards](https://github.com/wekan/wekan/issues/709), subtasks. Dependencies. 
* [Top Level Projects](https://github.com/wekan/wekan/issues/641)
* [Swimlanes (rows)](https://github.com/wekan/wekan/issues/955)
* Kanban workflows
* Gantt charts
* [WIP limits](https://github.com/wekan/wekan/issues/783)
* [Timesheet/Time tracking](https://github.com/wekan/wekan/issues/812)
* Managing website
* [Same cards, multiple column sets](https://github.com/wekan/wekan/issues/211), related to [Themes](https://github.com/wekan/wekan/issues/781)
* [Calendar view](https://github.com/wekan/wekan/issues/808)
* [Vote on cards, number of votes, average](https://github.com/wekan/wekan/issues/796)
* [Board templates](https://github.com/wekan/wekan/issues/786)
* [Checklist templates](https://github.com/wekan/wekan/issues/904)

# More

[Platforms](https://github.com/wekan/wekan/wiki/Platforms)

[Integrations](https://github.com/wekan/wekan/wiki/Integrations)
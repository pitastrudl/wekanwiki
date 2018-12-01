# Wekan - Open Souce kanban - IRC FAQ

- [Wekan website](https://wekan.github.io)

## QA, answers by [xet7](https://github.com/xet), Maintainer of Wekan

## Answers to IRC questions are added to this wiki page, because most coming to IRC channel leave immediately, and don't wait for answer. Real IRC users know idling and stay at IRC channel. It is required that you read everything in this page before coming to IRC channel.

***

### Q: LDAP?

A: [LDAP for Standalone is now available](https://github.com/wekan/wekan/wiki/LDAP).

```
[17:56:10] <regdude> Hi! I'm trying to setup Wekan with LDAP,
but can't seem to get it to work.
Where could I found logs for why LDAP is not working?
[17:56:18] <regdude> does not seem to send out any LDAP packets
[17:58:31] <regdude> oh, it does not do anything
```

Please see is there existing issues at [LDAP Bugs and Feature Requests](https://github.com/wekan/wekan-ldap/issues), or add a new one.


### Q: Wekan Internal Server Error

2018-11-09

```
[20:45:22] <Rojola> hi
[20:45:35] <Rojola> Before I came here, I tried to find a solution myself
[20:46:17] <Rojola> e.g. I read the error log, read the installation troubleshooting docs, did research, and played around with the SMTP settings
[20:46:52] <Rojola> then I joined #sandstorm but nobody replied
[20:47:07] <Rojola> The problem:
[20:47:31] <Rojola> I always get an "Internal Server Error" when I try to send me the registration email
[20:49:15] <Rojola> https://filebin.net/11q54qsyd7rigpiq/internal_server_error.png?t=ziblx18b
[20:49:28] <Rojola> in theory, sandstorm + wekan is installed
[20:49:35] <Rojola> but, in reality I can not access it
```

A: See 4) at https://github.com/wekan/wekan/wiki/Adding-users . This is Stanalone Wekan (Snap, Docker, Source) email setting. This has nothing to do with Sandstorm.

***

### Q: 2018-11-07 Answer speed
```
[12:50:46] <gros> hey
[12:53:45] <gros> I won't whine, because I know sometimes it is
hard to answers to user's questions, but I'm here
since several days, I see that other users asks some things,
and no one is answering
[12:58:11] <gros> I think that you could close this channel in fact,
it will make win time for users
[12:58:24] <gros> and again I don't whine, thanks for the great Wekan :)
```
A:

- Fastest: If you want fast answers, get [Commercial Support](https://wekan.team/commercial-support/).
- Medium speed: If you have time to wait, [add new GitHub issue](https://github.com/wekan/wekan/issues).
- Slow: [Wekan Community Chat with webbroser and mobile Rocket.Chat](https://chat.vanila.io/channel/wekan)
- Slowest: If you want to chat on IRC, please stay at IRC idling, and ask question again also at some other day. Sometimes there is Internet connectivity issues, if it looks like xet7 is not online. IRC is very nice, some Wekan users prefer it. Answers to IRC questions are added to this wiki page, because most coming to IRC channel leave immediately, and don't wait for answer.

***

### Q: SMTP sending to own domain but not Gmail
```
[16:18:47] <k_sze> Does anybody have an idea why I can send e-mail from Wekan
to my personal domain, but not to a Gmail address?
[17:34:16] <k_sze> And now Wekan doesn't actually work. I set it up
from Snap on Ubuntu 18.04.
[17:34:32] <k_sze> (Wekan doesn't work after I reboot Ubuntu)
[17:38:51] <k_sze> Like, I get 502 Bad Gateway from my nginx reverse proxy
```

A: Did you set your domain SPF records (as TXT records) and DKIM records on your domain that your SMTP server uses? Problem is not in Wekan, it's your SMTP server. For example AWS SES works. Also see [Troubleshooting Email](https://github.com/wekan/wekan/wiki/Troubleshooting-Mail).

***

### Q: Integrating Wekan
```
[03:32:12] <ajay> Hi  can anyone tell me how to integrate wekan in
other applications
[03:32:50] <ajay> i am want to integrate it in QGIS for task management
[03:33:01] <ajay> *i want
```
A: Use [Wekan REST API](https://github.com/wekan/wekan/wiki/REST-API). For example, see [Wekan Gogs integration](https://github.com/wekan/wekan-gogs). You can also use [Outgoing Webhooks](https://github.com/wekan/wekan/wiki/Outgoing-Webhook-to-Discord) to send data to some Incoming Webhook. There is also [IFTTT Rules](https://github.com/wekan/wekan/wiki/IFTTT) for some automations.

***

### QA: Rescuing Subtask board
```
[18:33:29] <wekanuser> hello I have a wekan board that
never loads, I just get the spinner. all the other
boards are working fine. This happened after we moved
some subtasks from a subtask board to the main board.
any tips would be appreciated. thanks.
[18:33:58] <xet7> wekanuser: What Wekan version?
[18:34:45] <xet7> Can you move subtasks back to subtask board?
[18:42:02] <wekanuser> v 1.55.0. re: move tasks back to
subtask board - I can't, since the parent board will not load.
[18:42:35] <wekanuser> - I was in subtask board, and moved
manually each subtask over to parent board. Then went to
parent board and it will not load.
[18:43:28] <wekanuser> - the cards would not load on
the main board, but I was able to make an "export"
of the board from the GUI and re-imported it, to another
board but only a fraction of the stories and swimlanes were there.
[18:43:58] <wekanuser> - when I accessed the parent board
via the rest api, I see all my cards, looks like everything is there
[18:44:07] <wekanuser> - so something is hanging on loading the board
[18:44:32] <xet7> Do you still need subtasks on board?
[18:45:09] <wekanuser> no, since the subtasks on the subtasks
board have been moved, there should be nothing "linking" there
[18:46:11] <xet7> Do you see any subtask related in
exported JSON file? So you could remove subtasks from it before importing?
[18:47:06] <wekanuser> thanks, I will check
[18:47:34] <xet7> Does the exported JSON file have all data of
that board? You could check do you see same as with API
[18:47:56] <xet7> You can also create new board that is
similar structure of your exported board, and compare structure
[18:48:52] <xet7> Also please add new issue to
https://github.com/wekan/wekan/issues about what happened,
so somebody can think how to prevent that happening.
[18:52:53] <wekanuser> it appears the json file has all the data
[18:54:04] <xet7> Nice :) Then you can compare it with similar
working board, what is different
[18:54:39] <xet7> Does it have any custom fields?
[18:55:02] <xet7> sometimes removing custom fields makes import work
[18:56:05] <wekanuser> yes there are custom fields, I will consider
trying that. re: removing subtasks, you mean the subtask cards?
or the subtask references in parent cards?
[18:56:27] <xet7> Try first remove subtask references
[18:56:49] <xet7> compare to other exported board JSON that
does not have any subtasks
[18:57:38] <xet7> You don't need to try removing
custom fields yet, there has been some custom fields fixes
[18:58:14] <xet7> I would think that when there is
references to not existing subtasks then that could bring those problems
[19:10:37] <wekanuser> thanks, working on remove subtask refs'
[19:12:31] <wekanuser> I assume that is making
parentId :"" empty,
as I see only subtasks referencing parents,
not parents referencing subtasks
[21:54:39] <wekanuser> update: process of elimination
lead to the import board working if I remove all all
activities from the json file before import
[21:56:47] <xet7> Nice :) Then I think I should not
include activities in export.
[22:03:06] <wekanuser> is there an option to exclude
things from export? I only see the "BUTTON" that does an export
[22:06:16] <xet7> not yet
[22:07:19] <wekanuser> I am probing for possible bad activity item
[22:08:00] <xet7> Probably some activity types are not imported correctly
[19:22:59] <wekanuser> thanks for the help yesterday,
board has been restored.  I will document my issue in a real ticket,
hopefully it will help someone else. Thanks again
[19:23:13] <xet7> :)
```

***

### QA: Wekan in iFrame
```
[17:42:12] <siqueira> Hi, I want to embed my Kanban
from wekan in my website using iframe. Does Wekan
support this feature?
[18:13:59] <xet7> siqueira: Yes, set trusted-url to
your web address that iframes Wekan
https://github.com/wekan/wekan-snap/wiki/Supported-settings-keys
[18:15:35] <xet7> siquiera: If you have problems with browser
javascript console, or something not working, you can
also set browser-policy-enabled='false' that enables
all iframing - but that has a little less security
[18:18:13] <xet7> siquiera: Problem with iframing
Wekan is that link to card does not work well.
For that it's better to have Wekan in sub-url, and
add "iframe" replacing HTML/CSS at beginning of
body tag, and at end of body tag, but that
feature is not yet in Wekan, I'm currently developing it.
[19:25:07] <siqueira> xet7, Thanks a lot
for the information! I just want to have my
public tasks on my website. I think the
browser-policy-enabled can solve my problem,
until I wait for the new feature. Thanks :)
[19:25:51] <xet7> siqueira: You can set
board as public, and provide that public link in iframe.
[19:27:32] <siqueira> I will try it :)
```

***

### Q: Docker reverse proxy

```
yogab> Hi! How are you today ? Can i ask
a docker x reverse proxy x wekan question here ?
```

A: Hmm, it seems you did not ask. Just guessing, maybe it's about [Traefik reverse proxy and Docker](https://github.com/wekan/wekan/wiki/Traefik-and-self-signed-SSL-certs).

***

### Congratulations ! You did read the whole IRC FAQ !

Your next requirement is to tick following box to paper you write on post-it-note attached to
your laptop display:

[_] From beginning of today ____________ (YYYY-MM-DD) I will stay at Wekan IRC channel
for at least one week without leaving IRC channel, keeping IRC channel open
and logged in for 24h x 7 days, so that I can get license to ask questions and wait
patiently for the whole week for answer without leaving IRC channel.

Now:

a) If you are able to all of above and tick that box, you have now have license
to Enter Freenode IRC #wekan and idle at IRC channel for one week.
You can also ask question when you have promised to wait for answer for one week.

b) If you would like to get your answer sooner, you can add search about
existing GitHub issues, and if there is not any, add new GitHub issue to [Wekan Feature Requests and Bugs](https://github.com/wekan/wekan/issues). Also at IRC chat scrolls up and details
get lost easily, so IRC is only useful for general chat, not for a long detail.
Most likely at IRC you will be asked to add a new GitHub issue anyway.

***

## Still reading?

Wow, you are so cool ! You gonna be an expert guru soon.

Check out here for more wild stuff: https://github.com/wekan/wekan

There is:
- Info about translations, dev stuff, changelog, and huge amount of Wekan features.
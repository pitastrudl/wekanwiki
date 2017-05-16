> Offline is the new normal. Open Source and Free Software and Hardware is eating the world. Encrypted everywhere. Secure by design. Defence in depth. Legal. Allowed to do business. - [xet7](https://github.com/xet7) 2017-05, implementing GDPR

Case: Implementing [EU General Data Protection Regulation](https://en.wikipedia.org/wiki/General_Data_Protection_Regulation) with [Wekan](https://wekan.github.io), [Sandstorm](https://sandstorm.io) and [Qubes OS](https://www.qubes-os.org).

Disclaimer: All these opinions are my own, and I'm implementing this for myself. This has nothing to do with my previous, current or future employers. Everything is subject to change, as this is a process. I'm not a lawyer. I have not read the full legistlation yet, I'm just starting from the very first basic steps. GDPR has different requirements for different industries etc so this may not apply to you. I don't even know what all parts apply to me yet.

I [xet7](https://github.com/xet7) was this week at [Drupalcamp Nordics 2017](http://www.drupalcampnordics.com) and got more details about this regulation, so I started implementing this yesterday in the way I understand it currently, using technologies I'm most familiar with: [Wekan](https://wekan.github.io), [Sandstorm](https://sandstorm.io) and [Qubes OS](https://www.qubes-os.org). All hardware and software is subject to change if better alternatives are found.

This wiki is editable to all users that have GitHub account to add more details or questions what I have not considered yet.

## Deadlines

Date | Requirements | Sanctions if not ready
------------ | ------------- | ------------
2017-05-13 | Started documenting project with pen to paper in Finnish and English. This wiki page history is also used to show versions of process. | Unable to do business legally if not documented everything, including process of preparing to regulation
2017-05-31 | Need to find missing keys | Pay for expensive changing of locks
2017- | Find from home all harddrives, USB sticks, etc | Not known yet
2017- | Downloaded all data from Internet | Not known yet
2017- | Sorted and moved all data on offline computer to different Qubes OS AppVMs named by person | Not known yet
2017- | Found all required alternatives to propietary software from Qubes OS and Sandstorm | Not known yet
2017- | Converted all propietary file formats to free software file formats, like JSON etc. | Not known yet
2017- | Implemented exporting of all data to file download, and deleting of persons data in web interface | Not known yet
2018-04-25 | All data stored securely following GDPR | Unable to do business legally

## Security requirements

There is very high penalties for security breaches. If I have not considered some security aspect, please add it to this wiki page.

I need to know exactly where all my data physically is. It's not OK to spread it all over Internet in cloud services Google/AWS/Amazon/Dropbox etc. I need the abitily to absolutely have the proof and knowledge that when I delete one person's data, it's gone, totally, completely, from everywhere.

### Hardware: x64

##### Current

a) Current version 3.x of [Qubes OS](https://www.qubes-os.org), if hardware supports it. Laptop/Desktop hardware should be silent, otherwise it disturbs work. Qubes-certified laptops are nice, it has hardware switches to turn off wireless. Alternatively desktop PC that has not any wireless WLAN, Bluetooth etc device integrated.

b) If hardware does not support Qubes OS, I will install some of these:

* [Subgraph OS](https://subgraph.com/sgos/)
* [True OS/FreeNAS](https://www.trueos.org), see [FLOSS423](https://twit.tv/shows/floss-weekly/episodes/432)

##### Hardening

[Intel AMT Checker for Linux](https://github.com/mjg59/mei-amt-check) and it's [HN discussion](https://news.ycombinator.com/item?id=14335159).

For me it shows Intel AMT is present, AMT is unprovisioned, so I need to:
* Install English ISO of [Win7](https://www.microsoft.com/en-us/software-download/windows7) or [Win8.1](https://www.microsoft.com/en-us/software-download/windows8ISO) or [Win10](https://www.microsoft.com/en-us/software-download/windows10ISO) to USB stick
* or Install Finnish ISO of [Win7](https://www.microsoft.com/fi-fi/software-download/windows7) or [Win8.1](https://www.microsoft.com/fi-fi/software-download/windows8ISO) or [Win10](https://www.microsoft.com/fi-fi/software-download/windows10ISO) to USB stick
* or convert [evaluation VM of Windows](https://developer.microsoft.com/en-us/microsoft-edge/tools/vms/) to RAW image using [instructions](https://www.qubes-os.org/doc/hvm/#converting-virtualbox-vm-to-hvm) that [I contributed to Qubes documentation](https://github.com/QubesOS/qubes-doc/pull/210), and use [dd command](https://wiki.archlinux.org/index.php/disk_cloning) to write it to USB stick
* Install patch from [HP website](http://www8.hp.com/us/en/intelmanageabilityissue.html#Commercial_Notebooks)
* Check all other hardware and disable AMT where possible.

##### Future

[Rowhammer](https://en.wikipedia.org/wiki/Row_hammer) protection, see [LWN article](https://lwn.net/Articles/704920/), [SN576](https://twit.tv/shows/security-now/episodes/576), [SN583](https://twit.tv/shows/security-now/episodes/583). Without it, just browsing Internet with Javascript enabled makes it possible to [exploit using Javascript on webpage](https://github.com/IAIK/rowhammerjs) through all layers of virtualization protections and install malware to firmware like UEFI/Graphics card card/harddrive/SD card etc, so it is not possible get clean computer by just securely erasing harddrive. Alternatively malware can then brick computer, making it unable to boot, as has already happened to IoT devices connected to Internet. Currently Google Cloud kills immediately VMs that try to use Rowhammer serverside code. This is needed for all devices in use.

[Qubes 4.x certified hardware](https://www.qubes-os.org/news/2016/07/21/new-hw-certification-for-q4/) when it becomes available.

### Hardware: ARM

Raspberry Pi  or similar ARM device without built-in wireless, so it can be used offline. Fanless preferred to keep it completely silent. I don't know is there any writeable firmware in RasPi at all, is SD card only writeable storage. AFAIK RasPi hardware does not have any hardware virtualization or Rowhammer protection features.

### Software

I need to keep multiple encrypted offline backups. Otherwise some ransomware will just encrypt all my files and demand that I give money, bitcoins, etc to get my files back. Malware exists for all platforms, including Linux. 

Media type:

a) Write-only, like DVD-R

b) Is there storage media that has physical hardware switch that makes media read-only?

I need to have source code for every software I use, and tested working way to compile it from source.

I need to test [Qubes compromise recovery](https://www.qubes-os.org/news/2017/04/26/qubes-compromise-recovery/).

[Porting software to Sandstorm](https://docs.sandstorm.io/en/latest/developing/raw-packaging-guide/). Not all ports are up-to-date yet, but they are anyway protected by Sandstorm [high-end security features](https://docs.sandstorm.io/en/latest/using/security-practices/), [security audit with fixes already implemented](https://sandstorm.io/news/2017-03-02-security-review) and also [authentication and clustering](https://sandstorm.io/news/2017-02-06-sandstorm-returning-to-community-roots).

[Web developer security checklist](https://simplesecurity.sensedeep.com/web-developer-security-checklist-f2e4f43c9c56) and it's [HN discussion](https://news.ycombinator.com/item?id=14346652)

Software | Propietary Desktop | Propietary Web | FLOSS Desktop | FLOSS Web
------------ | ------------- | ------------ | ------------ | ------------
Word processing | MS Word | Google Docs | [LibreOffice](https://www.libreoffice.org) Writer | [Sandstorm](https://sandstorm.io) / [Etherpad](http://etherpad.org)
Spreadsheet | MS Excel | Google Sheets | [LibreOffice](https://www.libreoffice.org) Calc | [Sandstorm](https://sandstorm.io) / [EtherCalc](https://ethercalc.net)
Presentations | MS PowerPoint | Google Slides | [LibreOffice](https://www.libreoffice.org) Impress | [Sandstorm](https://sandstorm.io) / Hacker Slides
RAD Database | MS Access | - | [LibreOffice](https://www.libreoffice.org) Base | [nuBuilderPro](https://www.nubuilder.net)
Basic Programming | MS Visual Basic | - | [Gambas](http://gambas.sourceforge.net) see [FLOSS353](https://twit.tv/shows/floss-weekly/episodes/353) | [Gambas](http://gambas.sourceforge.net)
Pascal Programming | Delphi | - | [Lazarus](https://www.lazarus-ide.org), [Lazarus for Amiga, AROS, MorphOS](https://blog.alb42.de/virtual-lazarus), [Ultibo IoT OS for Raspberry Pi](https://ultibo.org) | -
Diagramming | MS Visio | - | [LibreOffice](https://www.libreoffice.org) Draw, [Inkscape](https://inkscape.org) has also JPG to SVG etc, Dia | [Sandstorm](https://sandstorm.io) / draw.io
Password manager | LastPass | LastPass | keepass2 | [Sandstorm](https://sandstorm.io) / Sandpass
Hardware info | CPU-Z | - | [I-Nex](http://i-nex.linux.pl) | -
Kanban | - | Trello | - | [Sandstorm](https://sandstorm.io) / [Wekan](https://wekan.github.io) see [author's talk](https://www.youtube.com/watch?v=N3iMLwCNOro) - current maintainer is [xet7](https://github.com/xet7)
Chat | Skype | Slack | Pidgin, HexChat | [Sandstorm](https://sandstorm.io) / [Rocket.Chat](https://rocket.chat)
Video conferencing | Skype | Google Hangouts | - |  [Sandstorm](https://sandstorm.io) / [Rocket.Chat](https://rocket.chat)
Screen recorder | - | - | [Simplescreenrecorder](http://www.maartenbaert.be/simplescreenrecorder/), [Green recorder](http://www.omgubuntu.co.uk/2017/02/record-your-screen-on-ubuntu-this-app), [VokoScreen](https://github.com/vkohaupt/vokoscreen), [Byzanz](https://wiki.ubuntu.com/CreatingScreencasts), [VLC](http://www.videolan.org), [OBS Studio](https://obsproject.com/), [Screenstudio](https://github.com/patrickballeux/screenstudio) | -
Website/Blog | - | Google Sites/Blogger.com | - | [Sandstorm](https://sandstorm.io) / [Ghost](https://ghost.org), [WordPress](https://wordpress.org), [Hugo](https://gohugo.io), Hakyll CMS
Robot simulation | - | - | - | [Roboschool](https://blog.openai.com/roboschool) and [HN discussion](https://news.ycombinator.com/item?id=14346227)
SIEM | - | - | - | [AlienVault Ossim](https://www.alienvault.com/products/ossim)
Endpoint Visibility | - | - | - | [osquery](https://osquery.io)
Immediate changed file restore, replication and HA | - | - | - | [mgmt](https://github.com/purpleidea/mgmt)
Compliance | - | - | - | [SIMP](https://simp-project.com) see [FLOSS426](https://twit.tv/shows/floss-weekly/episodes/426), [Saltstack](https://saltstack.com/infrastructure-compliance) see [videos](https://www.youtube.com/user/SaltStack/videos)
Encrypted port knocking | - | - | - | [fwknop](https://www.cipherdyne.org/fwknop/) see [FLOSS352](https://twit.tv/shows/floss-weekly/episodes/352)
Restore database back in time | - | - | - | [pgBackRest](http://www.pgbackrest.org) see [FLOSS429](https://twit.tv/shows/floss-weekly/episodes/429)
Remote Desktop using webbrowser | - | - | - | [Guacamole](https://guacamole.incubator.apache.org)
Docker Security Scan | - | - | - | [Anchore](https://github.com/anchore/anchore) see [FLOSS427](https://twit.tv/shows/floss-weekly/episodes/427)
> [Offline](https://en.wikipedia.org/wiki/Online_and_offline) is the [new normal](https://en.wiktionary.org/wiki/new_normal). [Open Source](https://en.wikipedia.org/wiki/Open-source_software) and [Free Software](https://en.wikipedia.org/wiki/Free_software) and [Open-Source Hardware](https://en.wikipedia.org/wiki/Open-source_hardware) is [eating the world](https://en.wikipedia.org/wiki/Marc_Andreessen#cite_note-WSJ_Software_Eating-35) in the [war on general-purpose computing](https://boingboing.net/2012/01/10/lockdown.html) ([HN](https://news.ycombinator.com/item?id=14335261)). [Encrypted](https://en.wikipedia.org/wiki/Encryption) everywhere. [Secure by design](https://en.wikipedia.org/wiki/Secure_by_design). [Defence in depth](https://en.wikipedia.org/wiki/Defense_in_depth_(computing)). [Legal](https://en.wikipedia.org/wiki/Law). Allowed to do [business](https://en.wikipedia.org/wiki/Business). - [xet7](https://github.com/xet7) 2017-05, implementing GDPR

Case: Implementing [EU General Data Protection Regulation](https://en.wikipedia.org/wiki/General_Data_Protection_Regulation) with [Wekan](https://wekan.github.io), [Sandstorm](https://sandstorm.io) and [Qubes OS](https://www.qubes-os.org).

Disclaimer: All these [opinions](https://en.wikipedia.org/wiki/Opinion) are my own, and I'm implementing this for myself. This has nothing to do with my previous, current or future [employers](https://en.wikipedia.org/wiki/Employment#Employees_and_employers). Everything is subject to change, as this is a [process](https://en.wikipedia.org/wiki/Software_development_process). I'm not a [lawyer](https://en.wikipedia.org/wiki/Lawyer). I have not read the full [regulation](https://en.wikipedia.org/wiki/Regulation) yet, I'm just starting from the very first basic steps. GDPR has different [requirements](https://en.wikipedia.org/wiki/Requirement) for different [industries](https://en.wikipedia.org/wiki/Industrial_Revolution) etc so this may not apply to you. I don't even know what all parts apply to me yet.

I [xet7](https://github.com/xet7) was this week at [Drupalcamp Nordics 2017](http://www.drupalcampnordics.com) and got more details about this regulation, so I started implementing this yesterday in the way I understand it currently, using [technologies](https://en.wikipedia.org/wiki/Technology) I'm most familiar with: [Wekan](https://wekan.github.io), [Sandstorm](https://sandstorm.io) and [Qubes OS](https://www.qubes-os.org). All hardware and software is subject to change if better alternatives are found.

This wiki is editable to all users that have [GitHub](https://en.wikipedia.org/wiki/GitHub) [account](https://en.wikipedia.org/wiki/User_(computing)#User_account) to add more [details](https://en.wikipedia.org/wiki/Security_detail) or [questions](https://en.wikipedia.org/wiki/Question) what I have not [considered](https://en.wikipedia.org/wiki/Consideration) yet.

## Deadlines

Date | Requirements | Sanctions if not ready
------------ | ------------- | ------------
2017-05-13 | Started documenting project. This wiki page history is also used to show versions of process. | Unable to do business legally if not documented everything, including process of preparing to regulation
2017-07-31 | Need to find missing keys | Pay for expensive changing of locks
2017- | Find from home all harddrives, USB sticks, etc | Not known yet
2017- | Downloaded all [data]([data](https://en.wikipedia.org/wiki/Data)) from Internet | Not known yet
2017- | Sorted and moved all [data]([data](https://en.wikipedia.org/wiki/Data)) on [offline](https://en.wikipedia.org/wiki/Online_and_offline) [computer](https://en.wikipedia.org/wiki/Computer) to different [Qubes OS](https://www.qubes-os.org) [AppVMs](https://www.qubes-os.org/doc/software-update-vm/) named by person | Not known yet
2017- | Found all required alternatives to propietary software from [Qubes OS](https://www.qubes-os.org) and Sandstorm | Not known yet
2017- | Converted all [propietary file formats](https://en.wikipedia.org/wiki/Proprietary_format) to [free software](https://en.wikipedia.org/wiki/Free_software) [file formats](https://en.wikipedia.org/wiki/File_format), like [JSON](https://en.wikipedia.org/wiki/JSON) etc. | Not known yet
2017- | Implemented [exporting](https://en.wikipedia.org/wiki/Import_and_export_of_data) of all [data](https://en.wikipedia.org/wiki/Data) to [file](https://en.wikipedia.org/wiki/Computer_file) [download](https://en.wikipedia.org/wiki/Download), and [deleting](https://en.wikipedia.org/wiki/File_deletion) of [persons](https://en.wikipedia.org/wiki/Person) [data](https://en.wikipedia.org/wiki/Data) in [web](https://en.wikipedia.org/wiki/World_Wide_Web) [interface](https://en.wikipedia.org/wiki/User_interface) | Not known yet
2018-04-25 | All [data](https://en.wikipedia.org/wiki/Data) [stored](https://en.wikipedia.org/wiki/Data_storage_device) [securely](https://en.wikipedia.org/wiki/Application_security) following GDPR | Unable to do business legally

## Security requirements

There is very high [sanctions](https://en.wikipedia.org/wiki/Sanctions_(law)) for [data breaches](https://en.wikipedia.org/wiki/Data_breach). If I have not [considered]([considered](https://en.wikipedia.org/wiki/Consideration)) some [security](https://en.wikipedia.org/wiki/Application_security) [aspect](https://en.wikipedia.org/wiki/Aspect_(computer_programming)), please add it to this [wiki](https://en.wikipedia.org/wiki/Wiki) [page](https://en.wikipedia.org/wiki/Web_page).

I need to know exactly where all my [data]([data](https://en.wikipedia.org/wiki/Data)) physically is. It's not OK to spread it all over Internet in cloud services Google/AWS/Amazon/Dropbox etc. I need the abitily to absolutely have the proof and knowledge that when I delete one person's [data]([data](https://en.wikipedia.org/wiki/Data)), it's gone, totally, completely, from everywhere.

### Hardware: [x64](https://en.wikipedia.org/wiki/X86-64)

##### Current

a) Current version 3.x of [Qubes OS](https://www.qubes-os.org), if hardware supports it. Laptop/Desktop hardware should be silent, otherwise it disturbs work. [Qubes-certified laptops](https://www.qubes-os.org/doc/certified-laptops/) are nice, it has hardware switches to turn off wireless. Alternatively desktop PC that has not any wireless WLAN, Bluetooth etc device integrated.

b) If hardware does not support [Qubes OS](https://www.qubes-os.org), I will install some of these:

* [Subgraph OS](https://subgraph.com/sgos/)
* [True OS/FreeNAS](https://www.trueos.org), see [FLOSS423](https://twit.tv/shows/floss-weekly/episodes/432)

##### Hardening

[Intel AMT Checker for Linux](https://github.com/mjg59/mei-amt-check) and it's [HN discussion](https://news.ycombinator.com/item?id=14335159).

For me it shows Intel AMT is present, AMT is unprovisioned, so I need to:
* Install English ISO of [Win7](https://www.microsoft.com/en-us/software-download/windows7) or [Win8.1](https://www.microsoft.com/en-us/software-download/windows8ISO) or [Win10](https://www.microsoft.com/en-us/software-download/windows10ISO) to [USB stick](https://en.wikipedia.org/wiki/USB_flash_drive)
* or Install Finnish ISO of [Win7](https://www.microsoft.com/fi-fi/software-download/windows7) or [Win8.1](https://www.microsoft.com/fi-fi/software-download/windows8ISO) or [Win10](https://www.microsoft.com/fi-fi/software-download/windows10ISO) to USB stick
* or convert [evaluation VM of Windows](https://developer.microsoft.com/en-us/microsoft-edge/tools/vms/) to RAW image using [instructions](https://www.qubes-os.org/doc/hvm/#converting-virtualbox-vm-to-hvm) that [I contributed to Qubes documentation](https://github.com/QubesOS/qubes-doc/pull/210), and use [dd command](https://wiki.archlinux.org/index.php/disk_cloning) to write it to USB stick
* Install patch from [HP website](http://www8.hp.com/us/en/intelmanageabilityissue.html#Commercial_Notebooks)
* Check all other hardware and disable AMT where possible.

##### Future

[Rowhammer](https://en.wikipedia.org/wiki/Row_hammer) protection, see [LWN article](https://lwn.net/Articles/704920/), [SN576](https://twit.tv/shows/security-now/episodes/576), [SN583](https://twit.tv/shows/security-now/episodes/583). [HN discussion](https://news.ycombinator.com/item?id=12821019) that has [comment with links to paper and repo of software protections as linux kernel module](https://news.ycombinator.com/item?id=12822490) (I have not tested it yet) and [Qubes Users discussion](https://groups.google.com/forum/#!msg/qubes-users/wbot4wd4Rcw/gxjKyhB1AAAJ). Without it, just browsing Internet with Javascript enabled makes it possible to [exploit using Javascript on webpage](https://github.com/IAIK/rowhammerjs) through all layers of virtualization protections and install malware to firmware like UEFI/Graphics card card/harddrive/SD card etc, so it is not possible get clean computer by just securely erasing harddrive. Alternatively malware can then brick computer, making it unable to boot, as has already happened to IoT devices connected to Internet. Currently Google Cloud kills immediately VMs that try to use Rowhammer serverside code. This is needed for all devices in use.



[Qubes 4.x certified hardware](https://www.qubes-os.org/news/2016/07/21/new-hw-certification-for-q4/) when it becomes available.

### Hardware: [ARM](https://en.wikipedia.org/wiki/ARM_architecture)

[Raspberry Pi](https://en.wikipedia.org/wiki/Raspberry_Pi)  or similar ARM device without built-in wireless, so it can be used offline. [Fanless](https://en.wikipedia.org/wiki/Computer_fan#Alternatives) preferred to keep it completely [silent](https://en.wikipedia.org/wiki/Silence_(disambiguation)). I don't know is there any writeable [firmware](https://en.wikipedia.org/wiki/Firmware) in RasPi at all, is [SD card](https://en.wikipedia.org/wiki/Secure_Digital) only writeable storage. AFAIK RasPi hardware does not have any [hardware virtualization](https://en.wikipedia.org/wiki/Hardware_virtualization) or [Rowhammer](https://en.wikipedia.org/wiki/Row_hammer) protection features.

### Software

I need to keep multiple encrypted offline [backups](https://en.wikipedia.org/wiki/Backup). Otherwise some [ransomware](https://en.wikipedia.org/wiki/Ransomware) will just encrypt all my files and demand that I give [money](https://en.wikipedia.org/wiki/Money), [bitcoins](https://en.wikipedia.org/wiki/Bitcoin), etc to get my files back. [Malware](https://en.wikipedia.org/wiki/Malware) exists for most [Operating systems](https://en.wikipedia.org/wiki/Operating_system), including Linux. 

Media type:

a) Write-only, like [DVD-R](https://en.wikipedia.org/wiki/DVD)

b) Is there [storage media](https://en.wikipedia.org/wiki/Data_storage_device) that has physical [hardware](https://en.wikipedia.org/wiki/Hardware) [switch](https://en.wikipedia.org/wiki/Switch) that makes media [read-only](https://en.wikipedia.org/wiki/Read-only) ?

I need to have [source code](https://en.wikipedia.org/wiki/Source_code) for every [software](https://en.wikipedia.org/wiki/Software) I use, and tested working way to [compile](https://en.wikipedia.org/wiki/Compiler) it from source.

I need to test [Qubes compromise recovery](https://www.qubes-os.org/news/2017/04/26/qubes-compromise-recovery/).

[Porting software to Sandstorm](https://docs.sandstorm.io/en/latest/developing/raw-packaging-guide/). Not all ports are up-to-date yet, but they are anyway protected by Sandstorm [high-end security features](https://docs.sandstorm.io/en/latest/using/security-practices/), [security audit with fixes already implemented](https://sandstorm.io/news/2017-03-02-security-review) and also [authentication and clustering](https://sandstorm.io/news/2017-02-06-sandstorm-returning-to-community-roots).

[Web developer security checklist](https://simplesecurity.sensedeep.com/web-developer-security-checklist-f2e4f43c9c56) and it's [HN discussion](https://news.ycombinator.com/item?id=14346652)

Software | Propietary Desktop | Propietary Web | FLOSS Desktop | FLOSS Web
------------ | ------------- | ------------ | ------------ | ------------
[Word processing](https://en.wikipedia.org/wiki/Word_processor) | [MS Word](https://en.wikipedia.org/wiki/Microsoft_Word) | [Google Docs](https://en.wikipedia.org/wiki/Google_Docs,_Sheets_and_Slides) | [LibreOffice](https://www.libreoffice.org) Writer | [Sandstorm](https://sandstorm.io) / [Etherpad](http://etherpad.org)
[Spreadsheet](https://en.wikipedia.org/wiki/Spreadsheet) | [MS Excel](https://en.wikipedia.org/wiki/Microsoft_Excel) | [Google Sheets](https://en.wikipedia.org/wiki/Google_Docs,_Sheets_and_Slides) | [LibreOffice](https://www.libreoffice.org) Calc | [Sandstorm](https://sandstorm.io) / [EtherCalc](https://ethercalc.net)
[Presentations](https://en.wikipedia.org/wiki/Presentation_program) | [MS PowerPoint](https://en.wikipedia.org/wiki/Microsoft_PowerPoint) | [Google Slides](https://en.wikipedia.org/wiki/Google_Docs,_Sheets_and_Slides) | [LibreOffice](https://www.libreoffice.org) Impress | [Sandstorm](https://sandstorm.io) / Hacker Slides
[RAD](https://en.wikipedia.org/wiki/Rapid_application_development) [Database](https://en.wikipedia.org/wiki/Database) | [MS Access](https://en.wikipedia.org/wiki/Microsoft_Access) | - | [LibreOffice](https://www.libreoffice.org) Base | [nuBuilderPro](https://www.nubuilder.net)
[Basic Programming](https://en.wikipedia.org/wiki/BASIC) | [MS Visual Basic](https://en.wikipedia.org/wiki/Visual_Basic) | - | [Gambas](http://gambas.sourceforge.net) see [FLOSS353](https://twit.tv/shows/floss-weekly/episodes/353) | [Gambas](http://gambas.sourceforge.net)
[Pascal Programming](https://en.wikipedia.org/wiki/Pascal_(programming_language)) | [Delphi](https://en.wikipedia.org/wiki/Delphi_(programming_language)) | - | [Lazarus](https://www.lazarus-ide.org), [Lazarus for Amiga, AROS, MorphOS](https://blog.alb42.de/virtual-lazarus), [Ultibo IoT OS for Raspberry Pi](https://ultibo.org) | -
[Cross-platform programming](https://en.wikipedia.org/wiki/Cross-platform) | - | - | [Haxe](https://haxe.org) with [HaxeUI](http://haxeui.org) | [Haxe](https://haxe.org) with [HaxeUI](http://haxeui.org)
[Diagramming](https://en.wikipedia.org/wiki/Diagram) and [Vector graphics editor](https://en.wikipedia.org/wiki/Vector_graphics_editor) | [MS Visio](https://en.wikipedia.org/wiki/Microsoft_Visio) | - | [LibreOffice](https://www.libreoffice.org) Draw, [Inkscape](https://inkscape.org) has also [JPG](https://en.wikipedia.org/wiki/JPEG) to [SVG](https://en.wikipedia.org/wiki/Scalable_Vector_Graphics) etc, Dia | [Sandstorm](https://sandstorm.io) / draw.io
[Password manager](https://en.wikipedia.org/wiki/Password_manager) | [LastPass](https://en.wikipedia.org/wiki/LastPass) | [LastPass](https://en.wikipedia.org/wiki/LastPass) | [KeePass](https://en.wikipedia.org/wiki/KeePass) | [Sandstorm](https://sandstorm.io) / Sandpass
[Hardware](https://en.wikipedia.org/wiki/Computer_hardware) info | [CPU-Z](https://en.wikipedia.org/wiki/CPU-Z) | - | [I-Nex](http://i-nex.linux.pl) | -
[Kanban](https://en.wikipedia.org/wiki/Kanban_(development)) | - | [Trello](https://en.wikipedia.org/wiki/Trello) | - | [Sandstorm](https://sandstorm.io) / [Wekan](https://wekan.github.io) see [author's talk](https://www.youtube.com/watch?v=N3iMLwCNOro) - current maintainer is [xet7](https://github.com/xet7)
[Chat](https://en.wikipedia.org/wiki/Online_chat) | [Skype](https://en.wikipedia.org/wiki/Skype) | [Slack](https://en.wikipedia.org/wiki/Slack_(software)) | [Pidgin](https://en.wikipedia.org/wiki/Pidgin_(software)), [HexChat](https://hexchat.github.io) | [Sandstorm](https://sandstorm.io) / [SandChat](https://apps.sandstorm.io/app/q95sez0acjwq7c1emxyxz38947sr7sgc1gn9yju93nqccz83fzyh) and [Rocket.Chat](https://rocket.chat)
[Video conferencing](https://en.wikipedia.org/wiki/Comparison_of_web_conferencing_software) | [Skype](https://en.wikipedia.org/wiki/Skype) | [Google Hangouts](https://en.wikipedia.org/wiki/Google_Hangouts) | [Friend](https://friendup.cloud), [Riot](https://about.riot.im) | [Riot](https://about.riot.im), [Sandstorm](https://sandstorm.io) / [Rocket.Chat](https://rocket.chat)
[Screen recorder](https://en.wikipedia.org/wiki/Screencast) | - | - | [Simplescreenrecorder](http://www.maartenbaert.be/simplescreenrecorder/), [Green recorder](http://www.omgubuntu.co.uk/2017/02/record-your-screen-on-ubuntu-this-app), [VokoScreen](https://github.com/vkohaupt/vokoscreen), [Byzanz](https://wiki.ubuntu.com/CreatingScreencasts), [VLC](http://www.videolan.org), [OBS Studio](https://obsproject.com/), [Screenstudio](https://github.com/patrickballeux/screenstudio) | -
[Website](https://en.wikipedia.org/wiki/Website) or [Blog](https://en.wikipedia.org/wiki/Blog) | - | [Google Sites](https://en.wikipedia.org/wiki/Google_Sites), [Blogger](https://en.wikipedia.org/wiki/Blogger_(service)) | - | [Sandstorm](https://sandstorm.io) / [Ghost](https://ghost.org), [WordPress](https://wordpress.org), [Hugo](https://gohugo.io), Hakyll CMS
[Robot](https://en.wikipedia.org/wiki/Robot) [simulation](https://en.wikipedia.org/wiki/Simulation) | - | - | - | [Roboschool](https://blog.openai.com/roboschool) and [HN discussion](https://news.ycombinator.com/item?id=14346227)
[SIEM](https://en.wikipedia.org/wiki/Security_information_and_event_management) | - | - | - | [AlienVault Ossim](https://www.alienvault.com/products/ossim)
[Endpoint Visibility](https://en.wikipedia.org/wiki/Endpoint_security) | - | - | - | [osquery](https://osquery.io) see [LWN](https://lwn.net/Articles/723200/) and [doorman](https://github.com/mwielgoszewski/doorman)
Immediate changed file [restore](https://en.wikipedia.org/wiki/Backup), [replication](https://en.wikipedia.org/wiki/Replication_(computing)) and [HA](https://en.wikipedia.org/wiki/High_availability) | - | - | - | [mgmt](https://github.com/purpleidea/mgmt)
[Compliance](https://en.wikipedia.org/wiki/Compliance) to [Cyber Security Standards](https://en.wikipedia.org/wiki/Cyber_security_standards) | - | - | - | [SIMP](https://simp-project.com) see [FLOSS426](https://twit.tv/shows/floss-weekly/episodes/426), [HubbleStack](https://hubblestack.io) = [Saltstack](https://saltstack.com/infrastructure-compliance) see [videos](https://www.youtube.com/user/SaltStack/videos) + [osquery](https://osquery.io)
Encrypted [port knocking](https://en.wikipedia.org/wiki/Port_knocking) | - | - | - | [fwknop](https://www.cipherdyne.org/fwknop/) see [FLOSS352](https://twit.tv/shows/floss-weekly/episodes/352)
[Restore](https://en.wikipedia.org/wiki/Backup) [database](https://en.wikipedia.org/wiki/Database) [back in time](https://en.wikipedia.org/wiki/Time_travel) | - | - | - | [pgBackRest](http://www.pgbackrest.org) see [FLOSS429](https://twit.tv/shows/floss-weekly/episodes/429)
[Remote Desktop](https://en.wikipedia.org/wiki/Remote_desktop_software) | TeamViewer | TeamViewer | [x2go](https://wiki.x2go.org) | [Guacamole](https://guacamole.incubator.apache.org)
[Docker](https://en.wikipedia.org/wiki/Docker_(software)) [Security Scan](https://en.wikipedia.org/wiki/Application_security) | - | - | - | [Anchore](https://github.com/anchore/anchore) see [FLOSS427](https://twit.tv/shows/floss-weekly/episodes/427)
Augmented Reality | - | - | - | [Web](https://github.com/jeromeetienne/AR.js)
Case: Implementing [EU General Data Protection Regulation](https://en.wikipedia.org/wiki/General_Data_Protection_Regulation) with Wekan and Sandstorm

I (xet7) was this week at [Drupalcamp Nordics 2017](http://www.drupalcampnordics.com) and got more details about this regulation, so I started implementing this yesterday in the way I understand it currently, using technologies I'm most familiar with: Wekan, Sandstorm and Qubes OS.

## Deadlines

Date | Requirements | Sanctions if not ready
------------ | ------------- | ------------
2017-05-13 | Started documenting project with pen to paper in Finnish and English | Unable to do business legally if not documented everything, including process of preparing to regulation
2017-05-31 | Need to find missing keys | Pay for expensive changing of locks
2017- | Found from home all harddrives, USB sticks, etc | Not known yet
2017- | Downloaded all data from Internet | Not known yet
2017- | Sorted and moved all data on offline computer to different Qubes OS AppVMs named by person | Not known yet
2017- | Found all required alternatives to propietary software from Qubes OS and Sandstorm | Not known yet
2017- | Converted all propietary file formats to free software file formats, like JSON etc. | Not known yet
2017- | Implemented exporting of all data to file download, and deleting of persons data in web interface | Not known yet
2018-04-25 | All data stored securely following GDPR | Unable to do business legally

## Security requirements

There is very high penalties for security breaches. If I have not considered some security aspect, please add it to this wiki page.

### Hardware

[Rowhammer](https://en.wikipedia.org/wiki/Row_hammer) protection, see [LWN article](https://lwn.net/Articles/704920/), [SN576](https://twit.tv/shows/security-now/episodes/576), [SN583](https://twit.tv/shows/security-now/episodes/583). Without it, just browsing Internet with Javascript enabled makes it possible to [exploit using Javascript on webpage](https://github.com/IAIK/rowhammerjs) through all layers of virtualization protections and install malware to firmware like UEFI/Graphics card card/harddrive/SD card etc, so it is not possible get clean computer by just securely erasing harddrive. Currently Google Cloud kills immediately VMs that try to use Rowhammer serverside code. This is needed for all devices in use.

[Qubes 4.x certified hardware](https://www.qubes-os.org/news/2016/07/21/new-hw-certification-for-q4/) when it becomes available.

It's not wise to spend money on broken insecure hardware before these come available. Just keep using your current hardware and keep multiple encrypted offline backups, preferably on write-only media. Otherwise some ransomware will just encrypt all your files and demand that you give money, bitcoins, etc to get your files back.
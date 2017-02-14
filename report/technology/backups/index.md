---
category: technology
created: 2016.11.17:0400
title: The Krueger Report - Backups
type: page
updated: 2016.11.17:0400
---

# Backups

It has been nearly 15 years since I last experienced a catastrophic data failure on any of my computers. When this happened, I lost most of the files that were important to me. I did not have any real backup plan in place, and managed to recover just a few that happened to be saved on other machines.

Ever since then, I have had at least a single backup of all of my data. While one backup is better than none, it still left me open to complete data loss. The couple of times that my primary hard drive failed, I was left with a single working drive. My data was intact, but I was one drive failure away from complete loss.

With the advent of [Dropbox](https://www.dropbox.com), [MobileMe](https://en.wikipedia.org/wiki/MobileMe), and [iCloud](https://www.icloud.com), I began to keep the most important of my files backed up online. Should both of my hard drives die, I would have the essential files: Pictures, school papers, other writings. But I would still lose all of my music and videos. At the time these services came about, online backup of hundreds of gigabytes was prohibitively expensive.

In recent years, that has changed. Tons of online services focused on data backup have come into existence. These services have reached a point where they are now cheap enough to be viable, even when the amount of data being backed up exceeds 1 terabyte.

### Objectives

Before exploring all of the options for a backup plan, I wrote down the following objectives that the plan must fulfill.

1. Data is encrypted.
2. Complete backups daily.
3. Data backed up to 3 separate locations.
4. At least one off-site backup.

### Arq

I first read about [Arq](https://www.arqbackup.com) a few years back. It ticked a lot of the right boxes for me, but I did not have a chance to fully explore it until this year.

Arq is an application for both macOS and Windows that acts as the client software for backup data. It encrypts the data with your own provided key, and then connects to your backup service of choice to upload the data.

The security of Arq was what first brought it to my attention. Before Arq uploads your data to a server, it is encrypted. If your service account is compromised or the data intercepted en route to the service, the data is encrypted and not viewable. To further protect the data, the format Arq uses is open, and third-party tools have been created that allow extraction of the data, with the proper encryption key.

Since Arq is just a front-end for the backup, it requires a separate cloud service to backup to. Arq lets you backup to all of the following services: [Amazon Cloud Drive](https://www.amazon.com/clouddrive/home/), [AWS](https://aws.amazon.com), [Dropbox](https://www.dropbox.com), [Google Cloud Storage](https://cloud.google.com/storage/), [Google Drive](https://www.google.com/drive/), [Microsoft OneDrive](https://onedrive.live.com), and if none of these solutions are to your liking, it can backup to a personal [SFTP](https://en.wikipedia.org/wiki/Secure_file_transfer_program) server. Having this level of flexibility is useful, as I can switch between services if needed without having to also replace Arq itself.

The above cloud services have varying ways to charge you. Some charge a flat fee per month, some charge by the amount of storage, and some have additional costs for restoring the data. To account for high storage needs, I took the pricing of all of the services and calculated out how much it would cost per month to store 1 terabyte of data. All of the costs are in US Dollars.

- **Amazon Cloud Drive**: $5 for storage, free to restore
- **AWS Glacier**: $4.09 for storage, $92.07 to restore
- **AWS S3**: $23.55 for storage, $92.07 to restore
- **AWS S3 Infrequent Access**: $12.80 for storage, $92.07 to restore
- **Dropbox**: $8.25, free to restore
- **Google Coldline Storage**: $7.17 for storage, $122.88 to restore
- **Google Nearline Storage**: $10.24 for storage, $122.88 to restore
- **Google Drive**: $9.99 for storage, free to restore
- **Microsoft OneDrive**: $6.99 for storage, free to restore

Monthly storage cost is important, but if restoring the data is prohibitively expensive, then that particular option is out. In the case of complete data loss, all of the AWS options and Google Storage options are too expensive. It would cost around one hundred dollars per terabyte to restore, which can add up quickly given my backup sizes.

Dropbox, Google Drive, and Microsoft OneDrive are all priced nicely, but their cost comes in strict tiers. For example, Google Drive charges $9.99/month for 1 terabyte, but if you need to store more, you must pay $99.99/month for 10 terabytes. There is no middle-ground between 1 terabyte and 10 terabytes. Dropbox and OneDrive only offer tiers up to 1 terabyte, and not larger. Without more precise tiers, these services are either too expensive or not adaptable enough for my needs.

This leaves only Amazon Cloud Drive. $5 not only gets you unlimited storage per month, but is also one of the few to not charge anything for restoring the backup.

Given these conditions, I went with Amazon Cloud Drive for my current backup solution.

### Current Solution

My data is split into two sets: irreplaceable personal data, and multimedia.

Irreplaceable personal data exists in all forms of backup. The main copies are stored in iCloud Drive, which automatically syncs all of the data between my Mac Mini and MacBook Air, as well as the intermediary servers that Apple runs. My MacBook Air is typically powered down, so if a catastrophe struck where the data on both the Mac Mini and iCloud servers was damaged, I could power up the MacBook Air, and as long as it did not connect to WiFi, all of the data would still be present.

In addition to the iCloud syncing, this data is backed up to Amazon Cloud Drive by way of Arq. Nightly backups are conducted. Daily snapshots are kept for the previous 7 days, and weekly snapshots going back for 60 days.

For my multimedia data, I use the same solution as above, but minus the iCloud syncing and snapshots. Arq still backs up the data to Amazon Cloud Drive, but just one single snapshot is kept. Since this data does not change once it is created, all I need to do is keep it stored.

Finally, all of the above data is kept in a single external hard drive, backed up twice a month using rsync and stored offsite. In the event of complete data loss on both of my computers, this would be my first recourse in data recover. Cloud storage would be in case this backup is not available.

This puts the locations for my data as follows. Irreplaceable personal data is backed up to my MacBook Air, iCloud servers, Amazon Cloud Drive, and offsite external hard drive. This is 4 total locations, with 3 offsite. Multimedia data is backed up to iCloud Drive, Amazon Cloud Drive, and the offsite external hard drive. This is a total of 3 locations, all offsite.

With all of these backup plans in place, my data is in enough places where if all of my backups failed at once, it would likely be due to complete societal and technological collapse, and I would have much larger problems than caring about backups of pictures and music.

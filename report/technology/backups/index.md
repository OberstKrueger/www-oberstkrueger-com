---
category: technology
created: 2016.11.17:0400
title: The Krueger Report - Backups
type: page
updated: 2017.08.06:1945
---

# Backups

It has been over 15 years since I last experienced a catastrophic data failure on any of my computers. When this happened, I lost most of the files that were important to me. I did not have any real [backup](https://en.wikipedia.org/wiki/Backup) plan in place, and managed to recover just a few that happened to be saved on other machines.

Ever since then, I have had at least a single backup of all of my data. While one backup is better than none, it still left me open to complete data loss. The couple of times that my primary hard drive failed, I was left with a single working copy of my data. While the data was intact, I was one drive failure away from complete loss.

With the advent of [Dropbox](https://www.dropbox.com), [MobileMe](https://en.wikipedia.org/wiki/MobileMe), and [iCloud](https://www.icloud.com), I began to keep the most important of my files backed up online. Should all of computer storage suffer irreparable damage, I would have the essential files: pictures, school papers, other writings, etc. But I would still lose all of my music and videos. At the time these services came about, online backup of hundreds of gigabytes was not financially possible.

In recent years, that has changed. Tons of online services focused on data backup have come into existence. These services have reached a point where they are now cheap enough to be viable, even when the amount of data being backed up exceeds 1 terabyte.

### Objectives

Before exploring all of the options for a backup plan, I wrote down the following objectives that the plan must fulfill.

1. Data is encrypted.
2. Complete backups daily, with commonly accessed data backed up hourly.
3. Data backed up to 3 separate locations.
4. At least one off-site backup.

## Arq

I first read about [Arq](https://www.arqbackup.com) a few years back. It ticked a lot of the right boxes for me, but I did not have a chance to fully explore it until last year.

Arq is an application for macOS and Windows that acts as the client for backing up data. It encrypts the data with your own provided key, and then connects to your backup service of choice to upload the data.

The security of Arq was what first brought it to my attention. Before Arq uploads your data to a server, it is encrypted. If your service account is compromised or the data intercepted en route to the service, the data is encrypted and indecipherable. To further protect the data, the format Arq uses is open, and third-party tools have been created that allow extraction of the data, with the proper decryption key.

Since Arq is just a front-end for the backup, it requires a separate cloud service to backup to. Arq lets you backup to all of the following services: [Amazon Drive](https://www.amazon.com/clouddrive/home/), [AWS](https://aws.amazon.com), [B2](https://www.backblaze.com/b2/), [Dropbox](https://www.dropbox.com), [Google Cloud Storage](https://cloud.google.com/storage/), [Google Drive](https://www.google.com/drive/), [Microsoft OneDrive](https://onedrive.live.com), [Wasabi](https://wasabi.com), and if none of these solutions are to your liking, it can backup to a personal [SFTP](https://en.wikipedia.org/wiki/Secure_file_transfer_program) server. Having this level of flexibility is useful, as I can switch between services if needed without having to also replace Arq itself.

## Cloud Storage

The above cloud services have various ways to charge you. Some charge a flat fee per month, others charge by the amount of storage, and some have additional costs for restoring the data. Some charge you per gigabyte of use, whereas others are tiered off by whole terabytes. Separating the storage into these two groups provides costs as follows.

### Services That Charge By Gigabyte

- **AWS Glacier**: $0.004 for storage, $0.09 to restore
- **AWS S3**: $0.023 for storage, $0.09 to restore
- **AWS S3 Infrequent Access**: $0.0125 for storage, $0.09 to restore
- **B2**: $0.005 for storage, $0.02 to restore
- **Google Coldline Storage**: $0.007 for storage, $0.17 to restore
- **Google Nearline Storage**: $0.01 for storage, $0.13 to restore
- **Wasabi**: $0.0039 for storage, $0.04 to restore

### Services That Charge By Terabyte

- **Amazon Drive**: $5 for storage, free to restore
- **Dropbox**: $8.25 for storage, free to restore
- **Google Drive**: $8.33 for storage, free to restore
- **Microsoft OneDrive**: $5.83 for storage, free to restore

Note: Some of the above services(Amazon Drive, Google Drive) offer tiers of 100GB that are priced significantly cheaper than their 1TB pricing. I have not included their pricing above as the value of those tiers is significantly less than any other option, as well as being a much smaller amount of data than I could use. Additionally, annual pricing is used when available and just divided down to what that monthly cost would be.

### All Services Calculated To Charge By Terabyte

- **Amazon Drive**: $5 for storage, free to restore
- **AWS Glacier**: $4.10 for storage, $92.16 to restore
- **AWS S3**: $23.55 for storage, $92.16 to restore
- **AWS S3 Infrequent Access**: $12.80 for storage, $92.16 to restore
- **B2**: $5.12 for storage, $20.48 to restore
- **Dropbox**: $8.25 for storage, free to restore
- **Google Coldline Storage**: $7.17 for storage, $174.08 to restore
- **Google Drive**: $8.33 for storage, free to restore
- **Google Nearline Storage**: $10.24 for storage, $133.12 to restore
- **Microsoft OneDrive**: $5.83 for storage, free to restore
- **Wasabi**: $3.99 for storage, $4.10 to restore

Monthly storage cost is important, but if restoring the data is prohibitively expensive, then that particular option is out. In the case of complete data loss, all of the AWS options and Google Storage options are too expensive. It would cost around one hundred dollars or more per terabyte to restore, which can add up quickly given my backup sizes.

Dropbox, Google Drive, and Microsoft OneDrive are all priced nicely, but their cost comes in strict tiers. For example, Google Drive charges $8.33/month for 1 terabyte when paid annually or $19.99/month for 2 terabytes with no option for an annual discount, but if you need to store more, you must pay $99.99/month for 10 terabytes. There is no middle-ground between 2 terabytes and 10 terabytes. Dropbox and OneDrive offer larger tiers, but there are similar gaps between the small and large tiers. Without more precise control over the amount of storage purchased, these services are either too expensive or not adaptable enough for my needs. Amazon Drive charges per terabyte with a max of 30 terabytes total, but allows the most flexibility of those in this category of services.

## B2

B2 was selected as my cloud backup for a variety of reasons. Due to my data needs currently being sub-terabyte, I wanted to use a service that allowed me to pay per gigabyte. All of the services that charge in this manner are still comparably priced to the ones that charge by terabyte. In the short-term, I am able to save some money by paying per gigabyte, while still not overpaying when my data again reaches the terabyte range.

With the list of services now limited to AWS, B2, Google Cloud Storage, and Wasabi, I had to decide which amongst these 4 services made the most sense.

As mentioned above in the overall storage section, one aspect of pricing that needs to be watched is the cost of restoring data from the services. AWS and Google charge exorbitant amounts to download data back out of their systems. AWS and Google Cloud Storage are meant to be used as the primary storage point for cloud services, and not meant as offsite backup that is restored from. Should I suffer local drive failure, restoring from either service would be doubling what I am already paying on top of replacing the local hardware. 

This leaves B2 and Wasabi. B2 is run by [Backblaze](https://www.backblaze.com), which has been in the cloud backup game since 2007. They have shown themselves to be reliable, making their use as a cloud backup service to not be risky. On the other hand, Wasabi is a new entrant into the cloud storage field, having just launched in the first half of 2017. Their pricing is the cheapest of any of the services outlined here, both in storage and restoration cost. This makes their offering tempting, but when it comes to backing up data, a certain level of reliability must first be proven. This leads me to discounting Wasabi as my primary manner of backing up data, although they are one I will watch for potential future uses.

For all of the above reasons, B2 provides the best bang for my buck without the risks of huge costs further down the road when I will be needing them the least.

## Current Solution

My data is split into two sets: irreplaceable personal data, and multimedia. Both sets of data are stored on the same drive, but my backup solution for the irreplaceable data has a few more parts to it.

Irreplaceable personal data exists in all forms of backup. The main copies are stored in iCloud Drive, which automatically syncs all of the data between my Mac Mini and iPhone, as well as the intermediary servers that Apple runs. Since the iPhone does not keep local copies of all of the files, it is not a backed up device, although it is able to access the files directly from Apple's servers.

In addition to the iCloud syncing, this data is backed up to B2 by way of Arq. Hourly backups are conducted. Daily snapshots are kept for the previous 7 days, and weekly snapshots going back for 60 days.

For my multimedia data, I use the same solution as above, but minus the iCloud syncing and snapshots. Arq still backs up the data to B2, but just one single snapshot is kept. Since this data does not change once it is created, all I need to do is keep it stored.

Finally, all of the above data is kept in a single external hard drive, backed up twice a month using rsync and stored offsite. In the event of complete storage malfunction on my Mac Mini, iCloud Drive would automatically download all data back when the drive is replaced, and multimedia files would be restored from the external drive. Although the possibility is remote, if all data was simultaneously lost on iCloud and B2, the external drive would also provide a backup for this primary data

This puts the locations for my data as follows. Irreplaceable personal data is primarily stored on the Mac Mini and backed up to iCloud, B2, and the offsite external hard drive, totaling 4 locations, 3 of which are offsite. Multimedia data is primarily stored on the Mac Mini and backed up to B2 and the offsite external hard drive. This is a total of 3 locations, with both backups being offsite.

With all of these backup plans in place, my data is in enough places where if all of my backups failed at once, it would likely be due to complete societal and technological collapse, and I would have much larger problems than caring about backups of pictures and music.

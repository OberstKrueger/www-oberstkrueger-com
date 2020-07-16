---
created: 2016-11-17T04:00Z
title: Backups
type: page
updated: 2020-07-16T21:20Z
---

It has been 20 years since I experienced a catastrophic data failure on any of my computers. When this happened, I lost many of the files that were important to me. I did not have aa proper [backup](https://en.wikipedia.org/wiki/Backup) plan in place, and managed to recover but a few that happened to be saved on other machines.

Since then, I have had at least a single backup of my data. While one backup is better than none, I had not removed all risk of data loss. The few times that my primary hard drive failed, I was left with a single working copy of my data. While the data was intact, I was one drive failure away from complete loss.

With the advent of [Dropbox](https://www.dropbox.com), [MobileMe](https://en.wikipedia.org/wiki/MobileMe), and [iCloud](https://www.icloud.com), I began to keep the most important of my files backed up online. Should all of computer storage suffer irreparable damage, I would have the essential files: pictures, school papers, other writings. But I would lose all my music and videos. At the time these services came about, online backup of hundreds of gigabytes was not financially possible.

In recent years, that has changed. Tons of online services focused on data backup have come into existence. These services have reached a point where they are now cheap enough to be viable, even when the amount of data being backed up exceeds 1 terabyte.

### Objectives

Before exploring all the options for a backup plan, I wrote down the following objectives that the plan must fulfill.

1. Data is encrypted.
2. Complete backups daily, with commonly accessed data backed up hourly.
3. Data backed up to 3 separate locations.
4. At least one off-site backup.

## Arq

I first read about [Arq](https://www.arqbackup.com) a few years back. It ticked a lot of the right boxes for me, but I did not have a chance to explore it until last year.

Arq is an application for macOS and Windows that acts as the client for backing up data. It encrypts the data with your own provided key, and then connects to your backup service of choice to upload the data.

The security of Arq was what first brought it to my attention. Before Arq uploads your data to a server, it is encrypted. If your service account is compromised or the data intercepted en route to the service, the data is encrypted and indecipherable. To further protect the data, the format Arq uses is open, and third-party tools have been created that allow extraction of the data, with the proper decryption key.

Since Arq is software that facilitates the backup, it requires a separate cloud service to backup the data. Arq lets you backup to all the following services: [Amazon Drive](https://www.amazon.com/clouddrive/home/), [AWS](https://aws.amazon.com), [B2](https://www.backblaze.com/b2/), [Dropbox](https://www.dropbox.com), [Google Cloud Storage](https://cloud.google.com/storage/), [Google Drive](https://www.google.com/drive/), [Microsoft OneDrive](https://onedrive.live.com), [Wasabi](https://wasabi.com), and if none of these solutions are to your liking, it can backup to a personal [SFTP](https://en.wikipedia.org/wiki/Secure_file_transfer_program) server. Having this level of flexibility is useful, as I can switch between services if needed without having to replace Arq itself.

## Cloud Storage

There are various ways the above cloud services charge you. The primary cost is in the storage itself, which is charged as either a flat fee or rising cased based on total storage used, which is broken down either by per gigabyte used or whole terabytes. The services that charge per gigabyte tend to charge for downloading the data back, although this is not true for all services.

For consistency, all prices have been equalized to price per month for one terabyte, with any limitations noted.

- **Amazon Drive**: $4.99 for storage, free to restore, limit of 30 TB
- **Amazon S3**: $23.55 for storage, $92.07 to restore
- **Amazon S3 Glacier**: $4.10 for storage, $92.07 to restore
- **Amazon S3 Glacier Deep Archive**: $1.01 for storage, $92.07 to restore
- **Amazon S3 Infrequent Access**: $12.80 for storage, $92.07 to restore
- **Amazon S3 Infrequence Access (One-Zone)**: $10.24 for storage, $92.07 to restore
- **Backblaze B2**: $5.12 for storage, $10.24 to restore
- **Dropbox**: $5.52 for storage, free to restore, limit of 3 TB
- **Google Archive Storage**: $1.22 for storage, $158.72 to restore
- **Google Cloud Standard**: $20.48 for storage, $107.52 to restore
- **Google Coldline Storage**: $4.09 for storage, $128.00 to restore
- **Google Nearline Storage**: $10.24 for storage, $117.76 to restore
- **Google Drive**: $9.99 for storage, free to restore, limit of 30 TB
- **Microsoft OneDrive**: $5.83 for storage, free to restore, limit of 1 TB
- **Wasabi**: $5.99 for storage, free to restore, limit of one complete restore per month

## Balancing The Cost

Finding the balance between the cost of both data storage and restoration is important. Most of the above options fall into one of two categories: more expensive storage with less expensive data restoration, or less expensive storage with more expensive data restoration.

Four of the above categories fall into what I would consider expensive for both data storage and restoration (Amazon S3, Amazon S3 Infrequent Access, Google Cloud Storage, and Google Nearline Storage) and are not good options for any data backup. The services with an upper cap on the amount of data that can be stored (Amazon Drive, Dropbox, Google Drive, and Microsoft OneDrive) make them inadequate for backing up.

To decide whether it is more cost efficient to use a service that is more expensive for data storage or retrieval, I look at my past needs when it comes to restoring backups. My backup strategy has relied on online backups for 4 years now, without ever experiencing a complete data loss. While it is not reasonable to assume that this trend of not needing to restore will ever change, it is reasonable to assume that I will need to do a complete backup restoration every few years at most, likely in the range of once every five or more years.

With this assumption in mind, I created a small Swift program that figured out at what point does the cheap storage option become more cost efficient. I compared the two options that were at the best option for each category based on price: Amazon S3 Glacier Deep Archive for cheaper data storage, Backblaze B2 for cheaper restoration. The code for this program is as follows:

    struct Service {
        let monthly: Float64
        let restore: Float64
    }

    func compare(_ first: Service, _ second: Service) {
        func total(_ service: Service, _ period: UInt) -> Float64 {
            return (service.monthly * Float64(period)) + (service.restore)
        }

        var check: Bool = true
        var period: UInt = 1

        while check {
            let firstTotal = total(first, period)
            let secondTotal = total(second, period)

            print("Period \(period) => \(firstTotal) => \(secondTotal)")

            if firstTotal < secondTotal {
                check = false
            } else {
                period += 1
            }
        }
    }

    let storage = Service(monthly: 1.01, restore: 92.07)
    let retrieval = Service(monthly: 5.12, restore: 10.24)

    compare(storage, retrieval)

Running this script, the result was in that at the 20 month mark, cost efficiency flipped to favor the service with cheaper storage. With this period being less than 2 years, the best case scenario surpassed the five year assumption previously made.

## A World-Wide Backup

Knowing that money can be saved by switching to one of the cheaper storage options, I then explored the possibility of backups stored in multiple locations world-wide. Due to the [COVID-19 pandemic](https://en.wikipedia.org/wiki/COVID-19_pandemic), my ISP graciously granted me unlimited bandwidth for a nearly three-month period, which meant replicating my backups across multiple regions was feasible without incurring bandwidth overage charges.

The above backup objectives note that data should be stored in 3 separate locations, with at least 1 of them being offsite. In this instance, location is defined as the device location, not physical location. Data backed up to another hard drive stored in the same physical location fulfills this requirement. In the case of total home destruction, I would have access to only one copy of my data, that being the offsite backup. If all 3 backups were stored offsite and at different regional locations, I could suffer home destruction and have 3 copies of my data exist online.

Taking this a step further, if all 3 offsite backups were spread equally around the world, my data backups could become as close to natural disaster or war-proof as possible. In the apoclyptic event that an entire continent were laid to waste, my data would exist elsewhere in the world.

This does increase the cost. Simple math tells me that based on the above code, I could store my data in 5 separate locations without raising the monthly cost. But when you run those numbers through the above program, the flipping point for cost efficiency becomes 1,170 months. While the transhumanistic dream wants me to hope I can live that long, my risk aversion does not believe I could go nearly 100 years without complete data loss within my home. Going back to storing in 3 locations as outlined in the original objectives reduces the flipping point to 40 months, which is sufficient for my needs.

## Retrieval Times

The above calculations show AWS S3 Deep Glacier to be the cheapest solution, but cost is not the only factor to consider. One of the features that differentiates Google's archival storage options against Amazon's is that S3 Glacier Deep Archive has non-instantaneous retrieval times. If the speediest option is paid for, there is a 12 hour wait period before data can be downloaded back from Amazon. This would not be a major concern for a full backup restoration, as the download speed would take multiple days, and an additional 12 hours is noticeable but not a substantial portion of that time. Google's options do not require a waiting period, albeit at a cost increase of 72% for all data restoration processes.

Where this becomes an issue is in instances where I need to restore a small portion of the backup. These are more likely to be time-sensitive matters, and having to wait 12 hours could cause a delay in work that I am trying to complete. For these situations, the increased cost would not be substantial, as it is unlikely I would be restoring huge swaths of data. The timeliness is the more important facet of restoration.

## Current Solution

Running the above Swift code but with Google's Deep Archive pricing in it yields a return time of 4 years and 8 months when the data is split over 2 world-wide locations, and 8 years and 6 months when using 3 locations. The latter is a substantially longer period of time than I aimed to have, but with the requirement of having data stored in 3 locations, it is important that I use that pricing as my baseline. I decided that being the most cost efficient isn't the only goal, and paying a little more for convenience is an acceptable trade-off.

The Google Deep Archive data is stored in 3 locations around the world. The first location is in North America, allowing fast download speeds. This location will be the primary recovery location should I ever need to pull from the backup. The second location is in Europe, and the third location is in South East Asia. Should anything befall my data in all locations, then I will have much larger problems to worry about.

This first set of data is what I consider my archive and multimedia set. There is a second set of data that is more active working on my part, such as my writings and programming. This data is stored on iCloud, giving me a secondary backup option on Apple's servers, while allowing syncing between all my devices. All iCloud files are backed up to the above Google Deep Archive locations, putting this data in 4 separate places.

All data is backed up using Arq. The backup runs hourly, with the following retention schedule: hourly backups are kept for 7 days, daily backups for kept for 30 days, weekly backups are kept for 1 year, and monthly backups are kept for 10 years. This guarantees that any data I delete will be recoverable for a longer period of time than I would likely need it.

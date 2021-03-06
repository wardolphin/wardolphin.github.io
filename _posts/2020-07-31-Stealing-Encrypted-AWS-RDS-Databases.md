---
layout: post
title: Stealing Encrypted AWS RDS Databases
--- 
 
This post is about techniques to transfer databases between AWS accounts for penetration testing purposes.
 
 If you gain access to the AWS console you are usually a very happy hacker. No doubt you have a number of ways to gain access to the critical information you are after and extract it. What you usually want though is the fastest way. The clock is ticking as soon as you are in, especially if alerts are set up for potential malicious actions. 
 
One technique that is fairly fast and reliable is simply sharing a database backup or snapshot from the compromised account to an external account controlled by the attacker. 
 
This takes about 4 clicks and will give you a full copy of the entire database that you can snapshot yourself and save for later. *do note that there are standard security alerts written for this action in CloudTrail, so be prepared to be burned very quickly after initiating an action like this*
 
To see how to share an RDS snapshot to an external account follow steps [here](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_ShareSnapshot.html).
 
What happens when you find yourself in a situation with a high privileged AWS user account and AWS console access but the database is encrypted? As outlined above you can prepare for the transfer of an unencrypted DB fairly quickly, but things get complicated when encryption is involved. You might assume what I think most people assume, that encryption is adequate protection against stealing the DB via transfer. However, with some time pressure, desperation, and intense documentation reading an alternative solution has been found.
 
# Background
## KMS Keys keys kEyS
 
AWS has several options for management of CMK's (Customer Master Keys). These are the keys that customers use to encrypt their data (and databases!).
 
AWS has great documentation so if you want to read it straight from them you can get a good overview here: https://docs.aws.amazon.com/kms/latest/developerguide/concepts.html
 
I'm going to give a simplified overview that gives the relevant info for our situation.
 
CMK's can be divided into 3 categories. I've conveniently listed them in order of ease of hacking along with  the basic instructions on how to decrypt the database.
 
### Types of Encryption Keys
**Customer Managed Keys** - Edit the key policy yourself to grant your account access to the key  
**AWS Managed Keys** - Create a new key (customer managed) in a different region and then create a snapshot copy in that region encrypted with your newly created key  
**AWS Owned Keys** (unknown- haven’t looked into this)
 
Below I'll expand on detailed steps and explanation of each technique.
 
# Techniques
## Decrypt a Customer Managed Key Database Snapshot
*note you must have access to a fairly high permissioned account that can manage keys*
1. Locate a snapshot or automated backup of the database. RDS>Snapshots is a good place to look, for example. Make sure to check the manual and System tabs on that page. As always, if you see nothing, make sure to check all the Regions available in case you are in the wrong one. Snapshots are one off copies of the database. Engineers quite often have an automated backup schedule for emergency restore purposes using the AWS Backup Service or the automated backup window for the database.
2. If you don't have a snapshot available or any backups, then you will have to risk creating a snapshot of your own. I think it will warn you if there is any danger but I suppose do this at your own risk. :)
3. Every CMK has a [key policy](https://docs.aws.amazon.com/kms/latest/developerguide/key-policies.html) attached to it. Policies control who can access the keys. One of the advantages of having a customer managed key is that you can edit/manage the key policy. So essentially you would [grant your own account access to the key by modifying the policy for the key used to encrypt the database you were after](https://docs.aws.amazon.com/kms/latest/developerguide/key-policy-modifying-external-accounts.html).
4. [Share](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_ShareSnapshot.html) the database snapshot with an IAM/user in your external AWS account.
5. Grant an IAM user in your account access to the CMK using [policies](https://docs.aws.amazon.com/kms/latest/developerguide/iam-policies.html).
6. [Restore the snapshot](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_ShareSnapshot.html)
7. Reset the DB password https://aws.amazon.com/premiumsupport/knowledge-center/reset-master-user-password-rds/
8. Shoot’n Loot’n
 
## Decrypt an AWS Managed Key Database Snapshot
1. Follow Steps 1 + 2 above
2. Create a new **Customer Managed Key** in a **different AWS region** than the one the snapshot exists in. 
    - You **cannot** manage the key policy of an AWS managed key so this is where the loophole comes in. In order to decrypt the database the key material is needed. So instead you can copy the database to another key region and *create your own new key* to handle encryption and decryption. See Handling Encryption for explanation on [this](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_CopySnapshot.html) page or for a step by step instructional guide click [here](https://aws.amazon.com/blogs/database/securing-data-in-amazon-rds-using-aws-kms-encryption/). 
As explained in the above article:
>>>AWS KMS (Key management service) keys are Regional constructs. So, to copy a snapshot to another Region, you first must create a KMS key in the destination Region. Use this new key to encrypt the snapshot in the destination Region.
3. Copy the DB snapshot to a new region encrypting it with the new key you just created. See [Copying a DB Snapshot](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_CopySnapshot.html) for a step by step guide.
4. Continue on by following the process described in the last section, starting at step 3.
 
Hope this helps you on your final steps of operation success!

Special thanks to @mangopdf for locating the sacred texts required for these techniques in amazon's documentation!

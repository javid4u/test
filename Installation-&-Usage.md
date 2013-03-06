Hi Everyone,

Here's the installation and usage guidelines for the OpenEMR SMS Notifications using Twilio.

Usage of this script is pretty simple and we've thoroughly tested it and it works well. It takes less than 5min to setup.

**BACKUP FIRST!!**

Users just have to copy the files and folders I’ve provided, into the OpenEMR directory. Details below:

**Files Modified: (replace the existing)**
/var/www/openemr/library/globals.inc.php
/var/www/openemr/modules/sms_email/reminder/cron_sms_notification.php

**New Files/Directories Added:**
/var/www/openemr/modules/sms_email/reminder/sendnotifications.php
/var/www/openemr/modules/sms_email/reminder/twilio

**Cron for the script:**
Can be set to run every hour (or whatever you wish)
Command:
**wget -q --spider  http://IP_NUMBER/openemr/modules/sms_email_reminder/cron_sms_notification.php**
(change IP_NUMBER in above command to IP Number of OpenEMR on which the twilio script is running)

**SMS Body:**
This is now in the cron_sms_notifications.php file on line 141 and should be edited there as required.

**Usage:**
### 1. Placing files & Folders:
As soon as you will copy the provided files and folders (and replace globals.inc.php & cron_sms_notification.php); Administration >> Globals >> Notifications will have 3 new fields:
Twilio Account SID, Twilio Auth Token, Twilio From Name
You will need a Twilio a/c with SMS credits in it (minimum $20 – _they have very good rates and that’s why I got down to working on this script_) I understand Twilio also have a sandbox feature for testing purposes.
With your Twilio a/c will also come an **SMS number** which will be used to send SMS’s and the the recipient will receive your SMS’s from this number. (You can choose your number/location)
Also in your Twilio a/c will be the **Account SID** & the **Auth Code**. Fill in these details into the new fields you will see in **Administration >> Globals >> Notifications**
(I’ve placed a snapshot for your reference at http://www.NetConnexions.net/twilioopenemr/administration_globals_notification.jpg)
and Save.
### 2. Body of the SMS:
Next you need to set the message that will be received in the SMS. This is now in the cron_sms_notifications.php file on line 141 and should be edited there as required.
### 3. Setting a CRON for background auto-sending as per scheduled appointments:
Can be set to run every hour (or whatever you wish)
Command:
`wget -q --spider  http://IP_NUMBER/openemr/modules/sms_email_reminder/cron_sms_notification.php`
(change IP_NUMBER in above command to IP Number of OpenEMR on which the twilio script is running)
### 3b. Doing a manual run:
While you are testing the script, you may want to do a test-run of outgoing SMS’s instead of using CRON. Here’s what I did:
* Set the SMS Notification Hours to 1
* Make a test patient and use your own mobile/cell number in the Contact (use the number format: _+CountrycodeAreacodeNumber_ (**preceding + is important and there should be no spaces, hyphens or periods anywhere**) ). Make sure you select ‘Yes’ for your test patient’s “Allow SMS” (in Demographics >> Choices).
* Schedule an appointment for your test patient an hour away. Open the following URL: 
http://IP_NUMBER/openemr/modules/sms_email_reminder/cron_sms_notification.php
(change IP_NUMBER in above command to IP Number of OpenEMR on which the twilio script is running).
* If all’s OK, you should see something like what’s in the screenshot at:
[http://www.NetConnexions.net/twilioopenemr/sms_sent_success.jpg](http://www.NetConnexions.net/twilioopenemr/sms_sent_success.jpg)
and you should receive the SMS(if your Twilio a/c has enough SMS credits). You can also log into your Twilio a/c and see the SMS Messages Log. I’ve placed a snapshot showing 3 successful SMS’s sent:
[http://www.NetConnexions.net/twilioopenemr/twilio_log.jpg](http://www.NetConnexions.net/twilioopenemr/twilio_log.jpg)

### 4. Getting the SMS’s out:
Once all the above is in place, schedule appointments in OpenEMR as normal and 50hrs before the appointment(or whatever you’ve set for SMS Notification Hours), reminder SMS’s should be sent out as an automated background process and reflected in your Twilio SMS logs.
**Note: For your current and new patients, set their Mobile Phone numbers using the number format: +CountrycodeAreacodeNumber (preceding + is important and there should be no spaces, hyphens or periods anywhere) ). Make sure you select ‘Yes’ for your test patient’s “Allow SMS” (in Demographics >> Choices).**

If you want to see a working version of this in OpenEMR, send me a private message and I’ll give you access to mine.

If you require any additional info or clarifications, pls contact me.
I can also provide reports on the modifications made to **globals.inc.php** and **cron_sms_notification.php** showing side-by-side comparisons of the original vs. the modified versions.

Thanks and Kind Regards,
Fayyaz Kasmani.
 
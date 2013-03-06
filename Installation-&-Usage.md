Hi Everyone,

Here's the installation and usage guidelines for the OpenEMR SMS Notifications using Twilio.

Usage of this script is pretty simple and we've thoroughly tested it and it works well. It takes less than 5min to setup.

**BACKUP FIRST!!**

Users just have to copy the files and folders I’ve provided into the OpenEMR directory, details below:

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
[u]1. 1. Placing files & Folders:
As soon as you will copy the provided files and folders (and replace globals.inc.php & cron_sms_notification.php); Administration >> Globals >> Notifications will have 3 new fields:
Twilio Account SID, Twilio Auth Token, Twilio From Name
You will need a Twilio a/c with SMS credits in it (minimum $20 – [i]they have very good rates and that’s why I got down to working on this script[/i]) I understand Twilio also have a sandbox feature for testing purposes.
With your Twilio a/c will also come an [b]SMS number[/b] which will be used to send SMS’s and the the recipient will receive your SMS’s from this number. (You can choose your number/location)
Also in your Twilio a/c will be the [b]Account SID[/b] & the [b]Auth Code[/b]. Fill in these details into the new fields you will see in Administration >> Globals >> Notifications
(I’ve placed a snapshot for your reference at [url=http://www.NetConnexions.net/twilioopenemr/administration_globals_notification.jpg]http://www.NetConnexions.net/twilioopenemr/administration_globals_notification.jpg[/url])
and Save.
[u]2. Body of the SMS:[/u]
Next you need to set the message that will be received in the SMS. This is now in the cron_sms_notifications.php file on line 141 and should be edited there as required.
[u]3. Setting a CRON for background auto-sending as per scheduled appointments:[/u]
Can be set to run every hour (or whatever you wish)
Command:
[b]wget -q --spider  http://IP_NUMBER/openemr/modules/sms_email_reminder/cron_sms_notification.php[/b]
(change IP_NUMBER in above command to IP Number of OpenEMR on which the twilio script is running)
[u]3b. Doing a manual run:[/u]
While you are testing the script, you may want to do a test-run of outgoing SMS’s instead of using CRON. Here’s what I did:
-Set the SMS Notification Hours to 1
-Make a test patient and use your own mobile/cell number in the Contact (use the number format: [i]+CountrycodeAreacodeNumber[/i] ([b] preceding + is important and there should be no spaces, hyphens or periods anywhere[/b]) ). Make sure you select ‘Yes’ for your test patient’s “Allow SMS” (in Demographics >> Choices).
Schedule an appointment for your test patient an hour away. Open the following URL: 
http://IP_NUMBER/openemr/modules/sms_email_reminder/cron_sms_notification.php
(change IP_NUMBER in above command to IP Number of OpenEMR on which the twilio script is running).
If all’s OK, you should see something like what’s in the screenshot at:
[url=http://www.NetConnexions.net/twilioopenemr/sms_sent_success.jpg]http://www.NetConnexions.net/twilioopenemr/sms_sent_success.jpg[/url]
and you should receive the SMS(if your Twilio a/c has enough SMS credits). You can also log into your Twilio a/c and see the SMS Messages Log. I’ve placed a snapshot showing 3 successful SMS’s sent:
[url=http://www.NetConnexions.net/twilioopenemr/twiliolog.jpg]http://www.NetConnexions.net/twilioopenemr/twiliolog.jpg[/url]
[u]4. Getting the SMS’s out:[/u]
Once all the above is in place, schedule appointments in OpenEMR as normal and 50hrs before (or whatever you’ve set for SMS Notification Hours) the appointment, reminder SMS’s should be received and reflected in your Twilio SMS logs.
[b]Note: For your current and new patients, set their Mobile Phone numbers using the number format: +CountrycodeAreacodeNumber (preceding + is important and there should be no spaces, hyphens or periods anywhere) ). Make sure you select ‘Yes’ for your test patient’s “Allow SMS” (in Demographics >> Choices).
[/b]
If you want to see a working version of this in OpenEMR, send me a private message and I’ll give you access to mine.

If you require any additional info or clarifications, pls contact me.

Thanks and Kind Regards,
Fayyaz Kasmani.
 
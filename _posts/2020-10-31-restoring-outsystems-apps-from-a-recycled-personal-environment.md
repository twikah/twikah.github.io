---
postHero: /images/outsystems-model.png
title: 'Restoring OutSystems apps from a recycled personal environment'
categories: work
tags: [web-development, outsystems]
---

It's been a while since I last used my OutSystems personal environment.

I knew that, after a certain period of inactivity, OutSystems would recycle my
environment. You get some emails alerting you to this and then, if you do not
take action, you'll receive a final email with a link to reclaim your environment
in the future and another link to download a backup file with the apps you had
on your environment.

When I received this last email I was pretty happy that I had a way of recovering
the apps. A month had passed when I finally made some time to wake my environment
up to do some training. I had no issues with waking up the environment, but then!
I had no idea how to recover my old apps. What I mean is, I downloaded the backup
file from that last email I mentioned above, but I had to do some research before
I could access my apps on Service Studio.

Hence, this post is a way of hopefully making it easier for future newbies like
myself to go through this process more smoothly.

First of all, please note that:

&nbsp;&nbsp;&nbsp;&nbsp; 1. The backup file to access your old apps is only valid for 6 months;

&nbsp;&nbsp;&nbsp;&nbsp; 2. The backup file restores the apps but not any data.

Alright, so, I saw myself with a .osp file and no clue on what to with it. I
headed to Service Studio but I couldn't find any indication on where to upload
this .osp file. My next step was to double click on the .osp file, which opened
a wizard requiring some server information on where to upload the apps, namely
the 'Host Name', 'User Name' and 'Password'. The 'Host Name' is the server's name -
in case of personal environments, it will be something like
your_id.outsystemscloud.com. Then, the User Name and Password are the details
you use to enter your environment on Service Studio. I then clicked on the
'Upload' button, waited for the process to finish, reopened Service Studio,
*et voilà!* My apps were back.

<img class="pull-left" src="/images/osp-file.png"
alt="osp file wizard" style="width: 60%;">

This is how I overcame the issue but I looked up the forums for people struggling
with the same topic and I found
[this](https://www.outsystems.com/forums/discussion/16839/space-reclaimed-i-have-backup-how-do-i-load-from-backup/)
solution. The screenshots on that post are a bit old but I'd say the process
described to upload the backup file would be the same. I didn't test it but
you'll most likely get the same result.

<br>
<br>
<br>

I also found
[this](https://success.outsystems.com/Support/Personal_Environment/What's_an_OutSystems_personal_environment%3F)
article from OutSystems regarding personal environments with some more
interesting info.

All in all, getting my apps back wasn't so hard. I just think it would be really
handy to have these instructions either on the email that contains the link to
the backup file or on our platform home, where we can wake up the recycled
environment.
---
title:  "Usage of sendmail util"
search: true
categories: 
  - Recipes
tags:
  - linux
  - bash
  - crontab
  - sendmail
  - aws-ses
  - aws-ec2
---

Recently I've faced with a problem on Amazon EC2 instance.
The problem was that it's impossible (or I just didn't find a way) 
to send an email with a result of a cron job to a list of receivers, from a custom sender and with a custom subject.
I've tried to use basic capabilities of `crontab` util and `MAILTO` directive, but:
1. I wasn't able to specify sender since there is no `FROMTO` directive.
2. As a result of the first issue, `crontab` uses the following format of the sender: `root@ip-111-11-0-11.us-east-1.compute.internal`.
But if you use Amazon SES you have to confirm sender's and receiver's address and `root@ip-111-11-0-11.us-east-1.compute.internal`
you won't be able to confirm.
3. I wanted to specify a custom subject.

Therefore I've decided to use features of `sendmail` util and here is how I use it:
```bash
#!/usr/bin/env bash
(echo "Subject: Hello, World! "; echo | /var/job.sh) 2>&1 | /usr/sbin/sendmail -F -i -f noreply@sender.com -t first@recipient.com second@recipient.com
```

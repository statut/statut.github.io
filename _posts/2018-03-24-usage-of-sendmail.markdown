---
title:  "Usage of sendmail util"
search: true
categories: 
  - Recipes
tags:
  - linux
  - bash
last_modified_at: 2018-02-19T08:05:34-05:00
---

Sending an email to recipient with a subject, a result of executed job from predefined sender via sendmail linux util.
```bash
#!/usr/bin/env bash
(echo "Subject: Hello, World! "; echo | /var/job.sh) 2>&1 | /usr/sbin/sendmail -F -i -f noreply@sender.com -t first@recipient.com second@recipient.com
```
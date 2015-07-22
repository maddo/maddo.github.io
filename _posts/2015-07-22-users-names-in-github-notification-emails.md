---
title: User's names in Github notification emails
layout: post
published: yes
---

# {{ page.title }}

22 Jul 2015 - Buenos Aires

Throughout years of using Github, I've encountered a minor annoyance related to the reply-to field of Github notifications.

Though it affects several types of notifications emails, looking at pull request comment notifications will suffice to convey the idea.

When a user comments on a pull request, attached parties will receive an email sent from:
`Commenting User <notifications@github.com>`

The precise damage of this mixing of a unique user's name and a general Github email address depends on the email client being used, and the awareness of the email client user.

Two side effects I've noticed include:

* Accidentally sending an email to `notifications@github.com` when intending to send an email to the aliased individual.
* Certain email clients build up a contact list automatically, based on usage, for example, by replying to one of the Github notification emails to add your two cents to the pull review conversation. If you already have Joe Schmoe's email in your address book, you might end up with two entries for Joe, one of which is useless:
    * `Joe Schmoe <jschm@gmail.com>`
    * `Joe Schmoe <notifications@github.com>`

There's nothing here that can't be avoided with careful user behavior, but I think Github could do something better.

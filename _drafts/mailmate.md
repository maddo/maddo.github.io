#### TODO add headers

I thought I'd share my experience setting up Tags with a Gmail account in MailMate[^1], which turned out to be pretty cool. For the record, it's all in the wonderful [official documentation](https://manual.mailmate-app.com/account_setup#gmail)[^2].

Why any of this? It boils down to Google's IMAP implementation, and the fact that most emails exist in All Mail _and_ some other folder/label or the Inbox. As an example of why that matters, MailMate has some nifty power-user features, like double clicking on the subject or sender to find all matching messages. With emails duplicated across folders, each result appears twice, and things start to get messier from that point. (Imagine, for example, deleting one message and watching as two messages dissappear because they're technically the same message). Anyhow, enough preamble, let's configure.




[^1]: https://freron.com/
[^2]: https://manual.mailmate-app.com/account_setup#gmail


### Notes

```
Digging back into MailMate again. Gmail for work. Integration improved. It's all here: https://manual.mailmate-app.com/account_setup#gmail

Basically:
* Gmail does IMAP it's own way.
* MailMate does it the IMAP way.
* This caused problems (duplication of messages which breaks cool features like double click to search)
* Tags! (better than folders)
* tag column
* cool tag emoji
* folders disappear (yay)

Bonus lesson: once you've got all these tags, you can:
1. show images for messages marked "not junk"
2. set tags you trust to "not junk"
```
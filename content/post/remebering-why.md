---
title: Remembering Why
date: 2010-04-27T08:25:00-06:00
draft: false

---

You have someone come to you and say they want to implement "it" on  the database or SQL Server instance.  Or it could be maybe you hear a  conversation about implementing "it".  Unlike me, I don't recall things  "word for word" but remember reading about "it" not being a good idea in  certain circumstances or at all.

One particular thing I know of that  will get the blog post rolling is posting on a forum  "how can I schedule or how often should I shrink my database(s)?".  Which I  had this come up recently when a customer put in a request to have a  shrink job added prior to the backup occurring each day.  (Wait keep  reading first...).  I asked them why they thought they needed a shrink  job.  The customer returned with "we are trying to make them as small as  possible for zipping and shipping the data off to the customer".  Which  a few lines into the conversation I found he was referring to the  backup file, and trying to make it as small as possible.

I read a good bit of blogs and articles (at least try too).  I know from all that reading that shrinking the database can cause server fragmentation.  If you designed and configured the database right to begin with, there should be no reason to continually shrink the database (or at most very, very, very few occasions where you need to).  As well, all shrinking is going to do is cause the database to grow when more data is written.

Anyway, all that got me to thinking...where do I keep all those "justification" articles as to why you don't do this or that?  Sad to say, I can't remember where I keep it or even if I do have such a document laying around.  So...what else is a blog for than for documenting things you want to keep up with, and share with other people too.  So from this post I will try to start working on a page (title yet to be determined) that includes my favorite articles on why you don't do certain things.  (I will update this post with the link once I create and publish it.)

Hopefully the ambition to do this stays with me.  I will have to look at first checking with those authors to make sure they are aware I'm doing it :).  I know there are a few "wiki" sites that gather some of this information for you, and will include those as well.

---
layout: post
title:  "Android Turbo SFTP Client"
date:   2015-06-30 19:38:39
categories: android sftp turbo client
---
Since I [switched to this Jekyll blog][blog], one of my hiccups was how to get the files I needed over to my web server. In most instances it's *super* easy. If there's an image I need that I already have publicly available on the Internet somewhere, for example, I can simply connect in via SSH and `wget` it. Failing that, from my Windows laptop I can leverage [WinSCP][winscp]. If I'm on a Chromebook, I can use pretty much any web IDE like [Codeanywhere][codeanywhere] or [Cloud9][cloud9] to gain SFTP access. Admittedly, those scenarios make up the overwhelming majority of the instances where I'm looking to move content onto my web server. However, there are still outliers, and my phone is a big one.

In some instances I may need to take a photo - or more likely a [screenshot][screenshot] - and get it over to my server. Obviously I can get it into a place where it's accessible from one of my laptops, but that's a hassle if I can avoid it. So how do I get something from a phone or tablet onto a web server? The answer is mostly the same as any other device: SFTP. I figured there *had* to be some SFTP clients for Android. After a bit of searching around I settled on one called [Turbo][turbo]. It's simple, lightweight, free, and adheres to Material Design guidelines. I really couldn't ask for much else. After plugging in my server's information and then providing a username and password, I was able to connect without any issues.

![Turbo Client](/images/2015/turbo_client.jpg)

What's really neat is that, along with the SFTP portion that allows me to easily download and upload files from my server, Turbo comes bundled with an editor application as well. This editor can be leveraged to actually open documents, pieces of code, etc. hosted on the server for quick edits as well. I doubt I'll really need to use it for anything since I do all of my work in Markdown (and I **really** don't want to write a full, Markdown-laden post on my phone), but it could be handy in a pinch if I needed to update a .css file or something.

The other thing I found myself needing to contend with was handling the *size* of my images. My phone has a 1080 x 1920 screen resolution, so naturally that's the size of my screenshots. While by default Jekyll includes a nice `max-width: 100%` definition for `img` tags, I still don't want screenshots which are *that* massive. While Android's **Photos** app will allow for basic edits I didn't see resizing among them. Luckily, I did some more searching and found a simple app called [Photo Editor][photoeditor] in the Play Store. Sure enough, it has a very streamlined function for resizing photos, including some nice presets so that you can very quickly and easily opt to make a photo something like 640 pixels wide or any other "standard" size.

The two applications combined make it easier than ever for me to take a photo or screenshot from my phone, resize it, and then upload it to my web server. Then when I actually SSH in the *only* thing I have to worry about is hammering out my content.

[blog]: https://mads.ninja/blogging/software/platforms/2015/06/27/blogging.html
[winscp]: http://winscp.net/eng/download.php
[codeanywhere]: https://codeanywhere.com/
[cloud9]: https://c9.io/
[screenshot]: https://mads.ninja/google/play/music/radio/2015/06/29/play-music.html
[turbo]: https://play.google.com/store/apps/details?id=turbo.client
[photoeditor]: https://play.google.com/store/apps/details?id=com.iudesk.android.photo.editor

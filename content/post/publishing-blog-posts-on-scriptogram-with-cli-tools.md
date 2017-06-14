+++
date = "2014-01-23"
title = "Publishing blog posts on scriptogram with cli tools"
tags = ["dropbox"]
+++

To publish a post on scriptogram you need to write a file in markdown format to the Apps/scriptogram folder on your linked dropbox account.

Here we use [dropbox_uploader.sh](https://github.com/andreafabrizi/Dropbox-Uploader) to upload to dropbox from a headless Linux box (in this case a RPi running Arch Linux).

A quick peek at the markdown file:

    [craigb@alarmpi ~]$ head scriptogram-cli.md
    Date: 2014-01-23
    Title: Publishing blog posts on scriptogram with cli tools

Now upload to your linked dropbox (assumes you already did the first run dropbox_uploader.sh setup)

    [craigb@alarmpi ~]$ dropbox_uploader.sh upload scriptogram-cli.md Apps/scriptogram/posts/scriptogram-cli.md
    Uploading "/home/craigb/scriptogram-cli.md" to "/Apps/scriptogram/posts/scriptogram-cli.md"... DONE

If you have autosync enabled on your scriptogram account, your website will be automagically regenerated and published. Otherwise login to scriptogram, go to the dashboard and click "synchronize".

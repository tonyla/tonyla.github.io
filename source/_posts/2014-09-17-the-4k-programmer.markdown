---
layout: post
title: "The 4k Programmer"
date: 2014-09-17 19:28:34 -0400
comments: true
categories:
- Developer Tools
- Remote Office
---

In my internet travels I happened across this link [(4k is for programmers)](http://tiamat.tsotech.com/4k-is-for-programmers) about using a 4k Seiki as a primary display.
As I've always been a believer in more pixels, I figured why not give this a shot.

## My Old Setup

The setup that I was replacing was

* 2 x 24 inch monitors (one Samsung and one Dell) on 2 [Ergotron LX desk mounted arms](http://www.ergotron.com/tabid/65/PRDID/351/language/en-CA/default.aspx)
* 1 x Late 2012 model Mac mini

{% img /images/posts/4kp/before.jpg 600 auto %}

## Setup and Installation

Reading several blogs/forum posts I cobbled together the following requirements for getting the Seiki to run.

### Hardware

#### [Seiki 39" LED 4k TV (SE39UY04)](http://www.tigerdirect.ca/applications/SearchTools/item-details.asp?EdpNo=8430969&CatId=8893)
The Seiki 39" 4k TV is relatively easy to find online and even in B&M stores. I bought mine at local B&M store called [Tiger Direct](http://www.tigerdirect.ca).

#### [Accell (B086B-003B-2) UltraAV DisplayPort 1.1 to HDMI 1.4 Active Adapter - AMD Eyefinity Certified](http://www.amazon.ca/gp/product/B00DOZHLAA/ref=as_li_qf_sp_asin_tl?ie=UTF8&camp=15121&creative=330641&creativeASIN=B00DOZHLAA&linkCode=as2&tag=tonyla-20)

{% img /images/posts/4kp/accell.jpg %}

As far as I can gather this piece along with some software shenanigans (detailed below) are required to optimally connect the Seiki TV to my late 2012 mini (this includes all but the newest MacBooks with retina displays).

###Software

#### [Mac Pixel Clock Patch](https://github.com/vinc3m1/mac-pixel-clock-patch)
In conjunction with the Accell adapter most current Mac mini's and macbooks require a software patch to run 4k displays @ 30 Hz. I believe if you don't do this the highest refresh rate you are able to connect at is 18Hz if it runs at all.

Unfortunately at the time of writing this post this and the many other variants out there have not updated for OSX 10.9.4 yet. I did go through the steps in the README.md and verified that the patch command for 10.9.2 is still valid just the MD5 of the file has changed.
So I just ran these commands manually as root, be very careful to backup IOKit as if something goes wrong you may need to restore it via recovery console.

``` bash Patch https://github.com/vinc3m1/mac-pixel-clock-patch/blob/b2005690487ea18e592ae59f76d15b4ed66978d5/macPixelClockPatcher.command#L145 Source
cp /System/Library/Frameworks/IOKit.framework/Versions/A/IOKit /System/Library/Frameworks/IOKit.framework/Versions/A/IOKit.bak
sudo perl -i.bak -pe '$before = qr"\x0F\x85\x9D\x03\x00\x00"s;s/$before/\xE9\x84\x03\x00\x00\x90/g' /System/Library/Frameworks/IOKit.framework/Versions/A/IOKit
```

This patch basically bypasses the software checks on the supported refresh rates for the attached video card. This is what enables my mini to run 3840x2160@30Hz.


## Initial Impressions

I've had this setup running for over a month and overall I can say my experience is positive.

### Pros

* Less scrolling when reading code
* Less application switching because you have more active applications
* Text is crisp and it isn't too small
* This monitor is one of the most inexpensive "upgrades" I have done
* Watching videos looks really good

### Cons

* Extremely bright (Fixed below)
* Colors are terrible (Fixed below)
* Secondary monitor does not work on my Mac Mini
* Monitor is large so it results in more head movement then traditional monitor sizes
* Input lag is apparent but personally is not a huge deterrent

## Improving The Experience

Some of the cons above were almost deal breakers, especially the first 2. So I went about trying to find ways to mitigate/eliminate those cons in order to make this experiment a success.
The first 2 issues were linked as most advice online about making the Seiki TV more friendly as a computer monitor was to turn the "brightness" down to zero very close to it and to set "sharpness" to zero.
Because the way that colors work ([YPbPr](http://en.wikipedia.org/wiki/YPbPr)) turning down brightness affect color reproduction and even with brightness set all the way down to zero the backlight of the TV was too bright for me.

#### Solution

The solution is hidden away in the service menu. The service menu is accessible by brining up the regular menu

{% img /images/posts/4kp/menu.JPG 600 auto %}

Then you press the number 0 four times and it will open up the service menu

{% img /images/posts/4kp/service-menu.JPG 600 auto %}

Hidden away in the "other" option at the bottom is the "LED Backlight option".
{% img /images/posts/4kp/other-menu.JPG 600 auto %}

This is what solved the issue of extreme brightness and poor color reproduction on this monitor. It made such a difference that this experiment went from a borderline success to
a complete success. It has made the monitor usable for long periods of time for development.

## Conclusions

Overall I'm really happy with the purchase and would definitely do it again. When working on a complex issue it is a huge help to be able to have more space to view the different files.
It reduces scrolling, application switching and file switching. Though this monitor probably wont make you a more productive developer, as the slowest part of development is
the human mind. It will make the time which you spend inside code much more enjoyable.

I'd definitely recommend it to anyone that is considering taking the 4k dive.

{% img /images/posts/4kp/new.JPG 600 auto %}

Excuse the mess


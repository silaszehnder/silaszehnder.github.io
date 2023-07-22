---
layout: post
title: "Rooting the Onyx Boox Nova Air (fw v3.3.1), and e-ink asides"
categories: tech
date: 2023-03-30
---

There are a few threads and [blog posts](
https://blog.tho.ms/hacks/2021/03/27/hacking-onyx-boox-note-air.html) online about
rooting Boox products, but I thought I'd share my own experience with the latest
firmware as it was slightly involved due to the fact that Onyx has yet to post firmware
download links on their site. A lot of credit goes to Tho85 as their post linked above
set the groundwork for my experience. See this post of mine as a "spritual successor" to
theirs.

----------------------------------------------------------------------------------------

As expected, upgrading to 3.3.1 removed root on my Nova Air. Unexpectedly, the upgrade
rendered my tablet completely useless as I ran into `ContentBrowser keeps stopping`
messages on startup when using the Onyx Launcher as my home app. I could boot
successfully into a different launcher, but attempting to open apps like Notes (which
are embedded and run within the Onyx Launcher itself) consistently failed with that
message. Google only turned up one search result for this error, which was just a
[reddit thread](
https://www.reddit.com/r/Onyx_Boox/comments/z5qheh/factory_reset_nova_air/) suggesting a
factory reset. So I went ahead and did that. Luckily, I had created a backup of all my
notes before the upgrade, and regardless of the launcher issues was still able to use
USB debugging to `adb pull` other files I wanted to save before the reset.

## Rooting

### Getting a boot.img

Typically, this `boot.img` can be retrieved by following the `Decrypt firmware updates`
section of [Tho85's blog post](
https://blog.tho.ms/hacks/2021/03/27/hacking-onyx-boox-note-air.html), but I was unable
to do this since Onyx hasn't yet posted 3.3.x firmware download links on their site.
Instead, I needed to follow `Boot into Emergency Download (EDL) 9008 mode`, which went
something like this:

- Set up [Qualcomm Sahara / Firehose Attack Client / Diag Tools](
  https://github.com/bkerler/edl) by following their installation guide
- Reboot the tablet into EDL 9008 mode: `adb reboot edl`
- Grab the boot partition from the tablet:
  `python edl --loader=Loaders/prog_emmc_ufs_firehose_Sdm636_ddr.elf r boot boot.img --memory emmc`
  - Note `--memory emmc`. I think that the default behavior of this tool has changed
    since Tho85's post, as their commands didn't specify the usage of this argument.
  - Note for Nova Air 2 users: I had to use
    `0014d0e100000000_d40eee56f3194665_FHPRG.bin` instead as the Loader, and the
    partition was `boot_a` rather than `boot`.
  - Note for pyenv users: I ran into libusb issues due to pyenv expecting it to exist
    somewhere that it didn't. Following [this suggestion in a GitHub issue thread](
    https://github.com/pyusb/pyusb/issues/355#issuecomment-974726078) (running
    `sudo ln -s /opt/homebrew/lib/libusb-1.0.0.dylib /usr/local/lib/libusb.dylib`)
    solved this issue.

### Patching the boot.img

- magisk root
  - copy boot.img over to the tablet, run install
  - copy patch over to laptop
  - `adb reboot fastboot`
  - `fastboot boot magisk_patched*.img`
    - Note: On a Nova Air 2, I had to hop into `fastboot reboot bootloader` first in
      order for the `fastboot boot` command to be recognized.
  - confirmed the patched boot image worked
  - `fastboot flash boot magisk_patched*.img`
  - `fastboot reboot`

## Configuring

- Install AFWall+:
  - Disable network access for everything, then approve it for the apps and services I
    actually want to use. I have nearly all Onyx-related apps/services disabled.
  - _Why?_ I saw some requests being sent to Tencent IPs, which are most likely
    harmless, but I'd prefer to play it safe. Boox isn't transparent about what all is
    running on their tablets. On the other hand of transparency, their public [sdks](
    https://github.com/onyx-intl/OnyxAndroidDemo) have resulted in some [interesting
    tweaks](
    http://bbs.onyx-international.com/t/feature-request-pipe-dream-no-pen-lag-for-3rd-party-note-apps/1942/10)
    to exsiting applications to better support low latency e-ink writing in apps that
    don't already account for this use case.
- Install `a decluttered launcher`
- Set up notes to backup to Google Drive:
  - Within notes settings, enable saving to pdf on exit
  - Install `Autosync for Google Drive` and configure it to watch the `/note` directory

----------------------------------------------------------------------------------------

## Asides

### Why the Nova Air?

I used to have an iPad that I used almost exclusively as a Notability machine in
college, which was easily the best tablet note taking experience I've ever had. However,
after college it simply didn't get much use. Writing grocery lists and to-do lists for
chores on a > $1000 device felt like a waste, so I handed it off to my sister for her to
use for the remainder of her undergrad and grad school.

A few months after getting rid of the iPad, there were a few rare occasions where I
found myself missing the ability to jot down quick notes/diagrams that could be shared
electronically. I tried using the markup feature within the Notes app on my iPhone to
scribble down diagrams, but that was no good.

I happened to be in the market for a new laptop, so I went with the ThinkPad X1 Tablet
gen 3 to try and scratch the note taking itch. However, the pen's build quality and the
ergonomics of a Surface-like laptop just didn't work out for me really. I ended up
almost never using the pen or the touchscreen of this device, and its speakers stopped
working one day. Definitely a bit of a bummer of a laptop for my purposes.

I started looking into devices like reMarkable since that seemed like a great product
for my use case: e-ink display, wouldn't need to be charged frequently, and note taking
is the device's main feature. But I immediately lost interest when I saw how restricted
the OS was, as well as the fact that some features seemed to be locked behind a
subscription. At this point, I realized that all I really wanted was an e-ink Android
tablet with low-latency stylus input. I found the Nova, and that was that. It's been
great so far!

### The future

E-ink tablets, and e-ink in general, seems to be gaining traction in the US recently.
[Lenovo Smart Paper](
https://news.lenovo.com/pressroom/press-releases/dual-screen-yoga-book-9i-premium-consumer-devices-innovation-unexpected/)
is an example of a big company investing in this sector in the US. That being said, I am
still anxiously awaiting a pure Android e-ink tablet that doesn't include a proprietary
OS wrapper like so many of the current devices on the market have, the Smart Paper
included.

Do you know of any options on the market that provide a pure Android/Linux experience?
I'm keeping tabs on the [PineNote](https://www.pine64.org/pinenote/), but it is not in a
day-to-day usable state just yet. That is honestly my frontrunner at the moment. For the
next few years though, I'll stick with the Nova Air.

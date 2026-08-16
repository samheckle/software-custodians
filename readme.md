# Soft(ware) Custodians Workshop

## Required Tools

- Computer
  - Mac: OK
  - Linux: Some issues depending on your OS, good luck!
  - Windows: Iffy, might need more research!
- iDevice: iPod, iPhone, iPad
- Cable
  - Usually need USB-A to lightning or 10-prong. 

This is specific to iOS, but if you are looking for Android check the [extra resources below](#android-and-alternative-os)

## Before We Begin

1. Plug in your device if it is not charged already
2. Open this repo to follow along: https://github.com/samheckle/software-custodians
   
![github](/images/qrcode_github.com.png)

Zine!!
- [download the digital version](/zines/hope26-digital.pdf)
- [download the print version](/zines/hope26-print.pdf)

Thanks to Antonia (@slow.circuits) and Imani (@y2kbug.zip) for the amazing design and collaboration :))))

## Agenda

1. Who Am I (+ charge your devices)
2. Discussion: Outline Jailbreaking and Permacomputing
3. Identify Devices (and people) in the room
4. Set Up Devices for Jailbreaking
5. Jail! Break!
6. Repurposing
7. Other projects and references

## Who Am I (+ charge your devices!)

sam heckle (they/she)

- artist & educator based in nyc
- teach creative coding and full-stack web dev
- run an artist collective called [Destruction Junket](https://destructionjunket.com/)
- love https://nyc.permacomputing.net/
- maintainer of https://l5lua.org/ , a creative coding library

https://samheckle.com/  
https://bsky.app/profile/smarmy.space  
https://www.instagram.com/semantic.lol/  
(fediverse but only lurking for L5: @L5@tldr.nettime.org)  

This is a distillation of research that stemmed from the question:

**"How do I run a self-hosted website from my childhood iPod Touch?"**

## Discussion: Outline Jailbreaking and Permacomputing

I am only building on those who came before me:

- [Compile C Applications with GCC on iOS 4](https://blog.syshalt.net/index.php/2010/09/12/compile-c-applications-with-gcc-on-ios-4-iphone/) from Sergiu, 2010
- [Homebrew iOS](https://web.archive.org/web/20230119142632/https://wiki.secondlife.com/wiki/Homebrew_iOS) - Kira Komarov, 2012
- https://ios.cfw.guide/
     - This is my source of truth and a lot of the info is pulled from here. 

### What is jailbreaking?

Allows you to modify an iOS device to enable higher customization and mods. Since iOS historically hides the operating system and code as a way to "make a device easy to use", a lot of the system is locked away behind proprietary design.

<img src="/images/file-systems.png" style="width: 600px;">

### Levels of Abstraction

Apple created [Darwin](https://en.wikipedia.org/wiki/Darwin_(operating_system)), the base operating system for *all* Apple devices (computers, phones, tablets and tvs). By jailbreaking, we removing the abstraction (and intenional hiding) of the core OS interface. 

<img src="/images/abstraction.png" style="width: 400px;">

### Why would you jailbreak?

Through jailbreaking, we can effectively access the console on a device and make it do pretty much any task.

Oftentimes, people jailbreak to customize themes, change iOS version, install "tweaks" (the iOS term for mods), and access some type of package manager.

The goal of this workshop is to increase your familiarity with your devices by breaking the walled garden and accessing the native command-line interface on each device, instead of relying on proprietary Apple services for everything. 

### On Legality

Under the DMCA (Section 1201 of Title 17):

> unlawful to circumvent technological measures used to prevent unauthorized access to copyrighted works

HOWEVER, jailbreaking falls under an excemption passed in 2012 that allows modifications of smartphones. This execemption is reviewed every 3 years with petitioners to verify if the execemption is still needed. In 2015, the excemption was passed on to any all-purpose computing device (like tablets). This was renewed most recently [in 2024](https://www.federalregister.gov/d/2024-24563/p-79).

For example, here is an execerpt of [EFF's petition](https://www.eff.org/2012-DMCA-Exemption-Requests#Phones)

<img src="/images/dcma.png" style="width: 600px;">

**_But_**, jailbreaking does void the warranty!

### Permacomputing

Permacomputing is a term for "resilience and regenerativity in computer and network technology inspired by permaculture" (https://permacomputing.net/). By being in this room, you are already adhering to this philosophy.

From permaculture, the three core tenents are Earth Care, People Care, and Fair Share. Building permacomputing tenents from that: "a comprehensive approach to the design of human technology, taking into account social and ecological issues, encouraging resilience and supporting a fair coexistence".

By breathing life into these old devices, we are resisting e-waste and recycling them into our own artistic practices.

A website I found during my research that looks pretty awesome: https://suckless.org/rocks/

## Identify Devices (and people) in the room

1. Identify iOS version
   - https://ios.cfw.guide/get-started/
   - Search model number `Settings → General → About`
   - Find the device specs on wikipedia
2. Identify which jailbreaking tool that works for your version
   - iOS pre `v9`: https://github.com/LukeZGD/Legacy-iOS-Kit
   - iOS `12-12.8.7`: https://chimera.coolstar.org/
        - need PlumeImpactor as well: https://github.com/CLARATION/Impactor/releases/tag/v2.2.3
   - iOS `15-16.6.1`: https://ellekit.space/dopamine/
   - iPod Nano (except 6G): https://github.com/freemyipod/wInd3x?tab=readme-ov-file#wind3x
3. Connect your device to wifi
   - This will probably require a hotspot!
4. Run through the jailbreaking process
   - Even though this is the title of the workshop, this is actually the easiest part
   - As per the instructions on whichever too

## Post-Jailbreak

### Package managers

A package manager in the context of a jailbreak means you are using an interface to install applications and libraries. It can kind of be seen as the App Store + `apt` (but we have to install `apt` from the package manager)

There are a few package managers out there:

- Cydia
- Sileo
- Zebra

Each package manager requests data from a repository, which we will get into after we jailbreak our devices.

### Repositories

So now we have our jailbreaks, we can access these different repositories that retrieve different binaries for our Darwin devices.

Depending on your device, you might have access to `http` OR `https`. If you find you are running a device that is too old, download updates `https` certificates: https://tlsroot.litten.ca/

One important repository:

- http://apt.thebigboss.org/repofiles/cydia/

A resource for finding repositories:

- https://www.ios-repo-updates.com/repositories/

### Installing Dev Tools

Open up your package manager (Cydia, Sileo, or Zebra).

#### Suggested Packages to Install

Recommended for everyone:
- BigBoss Recommended Tools (includes OpenSSH, python, libcc and many useful dev tools)

Cydia:
- Mobile Terminal

Sileo / Zebra:
- MTerminal

#### What is Terminal?

Terminal is an application on Apple devices that gives users text-based access to the operating system (Darwin). Prior to 2017 (iOS 11), there was no way for mobile and tablet users to be able access the files on their devices, whereas Terminal.app is pre-installed on MacOS. 

Installing Mobile Terminal/MTerminal for mobile allows us to bypass the GUI provided by Apple. 

#### Common Issues 

- If your device is `>4.3` but you are having `https` issues, you might need to install some certificates: https://tlsroot.litten.ca/
- If you are having issues connecting to Cydia after installing certificates: you might need to `Update DateTime` in the menu.
- If you are using Sileo, you may need to update the packages first.

## Opening Terminal

This can be done either on the device or using SSH from your computer. If from your computer, make sure your device + computer are connected to the same wifi network (will likely need to be a hotspot), then `ssh root@{your-ip-address}`. You can retrieve this by checking your wifi advanced settings. The standard root password is usually `alpine`.

At this point, this tutorial diverges. When writing this tutorial, I used an iPod Touch 2 running `4.2.1`, but testing on other devices the system doesn't quite do the same thing.

### Using Legacy iOS Kit

My iPod is quite slow with typing and I find it easier to connect to it with SSH on my computer. You can do this from Legacy iOS Kit by opeing `Main Menu → Data Management → Connect to SSH`

From there, let's check our operating system we are working with.

We can see the name of the system with

```sh
uname
```

and the version

```sh
sysctl kern.version
```

**_What is `Darwin`?_** : https://en.wikipedia.org/wiki/Darwin_(operating_system)  
Key phrase "unix-like"


### Running a Webserver

Let's update the packages we can use with `apt-get`

```sh
apt-get update
```

We can install pretty much any library we want

```sh
apt-get install python
```

Ensure python is installed

```sh
python --version
```

It should already be installed through BigBoss Recommended Tools, but you could install it through your package manager or by typing:

```sh
apt-get install python
```

And we can run _a_ server using

```sh
python -m SimpleHTTPServer 8000
```

Which you can access if you and the iDevice are both connected to the same local network. 

#### Using a daemon instead

BUT this doesn't necessarily keep our server running. So let's install C :)

#### Install C

From [this guy](https://blog.syshalt.net/index.php/2010/09/12/compile-c-applications-with-gcc-on-ios-4-iphone/) - Sergiu, 2010

Bless him for keeping his files both `http` AND still hosting 16 years later. If these files for some reason don't work, I have made a backup in the [gcc-archive](/gcc-archive/) folder of this repository. 

1. `wget http://www.syshalt.net/pub/iphone/gcc-iphone/fake-libgcc_1.0_iphoneos-arm.deb`
2. `dpkg –i fake-libgcc_1.0_iphoneos-arm.deb`
   a. for iOS `>7` 
      - `wget http://www.syshalt.net/iphone/gcc-iphone/iphone-gcc_4.2-20080604-1-8p_iphoneos-arm.deb` 
      - `dpkg -i iphone-gcc_4.2-20080604-1-8p_iphoneos-arm.deb`
3. `apt-get install iphone-gcc`
4. `wget http://www.syshalt.net/iphone/gcc-iphone/sdk-2.0-headers.tar.gz`
5. `tar -xvzf sdk-2.0-headers.tar.gz`
6. `cd include-2.0-sdk-ready-for-iphone`
7. `cp –r * /usr/include`
8. `cd ..`
9. `wget http://www.syshalt.net/iphone/gcc-iphone/gcc_files.tar.gz`
10. `tar -xvzf gcc_files.tar.gz`
11. `cd gcc_files`
12. `cp –r * /usr/lib`

#### C-based http server daemon

I'm outsourcing this, I'm tired. 

1. Clone or download https://github.com/emikulic/darkhttpd
2. Create a folder (usually `www`) to run your `html` files. 
3. `./darkhttpd ./www/`

And so, I answered my question: **"Yes you can run a website from an iPod Touch"**

<img src="/images/running.PNG" style="width: 600px;">

*Screenshot of texting my partner*

## Other jailbreaking projects:

- [this guy](https://www.reddit.com/r/jailbreak/comments/5mzr0b/release_nginx_and_lsof_for_ios/) compiled nginx for iOS `> v7` 
   - this was my original goal (and was outlined in the original secondlife wiki but I was unable to do so)
- https://www.reddit.com/r/jailbreak/comments/ezyznx/tutorial_running_a_minecraft_server_on_ios_1331/

## Special thanks to these resources

- https://freemyipod.org/wiki/Main_Page
- https://q3k.org/wInd3x.html
- https://destinybox.blogspot.com/2013/05/nan0hail-12-download.html
- https://theapplewiki.com/wiki/Up_to_Speed
- https://www.reddit.com/r/jailbreak/
- https://www.reddit.com/r/LegacyJailbreak/

Some other useful resources:

- [Opportunities and Challenges in Securely Reusing and Repurposing Mobile Devices](https://arxiv.org/pdf/2606.06181)

## Android and alternative OS
- [resources for Radical Infrastructures, Permacomputing, Stealth Hosting and Other Networks](https://miriamreynoldson.com/2026/06/08/resources-for-radical-infrastructures-permacomputing-stealth-hosting-and-other-networks/) - zine on jailbreaking android devices starting on page 17
- Clara Rigaud reusing android devices as modular synths: [Zombitron](https://clararigaud.com/zombitron/)
- Wilderland workshop on [jailbreaking android devices](https://wilderland.ie/pages/permacomputing-workshop2-repurposing-smartphones.html)

### Postmarket
- [postmarketOS on apple devices](https://wiki.postmarketos.org/wiki/Apple_iPhone_6_(apple-n61))

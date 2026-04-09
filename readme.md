# Soft(ware) Custodians Workshop

## Required Tools

- Computer
- iDevice: iPod, iPhone, iPad
- Cable

## Agenda

1. Discussion: Outline Jailbreaking and Permacomputing
2. Identify Devices (and people) in the room
3. Set Up Devices for Jailbreaking
4. Jail! Break!
5. Repurposing
6. Other projects and references

## Discussion: Outline Jailbreaking and Permacomputing

I am only building on those who came before me:

- [Compile C Applications with GCC on iOS 4](https://blog.syshalt.net/index.php/2010/09/12/compile-c-applications-with-gcc-on-ios-4-iphone/) from Sergiu, 2010
- [Homebrew iOS](https://web.archive.org/web/20230119142632/https://wiki.secondlife.com/wiki/Homebrew_iOS) - Kira Komarov, 2012
- https://ios.cfw.guide/

### What is jailbreaking?

Allows you to modify an iOS device to enable higher customization and mods. Since iOS historically hides the operating system and code as a way to "make a device easy to use", a lot of the system is locked away behind proprietary design.

<img src="/images/file-systems.png" style="width: 600px;">

### On Legality

Under the DCMA (Section 1201 of Title 17):

> unlawful to circumvent technological measures used to prevent unauthorized access to copyrighted works

HOWEVER, jailbreaking falls under an excemption passed in 2012 that allows modifications of smartphones. This execemption is reviewed every 3 years with petitioners to verify if the execemption is still needed. In 2015, the excemption was passed on to any all-purpose computing device (like tablets). This was renewed most recently [in 2024](https://www.federalregister.gov/d/2024-24563/p-79).

For example, here is an execerpt of [EFF's petition](https://www.eff.org/2012-DMCA-Exemption-Requests#Phones)

<img src="/images/dcma.png" style="width: 600px;">

**_But_**, jailbreaking does void the warranty!

### Why would you jailbreak?

Through jailbreaking, we can effectively access the console on a device and make it do pretty much any task.

Oftentimes, people jailbreak to customize themes, change iOS version, install "tweaks" (the iOS term for mods), and access some type of package manager.

### Package managers

A package manager in the context of a jailbreak means you are using an interface to install applications and libraries. It can kind of be seen as the App Store + `apt` (but we have to install `apt` from the package manager)

There are a few package managers out there:

- Cydia
- Sileo
- Zebra

Each package manager requests data from a repository, which we will get into after we jailbreak our devices.

### Permacomputing

Permacomputing is a term for "resilience and regenerativity in computer and network technology inspired by permaculture" (https://permacomputing.net/). By being in this room (and attending this specific Electronic Faire), you are already adhering to this philosophy.

From permaculture, the three core tenents are Earth Care, People Care, and Fair Share.
Building permacomputing tenents from that: "a comprehensive approach to the design of human technology, taking into account social and ecological issues, encouraging resilience and supporting a fair coexistence".

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

Depending on your device, you will need to install different tools

All devices:

- OpenSSH
- MobileTerminal

Cydia (pre `v9`)

- BigBoss Recommended Tools

Sileo (post `v10`)

- update packages
- fakelibgcc

### Repositories

So now we have our jailbreaks, we can access these different repositories that retrieve different binaries for our Darwin devices.

Depending on your device, you might have access to `http` OR `https`.

One important repository:

- http://apt.thebigboss.org/repofiles/cydia/

A resource for finding repositories:

- https://www.ios-repo-updates.com/repositories/

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

Next, lets update the packages we can use with `apt-get`

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

And we can run _a_ server using

```sh
python -m SimpleHTTPServer 8000
```

BUT this doesn't necessarily keep our server running. So let's install C :)

From [this guy](https://blog.syshalt.net/index.php/2010/09/12/compile-c-applications-with-gcc-on-ios-4-iphone/) - Sergiu, 2010

Bless him for keeping his files both `http` AND still hosting 16 years later.

1. `wget http://www.syshalt.net/pub/iphone/gcc-iphone/fake-libgcc_1.0_iphoneos-arm.deb`
2. `dpkg –i fake-libgcc_1.0_iphoneos-arm.deb`
   a. for iOS `>7` - `wget http://www.syshalt.net/iphone/gcc-iphone/iphone-gcc_4.2-20080604-1-8p_iphoneos-arm.deb` - `dpkg -i iphone-gcc_4.2-20080604-1-8p_iphoneos-arm.deb`
   4.2 dpkg -i iphone-gcc_4.2-20080604-1-8p_iphoneos-arm.deb
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

Finally,

Clone or download https://github.com/emikulic/darkhttpd to run a server!

Other points of interest:

- [this guy](https://www.reddit.com/r/jailbreak/comments/5mzr0b/release_nginx_and_lsof_for_ios/) compiled nginx for iOS `> v7`
- https://www.reddit.com/r/jailbreak/comments/ezyznx/tutorial_running_a_minecraft_server_on_ios_1331/

Special thanks to these resources

- https://freemyipod.org/wiki/Main_Page
- https://q3k.org/wInd3x.html
- https://destinybox.blogspot.com/2013/05/nan0hail-12-download.html
- https://theapplewiki.com/wiki/Up_to_Speed
- https://www.reddit.com/r/jailbreak/
- https://www.reddit.com/r/LegacyJailbreak/

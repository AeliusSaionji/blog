In this post I'll just be explaining each and every extension in this list. Many of these extensions are not for the faint of heart- the price of the added privacy and security is that most websites will simply stop working until you add rule exceptions that allow them to work again. Many sites rely on multiple components to work properly and will require multiple rules from multiple extensions, so it is best to have a working understanding of each of these extensions if you wish to start using them.

<!-- more -->

I am not an expert, and this list is entirely of my own making. If someone more knowledgeable than me spots something missing or otherwise incorrect in this post, please let me know via the disqus comments on the blog page.

Not all of these extensions are just for security- some of them are just functionality I'd like to have in a browser. I'm including everything that I use in this list.

I will update this post as my setup evolves. The post is subject to change, so I urge you to save a local copy of this page if you want to preserve it as it is now (use MAF as suggested below!).

* * *

The first tool is of course, Firefox. Firefox certainly is not the only browser capable of these things- if you use linux, there are browsers like vimprobable, xombrero, dwb, that have some of the following security ideas built right in. Outside of linux though, Firefox is the only option I know of. Neither chrome, internet explorer, safari, maxthon, opera, or any other common (or uncommon) browser is capable of doing all of the below. Chrome users, yes I know a lot of the security extensions exist in the Chrome plugin catalog, however... Chrome, at the time of writing, just does not give extensions enough control over the browser to achieve the desired functionality. Chrome has a variant of Noscript that isn't as effective as the Firefox version, RequestPolicy simply can't be done, and even Adblockplus only hides ads, it doesn't block your connection to the ad server (like the Firefox version does). If this changes in the future, do let me know- but at the moment Chrome is simply inferior if you desire this level of control over your browser.

The list, in alphabetical order:

<https://addons.mozilla.org/en-US/firefox/collections/LinkSatonaka/ps/?sort=name>

* Auto Private
> Requires the extension Private Tab to work properly (without it, links that should be private opened in a new tab will not be private. It ideally should force private URLs to be opened in a new private window). This is fairly self explanatory- you specify that you want certain domains to always be loaded in private mode. All settings are done via about:config

* Clean Links
> Aggressively cleans URLs into a their pure form- this circumvents certain forms of tracking and URL redirects. You will need to add exceptions for several legitimate sites. By default facebook, twitter and google plus are in the exclusion list- I don't use those services so I don't know what will happen if you remove the exceptions... but I know that facebook in particular captures EVERY URL you click so it really should not be an excluded domain. Go into the config and remove it. The option "remove from links" seems to be exactly what the Pure URL extension does. I'm not confident in my RegEx, but I attempted to take all of Pure URL's rules and put them in Clean Links. The following appears to work just fine.
>
> Remove From Links:
> (?:ref|aff)\w*|utm_\w+|ga_\w+|fb_\w+|(?:merchant|programme|media|collection_)ID|action_(?:object|type|ref)_map|hc_location|yclid|_openstat|src
>
> I have the following options checked:
> * Event delegation mode
> * CopyLink Controller
> * Use HTTP Observer
> * Link Tracking

* Context Menu Image Saver
> I save a lot of pictures. This lets you save pictures directly into predefined folders. Ctrl+RClick on a picture to save it to the folder you last saved to.
>
> ![image](https://68.media.tumblr.com/a3c3c8a410e39b8c482eb6b24b163f63/tumblr_inline_nkzihvY2C71rl1tfe.png)

* Distill
> Monitor web pages that don't provide rss feeds or email alerts.

* DownThemAll
> You probably already know about this one.

* FlashGot
> With this, you can configure any program to open a download. I don't usually have adobe flash installed, so I use this to tell my video player to open videos as streams (as opposed to the firefox default: download the entire video then open the file with the selected program).

* Greasemonkey
> Find most scripts at <https://greasyfork.org/en>

* HackTheWeb
> Allows you to alter the way a page looks and save it as a Stylish script. Currently saving changes is broken, but it is my second choice after 'yet another remove it permanently'.

* Image Forward
> For sites like 4chan, or any site where you might want to view all images embedded or linked in a page in a sequential slideshow. It simply views the images with Firefox, nothing special. Lets you configure any file extension, too, so you can seamlessly create slideshows including not just images, but webms, mp4s, txt files.... anything. Automatic advance is not a built in feature; you have to use setInterval(). I have the code bound to a key combination with the help of pentadactyl. Here's the js code: <http://sprunge.us/YfEc>. This extension is incompatible with 'yet another remove it permanently' in that some of Firefox's keyboard shortcuts will stop working if both are installed.

* Karma Blocker
> This one is a little redundant, since the latest beta of RequestPolicy (only available on github) FINALLY has a blacklist in addition to a whitelist. However, I don't think I'll be getting rid of Karma Blocker because it has such a wonderful interface which both educated me on some of the underlying systems of the browser, and also makes it easier to fine tune what connections you want to always allow / deny. Also, if you're feeling lazy and just "temporarily allow all" with RequestPolicy on a site because you'll probably never go there again, the default rules for karma blocker will still offer you a bit of protection. A little redundancy is sometimes good to have.

* LastPass
> This needs a lot of work, but it's serviceable. I chose LastPass over all the alternatives because it supports biometrics- you can  use a fingerprint scanner to log into websites. I have it configured to  ask me for my fingerprint every time I log into a site. My cookies are cleared when Firefox closes. A good balance of security and convenience. My fingerprint scanner was 20USD on amazon.

* Minimize on Start and Close
> Don't accidentally close firefox!

* Mozilla Archive Format
> This is the best way to save a webpage that I know of. Don't take a picture of the page, don't convert it to pdf- save the page as maff. You'll thank me later.

* NoScript
> Selectively allow javascript to run on pages you specify (and selectively allow javascript loaded from other domains).
> 
> You probably already know of this one, since you're looking through a list of primarily security related extensions. What you probably don't know is that it covers a lot of browser exploits even when you have it set to "globally allow all scripts". Everyone really should install this, even if they don't use the script blocking feature. If you do use script blocking, there is support for syncing rules over Firefox sync hidden away in `about:config`. Also features the ability to force specified domains to use HTTPS
>
> ![image](https://68.media.tumblr.com/e39ca26977c1da064dab22babcd5e4c0/tumblr_inline_nkzj04TVI21rl1tfe.png)

* OpenDownload²
> Saves downloads to a temporary folder and launches them automatically when they finish downloading.
>
> ![image](https://68.media.tumblr.com/767428524d7a5bed6c27de57e01edc15/tumblr_inline_nkzj83gGp11rl1tfe.png)

* Pentadactyl
> This is where the meat is. Not just a vi-inspired keyboard layout, but an entire control system where the only limitation is your knowledge of JS and your creativity. I do most of my GUI customization with pentadactyl. Get the nightly version from their site. At the time of writing pentadactyl enforces a default maximum tab height, which you will have to undo in your config file if you want to use vertical tabs (<http://sprunge.us/MZEZ>). A notable feature of pentadactyl is cookie management, which is why I don't have any cookie control extensions in this list.
>
> This extension is really, really involved, so it might take a lot of time to get into. I should write a post going over the basics...

* Private Tab
> I have no particular need for this, but as mentioned the extension 'Auto Private' doesn't work right without it.

* QrCodeR
> One of the few QR code generators that is offline, so it doesn't contact googleapis (eg won't track you), it won't be blocked by RequestPolicy... it'll just work. Like it should.

* RefControl
> Every time you click a link, the new websites knows where you came from by way of the referrer. This extension blocks referrers, and allows you to whitelist certain sites that actually rely on referrers to function.

* RequestPolicy
> This prevents a site from accessing resources from other sites. For example, if tumblr.com tries to show you a picture that is hosted on imgur.com, RequestPolicy will block it. Why is this useful? It speeds up the loading of pages by cutting out anything unnecessary (but you can always create a rule that allows tumblr, or any site, to access imgur!). It stops other sites from tracking you. If we keep using the imgur example: when your browser accesses the picture hosted on imgur, it tells imgur what webpage you're currently viewing, and of course your IP address. Imgur will know which specific page you've been to on tumblr. You know how many sites have a "share to twitter/Facebook" gadget? That gadget contacts Facebook and twitter whether you click on it or not. Facebook knows what sites you have been to. You don't have to be logged into Facebook, they know who you are by your cookies and other identifying information, and you had better believe Facebook is collecting and storing any data they can get on you. Many other companies besides Facebook do this. With RequestPolicy, the site you visit is the ONLY site you touch, and YOU decide what resources that site is allowed to connect to on your behalf. In using RequestPolicy, what companies each site tries to connect to will be revealed to you quite plainly.
> 
> Between this, Noscript, Karma Blocker, and HackTheWeb, there is absolutely no reason to have any sort of adblock installed. Adblockers are bloated and WILL slow down Firefox- they contain HUGE rulesets that take up a lot of memory. RequestPolicy simply blocks everything unless you say otherwise, so poof, ads are gone. All of the previously mentioned extensions are lightweight and cover all the functionality of an adblocker (well, unless the ad is locally hosted and just displayed as a normal picture- I've seen this exactly once).
> 
> Set RequestPolicy to default-deny mode and begin the long, slow process of adding exceptions to unbreak all of the sites you regularly visit. This version seems to have been abandoned, but someone else has continued development at <https://requestpolicycontinued.github.io>. That one is not compatible with the 'RequestPolicy Sync' extension, which is why that extension is no longer featured here.
>
> ![image](https://68.media.tumblr.com/86e75dc20c7f90d63c3cc517fef67e39/tumblr_inline_nkziwfNEmX1rl1tfe.png)

* Session Manager
> More reliable and more configurable than the internal session manager.

* Stylish
> Honestly redundant, since pentadactyl has a command that applies style sheets. However, stylish has a repository where the author of a stylesheet can create updates and you'll automatically get them- something pentadactyl does not have. I use pentadactyl to apply simple things, like hiding the close buttons on tabs, and I use stylish for more advanced things, like changing the layout and colorscheme of a website. The ability to get stylesheet updates for constantly changing websites is also a plus.

* Stylish Sync
> Sync your style sheets over Firefox sync. The sync is independent of the stylish repository- you can make your own custom sheets and they'll be synced over your profile.

* Tab Scope
> It comes in handy if I have more than 10 tabs of pictures with ambiguous names and I want to find a specific one, but other than that it's unnecessary eye candy.
>
> The developer of tab scope actually emailed me a one line tweak for pentadactyl's source code that makes pentadactyl ignore tab scope (by default it is seen as 'menu' mode). Instructions here: <http://sprunge.us/PTJZ>
>
> ![image](https://68.media.tumblr.com/9cfc51eb54180289b02fe77266209fd9/tumblr_inline_nkzipxFRDR1rl1tfe.png)

* Tile Tabs
> I have this installed because it works fairly well with pentadactyl, and works well in general (not all of these types of extensions do). I might keep it, I might not. Update: I do find this useful for viewing multiple tabs at once (an occasional necessity). It's much faster than making a new window since Firefox is slow to initialize and draw windows, and a simple vertical split from Tile Tabs is instant. I do feel that this extension is rather over encumbered with options, and so I  have disabled just about every feature, menu entry, and shortcut except for: ctrl+drag tab/link, double-click tab new/close layout, ctrl+shift+arrowkey navigation, F12 new/close layout.

* Tree Style Tab
> Why are tabs not vertical by default? It might look strange to you at first, but vertical tabs are pretty objectively better, especially since monitors are widescreen. Ignoring the fact that widescreen websites never caught on in the first place, more and more websites are becoming even skinnier by catering to portrait oriented phones! You're wasting so much screen real estate by not using vertical tabs. Start using them now. You'll actually be able to read the tab title, you'll be able to see 50 tabs at once instead of just 8, and with this particular extension, tabs can be indented under the above tab if that site came from the above tab. Dramatically improves tab readability and navigation.
>
> ![image](https://68.media.tumblr.com/edbcb0b2ab32038487c419ed84ccedaf/tumblr_inline_nkzhydSksj1rl1tfe.png)

* UnloadTab
> This one dims tabs that are not loaded in memory so you can visually identify them (pictured above). You can right click any tab and click unload, you can have this extension unload tabs that have not been accessed in x seconds, and you can specify a whitelist of domains that are never unloaded.

* * *

## Greasemonkey Scripts

* [Download YouTube Captions](https://greasyfork.org/en/scripts/505-download-youtube-captions)
> Seems to be broken at the moment. Would let you download the subtitle files for a video.

* [LinkTube](http://isebaro.com/)
> Removes embedded YouTube players in sites and replaces them with a link to the YouTube video page. This prevents websites from slowing down when they're trying to access a video you didn't even want to see... and having a direct link to the video is what I want 9 out of 10 times.

* [Mouseover Popup Image Viewer](https://greasyfork.org/en/scripts/404-mouseover-popup-image-viewer)
> Finds the fullsize image and displays it when you hover your mouse over a thumbnail on any page.

* [Pixiv Direct Links](https://greasyfork.org/en/scripts/4555-pixiv-direct-links)
> This just gives you the direct image URL on pixiv servers for easy saving. However, this direct URL cannot be shared with other people- they'll get an access denied error. You can only share the regular page the picture is normally presented on.

* [Smooth Scroll](http://sprunge.us/TPYW)
> If you click a category URL on a Wikipedia page, normally your browser will just jump to the part of the page the category refers to. This script makes it scroll there, which helps quantify/visualize page navigation. This applies to any website with URLs that refer to a location within the same page, not just Wikipedia. Original host is down so I've rehosted the script.

* [Ugoira2GIF](https://greasyfork.org/en/scripts/6534-ugoira2gif)
> Another Pixiv tool, allows you to make and save GIFs of Pixiv's proprietary animated images.

* [ViewTube](http://isebaro.com/)
> Replaces YouTube's video player with an always HTML5 version that ignores age restrictions, doesn't show ads, allows for easy video downloading, and is generally faster, lighter, and better. If you don't want to install Adobe Flash, this and all its derivatives are your friends. Does not support 3D vision videos, nor captions. I personally couldn't be happier that captions don't work, I find them annoying and spammy 90% of the time. DASH playback is supported but doesn't work very well, I keep it disabled unless I want to download the highest quality video.
>
> ![image](https://68.media.tumblr.com/6cfe65217707d49236503d85ca77fae6/tumblr_inline_nkzje2ESCB1rl1tfe.png)

* [ViewTube+](http://isebaro.com/)
> ViewTube for several other video sharing sites.

* [ViewTubePlus](https://heliotropium.it/ViewTubePlus.user.js)
> ViewTube for adult (porn) sites.

* [Webm Looper](https://github.com/WhatIsThisImNotGoodWithComputers/webm-looper-userscript)
> Webm is the new GIF. Make your browser loop them like GIFs.

* * *

## Update - 15/05/26

I created a new firefox profile and was impressed with how light the newest Firefox can be. In an attempt to keep it light, I’ve dug deep and really pruned my extensions, relying on external software where possible. The following are what I now have installed:

* Flashgot - grabbing videos where youtube-dl cannot.
* Greasemonkey - Pretty much all above scripts are absolutely necessary
* Lastpass - gotta have passwords
* Mozilla archive format - I save pages infrequently, but I want to be able to open what I have saved
* Noscript - security

* OpenDownload² - I don’t want my downloads folder getting cluttered
* Pentadactyl - still doing most of the heavy lifting
* Pure URL- security
* Referrer Control - security (trying a different one on for size)

* Request Policy - security
* Session Manager - I don’t trust Firefox’s internal session management
* Stylish, Stylish sync - because that Wikipedia theme is too sexy

I am trying to rely entirely on pentadactyl’s buffer interface for tab management, so I’ve removed all tab related extensions. I’ll continue to update this post as I inevitably cave and add more functionality.

## Update - 15/08/10

Not many changes to the formula, though I don’t know if the reason is I’m used to pentadactyl buffers, or I just do less batch image viewing/tab aggregating these days.

* Reinstated RefControl, because Referrer Control doesn’t have import/export.
* Removed stylish. I might be able to apply the wikipedia theme with pentadactyl, I’ll look into that soon.
* New extension: [Open With](https://addons.mozilla.org/en-US/firefox/addon/open-with/). I’m using mpv on both Windows and Linux now- combined with youtube-dl you can pass many URLs directly to mpv and it will play any video on the page. If there’s a video on the page, I run “Open With mpv”.

## Update - 16/11/21

Web of Trust was evil, removing it from my list.

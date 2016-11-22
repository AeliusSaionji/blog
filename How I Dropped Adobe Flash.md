Disclaimer - I only ever used flash for video streaming sites. If you actually rely on flash based web apps, the only thing I can suggest is to try downloading the swf and running it in MPC-HC.
Disclaimer 2 - Nothing revolutionary here; I'm actually describing some very popular software. However, I managed to overlook this for a very long time despite trying to find basically exactly this. I think it's more well known in the Linux community and doesn't come across the radar of Windows users, despite being cross platform. If I overlooked this, I'm sure others have too, so I'm writing this for them.

<!-- more -->

Here's the rub: the program named youtube-dl (which supports more than youtube, full list here http://rg3.github.io/youtube-dl/supportedsites.html) extracts the location of the video file from any given web page and passes it off to a video player. The list of supported sites contains which providers youtube-dl can understand- but any given site can embed content from these providers. In fact, in my experience 9/10 porn sites not on the supported list get their videos from a site that IS supported. At first I was impressed with how often it worked, now I'm more surprised when it doesn't.

* Download http://rg3.github.io/youtube-dl/
	I like to put it somewhere on PATH
* Download http://mpv.srsfckn.biz/
	Extract to the same folder as youtube-dl.exe
	This player eats youtube-dl to gain its powers
* Install [Firefox](https://addons.mozilla.org/en-US/firefox/addon/open-with/) or [Chrome](https://chrome.google.com/webstore/detail/open-with-external-applic/hccmhjmmfdfncbfpogafcbpaebclgjcp) extension to facilitate use
	Create an "open with mpv"

Done. When a site has video content, click "open with mpv". If mpv opens, you're in business! If it doesn't open, youtube-dl doesn't like your site. It's possible to use youtube-dl with your video player of choice, but that's more complicated. It's much easier to just read mpv's documentation and submit to it :)

Oh, and be sure to check for youtube-dl updates from time to time. Sites change, youtube-dl updates to keep supporting them.

Worth noting- you can open YouTube playlists in this way, and opening a YouTube profile page will play all videos from the account, starting with the most recently uploaded.

## Update 2016/11/21
The chrome extension no longer works and I know of no replacement.

A privacy hardened daily use browser install guide.

The spectrum of how privacy hardened you want your browser to be (aka, your threat model) can vary greatly. This install is probably the most extreme you can get while still having a browser functional enough to be a daily user.


## About fingerprinting
Info about fingerprinting (you should read this!): https://github.com/arkenfox/user.js/wiki/3.3-Overrides-%5BTo-RFP-or-Not%5D
Basic explanation of what fingerprinting is: https://coveryourtracks.eff.org/learn

This install uses Resist Fingerprinting (RFP).
RFP can break some functions, you should read the "🟪 RFP" section of this page in it's entirety: https://github.com/arkenfox/user.js/wiki/3.3-Overrides-%5BTo-RFP-or-Not%5D#-rfp
In summary:
- RFP can break websites by masking the canvas, which causes a glitchy, colorful, wavy visual bug. You can easily set a permanent or temporary site exception by clicking the canvas button that appears when a site requests your canvas size, or by doing `Ctrl-I > Permissions > Extract canvas data`
- RFP makes it so your timezone is always UTC0
- RFP makes it so that you always use the light theme

For times when your threat model does demand that you are not fingerprinted at all, you can either use the Tor browser or Mullvad Browser in conjunction with a VPN (doesn't have to be Mullvad VPN.) For more information: https://www.privacyguides.org/en/desktop-browsers/#mullvad-browser and https://www.privacyguides.org/en/tor


## Guide
1. Install **LibreWolf**: https://librewolf.net/installation/
2. Install **arkenfox** (https://github.com/arkenfox/user.js/wiki)
	1. Download the latest release: https://github.com/arkenfox/user.js/releases/latest
	2. Go to about:support
	3. Open the folder shown next to *Profile Folder* under *Application Basics*
		- If you are not using a new profile: https://github.com/arkenfox/user.js/blob/master/scratchpad-scripts/arkenfox-cleanup.js
	 4. Extract the following from the arkenfox release you downloaded into your profile folder:
		- `user.js`
		- `updater.sh` (.bat on Windows)
		- `prefsCleaner.sh` (.bat on Windows)
	5. **arkenfox overrides** (https://github.com/arkenfox/user.js/wiki/3.1-Overrides)
		1. Create a file titled `user-overrides.js` in your profile folder
			- Add the following: 
				```js
				user_pref("browser.startup.page", 3); // Restores previous session on startup
				user_pref("privacy.clearOnShutdown_v2.browsingHistoryAndDownloads", false); // Doesn't clear browsing history on shutdown
				```
		2. Close LibreWolf
		3. Run `updater.sh` (.bat on Windows)
		4. Run `prefsCleaner.sh` (.bat on Windows)
		5. Check if arkenfox worked
			1. Go to about:config
			2. Search for "parrot" (yes, the bird)
			3. If arkenfox is working, it should say "SUCCESS: No no he's not dead, he's, he's restin'!" (A reference to the [Dead Parrot Sketch](https://wikipedia.org/wiki/Dead_Parrot_sketch))
3. Go through **Preferences**
	1. Go to Settings in LibreWolf or go to about:preferences
		1. **Search**
			1. *Default Search Engine*
				1. Check "*Use this search engine in Private Windows*"
			2. *Address Bar*
				1. Uncheck "*Shortcuts*"
				2. Uncheck "*Quick actions*"
			3. *Search Shortcuts*
				1. Uncheck **everything** except "*DuckDuckGo, Wikipedia (en), Bookmarks, Tabs, History*"
				2. Click "*Add*"
					Search engines you may want to add:
					- YouTube- https://www.youtube.com/results?search_query=%s
					- Urban Dictionary- https://www.urbandictionary.com/define.php?term=%s
					- More to be added in the future
		2. **Privacy & Security**
			1. *DNS over HTTPS*
				1. Click "*Max Protection*"
					- Click "*Custom*" under *Choose provider*
					- In the text box, put `https://base.dns.mullvad.net/dns-query`
					- For more filtering options and information about DNS: https://mullvad.net/help/dns-over-https-and-dns-over-tls (If you get "Hmm. We’re having trouble finding that site." set your DNS back to "*Default Protection*")
4. **Extensions**
	1. Configure **uBlock Origin** (installed by default) (https://github.com/gorhill/uBlock/wiki/Blocking-mode)
		1. Click the uBlock icon (Red shield in top right on LibreWolf)
		2. Open the dashboard (Gears icon)
		3. Check "*I am an advanced user*" under *Advanced*
		4. Click the uBlock icon again
		5. Next to `3rd-party scripts` and `3rd-party frames`, go to the left column and click the red.
			- You should see the left column being fully red and the right column being opaque red next to `3rd-party scripts` and `3rd-party frames`.
		6. Click the lock icon
		- If you don't already know how to block and unblock elements of a site permanently and temporarily, read this: https://www.maketecheasier.com/ultimate-ublock-origin-superusers-guide/
	2. Install **Skip Redirect**: https://addons.mozilla.org/firefox/addon/skip-redirect/
		- You may at times have to add sites to the *No-skip-urls-list*, to do this, open the extension and type the URL in the text box under *No-skip-urls-list*
	3. **Other extensions** you might want (all open-source)
		- Violentmonkey (Userscripts): https://addons.mozilla.org/firefox/addon/violentmonkey/
		- Bitwarden (Password manager): https://addons.mozilla.org/firefox/addon/bitwarden-password-manager
		- Search by Image (Reverse image search): https://addons.mozilla.org/firefox/addon/search_by_image/
		- LanguageTool (Grammar checker): https://addons.mozilla.org/firefox/addon/languagetool/
		- SponsorBlock (YouTube sponsor skip): https://addons.mozilla.org/firefox/addon/sponsorblock
		- DeArrow (YouTube crowdsourced titles and thumbnails): https://addons.mozilla.org/firefox/addon/dearrow
		- ImprovedTube (YouTube customizer) https://addons.mozilla.org/firefox/addon/youtube-addon/
		- Mullvad (For Mullvad VPN): https://mullvad.net/download/browser/extension
	- If you're wondering why you shouldn't install that extension that says it will enhance your privacy: https://github.com/arkenfox/user.js/wiki/4.1-Extensions#-dont-bother
5. Import **Bookmarks** if you have them
	1. Open Manage Bookmarks (`Ctrl + Shift + O`)
	2. Click *Import and Backup*
		1. Click "*Restore*" or "*Import Bookmarks from HTML*"
		2. Find your bookmarks file

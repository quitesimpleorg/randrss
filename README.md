What is randrss?
================
Normal RSS readers usually fetch all feeds more or less at the same time
at constant intervals. Anyone who monitors internet traffic can
look for this pattern and therefore identify users.

randrss fetches all your feeds at random intervals at an random order
over a certain period of time. The feeds will be downloaded and you then
serve them using your own web server. This way you also don't have to 
worry about how your client deals with cookies etc.

Additionally, by having only one client fetching the feeds and your readers
pointed to andrss's downloaded feeds, you avoid certain trackers
that may identify you across devices (google's feed proxy, cloudflare),
because it's very likely that the combination of feeds you read are 
unique. As your feeds are on a single server now, you can isolate your
RSS reader to its own network container so it can only contact your 
server. This is probably what you should do to be sure your client does
not contact the feed servers in any way. In Thunderbird, set 
browser.chrome.favicons to false.

A drawback of this approach is that the time you get new feeds
is delayed, but that should be acceptable.

Usage
=====
Fetchers
--------
Scripts that request the feeds while trying to look like a normal client. 
By default, they are launched with "torsocks". 

Config file
-----------
For each feed, an individual config file is used.

Example:
A simple example config file for kernel.org:
FEED_URL="https://www.kernel.org/feeds/kdist.xml"
FEED_OUTPUT="/var/www/feeds/kernelreleases.feed"

Launch
------
randrss [path to directory containing the config files] [fetchersfile]

fetchersfile: take a look at the example file in the repo. It lists
the paths to the fetchers that will randomly be used.

optional third parameter: "syncnow". Do not sleep for random intervals.
Fetch all feeds and exit.





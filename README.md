What is randrss?
================
Normal RSS readers usually fetch all feeds more or less at the same time
at constant intervals. Anyone who monitors internet traffic can
look for this pattern and therefore identify users.

In contrast, randrss fetches all your feeds at random intervals 
and also at an random order. The feeds will be downloaded and you then
serve them using your own web server. It poorly attemps to look like 
normal browsers while fetching the feeds, and uses Tor by default.

This has several advantages. You don't need to worry how your
client deals with cookies for example. Since you point your favorite
RSS client to randrss's downloaded feeds, you avoid certain trackers 
like google's feed proxy and cloudflare. They may identify you across 
devices as it is very likely that the combination of feeds you read
is unique. In the context of "hardening", this is also useful to
restrict the servers your RSS client can contact (for instance,
by using network namespaces, etc.).

A drawback of this approach is that the time you get new feeds
is delayed, but that should be acceptable. Furthermore, this tool
might leave a distinct signature itself. It should still be
better than fetching everything at once, however it's primary purpose
is to hide you from the mentioned (potential) trackers. 


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





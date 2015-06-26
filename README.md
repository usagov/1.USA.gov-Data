# 1.USA.gov Data

## On This Page
* [About the Data](#about-the-data)
* [How to Access The Data](#how-to-access-the-data)
* [Code from the 1.USA.gov Hack Day](#code-from-the-1usagov-hack-day)
* [Projects from the 1.USA.gov Hack Day](#projects-from-the-1usagov-hack-day)
* [Terms of Service](#terms-of-service)

## About The Data
1.USA.gov URLs are created whenever anyone shortens a .gov or .mil URL using [bitly](http://bitly.com/).

We provide a raw [pub/sub](http://en.wikipedia.org/wiki/Publish/subscribe) feed of data created any time anyone clicks on a 1.USA.gov URL. The pub/sub endpoint responds to http requests for any 1.USA.gov URL and returns a stream of JSON entries, one per line, that represent real-time clicks.

If you are using the 1.USA.gov data and have questions, feedback, or want to tell us about your product, please [e-mail us](mailto:usagov-developers@gsa.gov).

## How to Access The Data
You can access the feed at http://developer.usa.gov/1usagov

Measured Voice maintains an [archive of the raw data](http://bitly.measuredvoice.com/bitly_archive/?C=M;O=D) from June 2, 2011 - May 17, 2013.

The JSON data dictionary is as follows:

    {
            "a": USER_AGENT, 
            "c": COUNTRY_CODE, # 2-character iso code
            "nk": KNOWN_USER,  # 1 or 0\. 0=this is the first time we've seen this browser
            "g": GLOBAL_BITLY_HASH, 
            "h": ENCODING_USER_BITLY_HASH,
            "l": ENCODING_USER_LOGIN,
            "hh": SHORT_URL_CNAME,
            "r": REFERRING_URL,
            "u": LONG_URL,
            "t": TIMESTAMP,
            "gr": GEO_REGION,
            "ll": [LATITUDE, LONGITUDE],
            "cy": GEO_CITY_NAME,
            "tz": TIMEZONE # in http://en.wikipedia.org/wiki/Zoneinfo format
            "hc": TIMESTAMP OF TIME HASH WAS CREATED, 
            "al": ACCEPT_LANGUAGE http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.4 
        }

## Code from the 1.USA.gov Hack Day
We held a nationwide [1.USA.gov Hack Day](http://blog.usa.gov/post/7054661537/1-usa-gov-open-data-and-hack-day) on July 29, 2011 to encourage people to explore the 1.USA.gov data. The following code was created by participants and shared publicly for others to use:

*   [gogogon](https://github.com/measuredvoice/gogogon) - Consumes the 1.USA.Gov click feed and generates daily rankings of URLs
*   [gogogon fork](https://github.com/blackstonetech/gogogon) - Created for use with [dnsseclistwalk](https://github.com/blackstonetech/dnsseclistwalk)
*   [gist: 1114234](https://gist.github.com/1114234) - Python code to get the 1.USA.gov archive
*   [one-usa](http://github.com/chrismetcalf/one-usa) - A pub/sub listener for the 1.USA.gov feed

## Projects from the 1.USA.gov Hack Day
A number of items were created in anticipation of and at the Hack Day. Most tools centered around finding popular links, showing links by location, and using click data to enhance security:

*   **Popular now** - Barg Upender and Adam created a site called [PopGov.us](http://popgov.mobomo.com/) that shows which government links are popular in real time.
*   **Popularity by day** - Measured Voice created [GovClicks](http://govclicks.measuredvoice.com) to show the most popular links per day. GovClicks is built using [Gogogon](https://github.com/measuredvoice/gogogon) which consumes the 1.USA.Gov click feed and generates daily rankings of URLs.
*   **NASA links** - Adam Laiacano analyzed 1.USA.gov data and found that 42% of all clicks on 1.USA.gov links go to NASA websites. He created a [map](http://adamlaiacano.tumblr.com/post/8243398653/heres-one-of-the-plots-i-made-at-the-1-usa-gov) that shows that people in Europe are more likely to only click on NASA links, while people in the United States click on links from a wider variety of government links.
*   **Across the world** - Helmut Hissen made an [animation](http://youtu.be/-pHHtGfTPV4) that shows clicks across the globe on 1.USA.gov links from June 2 through July 14\. Red flashes represent clicks from non-mobile devices, and green flashes represent clicks from mobile devices. Note that the final NASA Shuttle launch occurred on July 8\. There’s a dramatic increase in activity at the 1:24 mark.
*   **Map of clicks** - Chris Metcalf built a [tool](http://github.com/chrismetcalf/one-usa) that ingests the 1.USA.gov data and feeds it into [Data.gov](http://explore.data.gov/Information-and-Communications/1-USA-gov-Short-Links/wzeq-n5pg). It also feeds the data into a Google Map to show [clicks based on location](http://opendata.socrata.com/dataset/1-USA-gov-Google-Map/vjkt-58f3).
*   **Popularity by location** - Robert built a [tool](http://corpdrone.com/GovHackDay/Spark.aspx) that searches for the most popular links near your city or within your country.
*   **NASA shuttle launch** - Bitly created a [visualization](http://blog.bitly.com/post/7624585240/visualizing-the-nasa-shuttle-launch-with-public) that shows clicks around the globe that relate to the NASA shuttle launch on July 8.
*   **Sharing by domain** - Shreyas Karnik looked at which government domains are commonly shortened at a particular point of time and from what location. The resulted in a [map](http://skarnik.wordpress.com/2011/07/30/analysis-of-usa-gov-shortened-links/) showing the location of where the top 10 domains are shared.
*   **DNSSEC status** - Earl Crane, Scott Rose, and Richard Bullington-McGuire worked on a tool to look at the popularity of 1.USA.gov links against the DNSSEC status of .gov domains. Their project is still in progress, but the code is available to the public ([gogogon fork](https://github.com/blackstonetech/gogogon) and [DNSSEC List Walk](https://github.com/blackstonetech/dnsseclistwalk)).
*   **DNSSEC status visualization** - Duane Wessels [graphed](http://www.verisignlabs.com/notes/usa.gov-hackathon/top200.svg) the DNSSEC status of domains by popularity of short URLs from that domain. The size of nodes in the graph represent the number of URLs at or below that name that were shortened. A number of agencies have DNSSEC deployed on their own domains, but employ third party CDN services, such as Akamai, which do not utilize DNSSEC at this point. [Scripts](http://www.verisignlabs.com/notes/usa.gov-hackathon/) and additional results are also available.
*   **Twitter mentions** - Dmitry Kachaev compared the list of .gov domain names from Data.gov against 1.USA.gov data. He found that only 296 registered domains, out of 1,731, were mentioned on Twitter in the past 60 days. He also created [Python code](https://gist.github.com/1114234) to get archived click data.
*   **Creation and clicks** - Harlan Harris looked at the time difference between when a link was created and when it was clicked. He created [density plots](http://www.harlan.harris.name/2011/07/hacking-gov-shortened-links/) to show the results. [Results are available on his blog.](http://www.harlan.harris.name/2011/07/hacking-gov-shortened-links/)
*   **Word cloud** - Hani Anani used 1.USA.gov data to identify popular government links, and then analyzed the contents with Open Calais to create a word cloud that summarizes popular government topics in near real time.
*   **Sonifications** - Niki Yoshiuchi from the New York event created a [sonification](http://www.aplusbi.com/?p=194), or audio representation of the data. Joachim Gossmann is also started working on a variety of sonifications.

## Terms of Service
By using this data, you agree to the [Terms of Service](/About/developer-resources/terms-of-service.shtml).
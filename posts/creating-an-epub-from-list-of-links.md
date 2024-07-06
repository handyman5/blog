<!--
.. title: Creating an ePub from a list of links
.. slug: creating-an-epub-from-list-of-links
.. date: 2017-01-22 12:00:00 UTC-07:00
.. tags: 
.. category: howto
.. link: 
.. description: 
.. type: text
-->

I’ve read and enjoyed parts of [Michael O. Church’s](https://web.archive.org/web/20201205012321/https://michaelochurch.wordpress.com/ "https://web.archive.org/web/20201205012321/https://michaelochurch.wordpress.com/") take on Venkatesh Rao’s [Gervais Principle](https://web.archive.org/web/20201205012321/http://www.ribbonfarm.com/the-gervais-principle/ "https://web.archive.org/web/20201205012321/http://www.ribbonfarm.com/the-gervais-principle/"), but he took his blog offline before I was able to read them all. I decided to snag copies of all of the posts from [the Wayback Machine](https://web.archive.org/web/20201205012321/https://archive.org/web/ "https://web.archive.org/web/20201205012321/https://archive.org/web/") and turn them into an ebook for convenient reading. This appears to be a solved problem thanks to [this handy little Python library, pypub](https://web.archive.org/web/20201205012321/https://pypub.readthedocs.io/en/latest/ "https://web.archive.org/web/20201205012321/https://pypub.readthedocs.io/en/latest/"), but just in case it winds up being useful to someone here is what I did.

<!-- TEASER_END -->

### Building the list of links


I googled for the first post, looked it up in the Wayback Machine, noted a working URL, and kept following links until I found all of the posts in the series.


For reference, here they are.

```

1: https://web.archive.org/web/20150325112004/https://michaelochurch.wordpress.com/2013/02/19/gervais-principle-questioned-macleods-hierarchy-the-technocrat-and-vc-startups/
2: https://web.archive.org/web/20150705103513/https://michaelochurch.wordpress.com/2013/02/20/1410/
3: https://web.archive.org/web/20151221082352/https://michaelochurch.wordpress.com/2013/02/22/gervais-rehash-part-iii-markov-and-management-plus-a-4th-culture/
4: https://web.archive.org/web/20151221143632/https://michaelochurch.wordpress.com/2013/02/26/gervais-macleod-4-a-world-without-losers/
5: https://web.archive.org/web/20151221143322/https://michaelochurch.wordpress.com/2013/02/28/gervais-macleod-5-interfaces-meritocracy-and-the-effort-thermocline/
6: https://web.archive.org/web/20151221143806/https://michaelochurch.wordpress.com/2013/03/01/gervais-macleod-6-morality-civility-and-chaos/
7: https://web.archive.org/web/20151018091056/https://michaelochurch.wordpress.com/2013/03/11/gervais-macleod-7-defining-organizational-health-the-mike-test-and-vc-istans-fate/
8: https://web.archive.org/web/20151221083041/https://michaelochurch.wordpress.com/2013/03/12/gervais-macleod-8-human-nature-theories-x-y-z-and-a/
9: https://web.archive.org/web/20151221144342/https://michaelochurch.wordpress.com/2013/03/14/gervais-macleod-9-convexity/
10: https://web.archive.org/web/20151221143541/https://michaelochurch.wordpress.com/2013/03/17/gervais-macleod-10-the-pull-of-lawful-evil/
11: https://web.archive.org/web/20151225141206/https://michaelochurch.wordpress.com/2013/03/18/gervais-macleod-11-alignment-and-careers/
12: https://web.archive.org/web/20151221143250/https://michaelochurch.wordpress.com/2013/03/19/gervais-macleod-12-growth-chaos-and-risk/
13: https://web.archive.org/web/20151221143502/https://michaelochurch.wordpress.com/2013/03/20/gervais-macleod-13-separability-work-and-play/
14: https://web.archive.org/web/20151221144410/https://michaelochurch.wordpress.com/2013/03/21/gervais-macleod-14-expanding-alignment-plus-well-adjustedness/
15: https://web.archive.org/web/20151221144210/https://michaelochurch.wordpress.com/2013/03/22/gervais-macleod-15-what-is-being-rich/
16: https://web.archive.org/web/20151221143221/https://michaelochurch.wordpress.com/2013/03/25/gervais-macleod-16-healthy-culture-vs-why-you/
17: https://web.archive.org/web/20151018092426/https://michaelochurch.wordpress.com/2013/03/26/gervais-macleod-17-building-the-future-and-financing-lifestyle-businesses/
18: https://web.archive.org/web/20151221144309/https://michaelochurch.wordpress.com/2013/03/28/gervais-macleod-18-more-on-trust-square-root-syndrome-brownian-and-progressive-time/
19: https://web.archive.org/web/20151221144051/https://michaelochurch.wordpress.com/2013/03/29/gervais-macleod-19-living-in-truth-fighting-the-lie/
20: https://web.archive.org/web/20150919091259/https://michaelochurch.wordpress.com/2013/04/01/gervais-macleod-20-bozo-bit-vs-simple-trust/
21: https://web.archive.org/web/20150910154001/https://michaelochurch.wordpress.com/2013/04/03/gervais-macleod-21-why-does-work-suck/
22: https://web.archive.org/web/20150919133351/https://michaelochurch.wordpress.com/2013/04/16/gervais-macleod-22-inferno/
23: https://web.archive.org/web/20151221143922/https://michaelochurch.wordpress.com/2013/04/30/gervais-macleod-23-managers-mentors-executives-cops-and-thugs/
24: https://web.archive.org/web/20151221082517/https://michaelochurch.wordpress.com/2013/06/04/gervais-macleod-24-fundamental-theorem-of-employment/
25: https://web.archive.org/web/20151221083106/https://michaelochurch.wordpress.com/2013/06/08/gervais-macleod-25-state-and-truth-seekers-plus-the-emergence-of-the-technocrat/
26: https://web.archive.org/web/20151221082619/https://michaelochurch.wordpress.com/2013/08/06/gervais-macleod-26-r-and-k-selection-in-organizations-and-capitalism/

```


### Creating the ebook


[pypub](https://web.archive.org/web/20201205012321/https://pypub.readthedocs.io/en/latest/ "https://web.archive.org/web/20201205012321/https://pypub.readthedocs.io/en/latest/") made this bit super easy!



```
import pypub, os
epub = pypub.Epub('Gervais Principle Questioned')
urls = open('links.txt').read()
real_urls = [x for x in urls.split() if x.startswith('https:')]
for u in real_urls:
  c = pypub.create_chapter_from_url(x)                                                                                                     
  epub.add_chapter(c)          
epub.create_epub(os.getcwd())  

```

Et voila!


### Share this:

* [Click to share on Twitter (Opens in new window)](https://web.archive.org/web/20201205012321/http://ajcsystems.com/blog/blog/2017/01/22/creating-an-epub-from-a-list-of-links/?share=twitter "Click to share on Twitter")
* [Click to share on Facebook (Opens in new window)](https://web.archive.org/web/20201205012321/http://ajcsystems.com/blog/blog/2017/01/22/creating-an-epub-from-a-list-of-links/?share=facebook "Click to share on Facebook")
* 


### *Related*


 
 


No comments
-----------


[Comments feed for this article](https://web.archive.org/web/20201205012321/http://ajcsystems.com/blog/blog/2017/01/22/creating-an-epub-from-a-list-of-links/feed/ "https://web.archive.org/web/20201205012321/http://ajcsystems.com/blog/blog/2017/01/22/creating-an-epub-from-a-list-of-links/feed/")



Trackback link: [http://ajcsystems.com/blog/blog/2017/01/22/creating-an-epub-from-a-list-of-links/trackback/](https://web.archive.org/web/20201205012321/http://ajcsystems.com/blog/blog/2017/01/22/creating-an-epub-from-a-list-of-links/trackback/ "https://web.archive.org/web/20201205012321/http://ajcsystems.com/blog/blog/2017/01/22/creating-an-epub-from-a-list-of-links/trackback/")




### Reply [Cancel reply](/web/20201205012321/http://ajcsystems.com/blog/blog/2017/01/22/creating-an-epub-from-a-list-of-links/#respond "/web/20201205012321/http://ajcsystems.com/blog/blog/2017/01/22/creating-an-epub-from-a-list-of-links/#respond")

Your email address will not be published.

 
Your comment

Name 


Email 


Website 


 Notify me of follow-up comments by email.

 Notify me of new posts by email.

 








Please copy the string **3wEPCI** to the field below:





 


### Other Me


* [Careers @ StackOverflow](https://web.archive.org/web/20201205012321/http://careers.stackoverflow.com/comptona "https://web.archive.org/web/20201205012321/http://careers.stackoverflow.com/comptona")
* [Facebook](https://web.archive.org/web/20201205012321/http://www.facebook.com/handyman5 "https://web.archive.org/web/20201205012321/http://www.facebook.com/handyman5")
* [Google+](https://web.archive.org/web/20201205012321/https://plus.google.com/107538173110176567352 "https://web.archive.org/web/20201205012321/https://plus.google.com/107538173110176567352")
* [LinkedIn](https://web.archive.org/web/20201205012321/http://www.linkedin.com/in/comptona "https://web.archive.org/web/20201205012321/http://www.linkedin.com/in/comptona")
* [Picasa](https://web.archive.org/web/20201205012321/https://picasaweb.google.com/107538173110176567352 "https://web.archive.org/web/20201205012321/https://picasaweb.google.com/107538173110176567352")
* [Twitter](https://web.archive.org/web/20201205012321/http://twitter.com/#!/comptona "https://web.archive.org/web/20201205012321/http://twitter.com/#!/comptona")



### Pages


* [Software](https://web.archive.org/web/20201205012321/http://ajcsystems.com/blog/software/ "https://web.archive.org/web/20201205012321/http://ajcsystems.com/blog/software/")
	+ [Amazon Cloud Drive FUSE filesystem](https://web.archive.org/web/20201205012321/http://ajcsystems.com/blog/software/amazon-cloud-drive-fuse-filesystem/ "https://web.archive.org/web/20201205012321/http://ajcsystems.com/blog/software/amazon-cloud-drive-fuse-filesystem/")
	+ [MythTV voice control](https://web.archive.org/web/20201205012321/http://ajcsystems.com/blog/software/mythtv-voice-control/ "https://web.archive.org/web/20201205012321/http://ajcsystems.com/blog/software/mythtv-voice-control/")
	+ [Poodledo / tdcli](https://web.archive.org/web/20201205012321/http://ajcsystems.com/blog/software/poodledo-tdcli/ "https://web.archive.org/web/20201205012321/http://ajcsystems.com/blog/software/poodledo-tdcli/")
	+ [valet: single-file drop-in git-backed wiki](https://web.archive.org/web/20201205012321/http://ajcsystems.com/blog/software/valet-single-file-drop-in-git-backed-wiki/ "https://web.archive.org/web/20201205012321/http://ajcsystems.com/blog/software/valet-single-file-drop-in-git-backed-wiki/")
* [SuperFeed](https://web.archive.org/web/20201205012321/http://ajcsystems.com/blog/my-activity-feed/ "https://web.archive.org/web/20201205012321/http://ajcsystems.com/blog/my-activity-feed/")


### Archives


* [November 2017](https://web.archive.org/web/20201205012321/http://ajcsystems.com/blog/blog/2017/11/ "https://web.archive.org/web/20201205012321/http://ajcsystems.com/blog/blog/2017/11/") (1)
* [January 2017](https://web.archive.org/web/20201205012321/http://ajcsystems.com/blog/blog/2017/01/ "https://web.archive.org/web/20201205012321/http://ajcsystems.com/blog/blog/2017/01/") (1)
* [June 2015](https://web.archive.org/web/20201205012321/http://ajcsystems.com/blog/blog/2015/06/ "https://web.archive.org/web/20201205012321/http://ajcsystems.com/blog/blog/2015/06/") (1)
* [October 2013](https://web.archive.org/web/20201205012321/http://ajcsystems.com/blog/blog/2013/10/ "https://web.archive.org/web/20201205012321/http://ajcsystems.com/blog/blog/2013/10/") (1)
* [September 2013](https://web.archive.org/web/20201205012321/http://ajcsystems.com/blog/blog/2013/09/ "https://web.archive.org/web/20201205012321/http://ajcsystems.com/blog/blog/2013/09/") (2)
* [August 2013](https://web.archive.org/web/20201205012321/http://ajcsystems.com/blog/blog/2013/08/ "https://web.archive.org/web/20201205012321/http://ajcsystems.com/blog/blog/2013/08/") (1)
* [October 2012](https://web.archive.org/web/20201205012321/http://ajcsystems.com/blog/blog/2012/10/ "https://web.archive.org/web/20201205012321/http://ajcsystems.com/blog/blog/2012/10/") (8)
* [August 2012](https://web.archive.org/web/20201205012321/http://ajcsystems.com/blog/blog/2012/08/ "https://web.archive.org/web/20201205012321/http://ajcsystems.com/blog/blog/2012/08/") (1)
* [June 2012](https://web.archive.org/web/20201205012321/http://ajcsystems.com/blog/blog/2012/06/ "https://web.archive.org/web/20201205012321/http://ajcsystems.com/blog/blog/2012/06/") (1)
* [November 2011](https://web.archive.org/web/20201205012321/http://ajcsystems.com/blog/blog/2011/11/ "https://web.archive.org/web/20201205012321/http://ajcsystems.com/blog/blog/2011/11/") (1)
* [October 2011](https://web.archive.org/web/20201205012321/http://ajcsystems.com/blog/blog/2011/10/ "https://web.archive.org/web/20201205012321/http://ajcsystems.com/blog/blog/2011/10/") (4)
* [February 2007](https://web.archive.org/web/20201205012321/http://ajcsystems.com/blog/blog/2007/02/ "https://web.archive.org/web/20201205012321/http://ajcsystems.com/blog/blog/2007/02/") (2)
* [December 2006](https://web.archive.org/web/20201205012321/http://ajcsystems.com/blog/blog/2006/12/ "https://web.archive.org/web/20201205012321/http://ajcsystems.com/blog/blog/2006/12/") (1)
* [October 2006](https://web.archive.org/web/20201205012321/http://ajcsystems.com/blog/blog/2006/10/ "https://web.archive.org/web/20201205012321/http://ajcsystems.com/blog/blog/2006/10/") (1)




 


 

### Meta


* [Log in](https://web.archive.org/web/20201205012321/http://ajcsystems.com/blog/wp-login.php "https://web.archive.org/web/20201205012321/http://ajcsystems.com/blog/wp-login.php")
* [Entries feed](https://web.archive.org/web/20201205012321/http://ajcsystems.com/blog/feed/ "https://web.archive.org/web/20201205012321/http://ajcsystems.com/blog/feed/")
* [Comments feed](https://web.archive.org/web/20201205012321/http://ajcsystems.com/blog/comments/feed/ "https://web.archive.org/web/20201205012321/http://ajcsystems.com/blog/comments/feed/")
* [WordPress.org](https://web.archive.org/web/20201205012321/https://wordpress.org/ "https://web.archive.org/web/20201205012321/https://wordpress.org/")



 


[Subscribe to feed](https://web.archive.org/web/20201205012321/http://ajcsystems.com/blog/feed/ "https://web.archive.org/web/20201205012321/http://ajcsystems.com/blog/feed/")



Powered by [WordPress](https://web.archive.org/web/20201205012321/http://wordpress.org/ "https://web.archive.org/web/20201205012321/http://wordpress.org/") and [Tarski](https://web.archive.org/web/20201205012321/http://tarskitheme.com/ "https://web.archive.org/web/20201205012321/http://tarskitheme.com/")



 
 
















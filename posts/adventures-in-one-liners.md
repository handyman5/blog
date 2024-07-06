<!--
.. title: Adventures in One-Liners
.. slug: adventures-in-one-liners
.. date: 2013-08-22 12:00:00 UTC-07:00
.. tags: 
.. category: linux
.. link: 
.. description: 
.. type: text
-->

_(originally from [https://web.archive.org/web/20150421214026/http://ajcsystems.com/blog/blog/2013/08/22/adventures-in-one-liners/])_

I wrote this one-liner today, and that it exists makes me sad.

<code>
rrdtool update $tmpfile $(curl "http://127.0.0.1:4242/api/query?start=$(($(date +'%s')+$start))&m=sum:$metric\{cluster=$cluster,hostname=$hostname\}" | python -c "import sys, json; j=json.loads(sys.stdin.read())[0]['dps']; sys.stdout.write(' '.join(['%d:%s' % (int(x), j[x]) for x in sorted(j.keys())]))")
<code>

That it actually works just downright terrifies me.

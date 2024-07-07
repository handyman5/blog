<!--
.. title: Blog Setup Notes
.. slug: blog-setup-notes
.. date: 2024-07-05 16:30:22 UTC-07:00
.. tags: 
.. category: 
.. link: 
.. description: 
.. type: text
-->

This page details the things I had to do to set up this blog.

## Initial Setup

References:

* [https://getnikola.com/handbook.html]
* [https://getnikola.com/getting-started.html]

## Automated Build

Using the [`nikola-action` Github Action](https://github.com/getnikola/nikola-action). Notably, I had to reference `v8` even though the README says `v4`.

Source: [main.yml](../../.github/workflows/main.yml)

I had to use a custom action to do the Nikola build; see [this page](https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site#publishing-with-a-custom-github-actions-workflow) for how to do so.

Additional references:

* https://getnikola.com/blog/automating-nikola-rebuilds-with-github-actions.html

## Backfilling old posts

I have some old blogs which have vanished from the internet (but not from the Internet Archive). I used [this tool](https://www.minifier.org/html-to-markdown) to convert their HTML to Markdown so I could import them here.

## Style References

* [The Cloistered Monkey](https://necromuralist.github.io/) - https://github.com/necromuralist/necromuralist.github.io

## Bluesky Comments


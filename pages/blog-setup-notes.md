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


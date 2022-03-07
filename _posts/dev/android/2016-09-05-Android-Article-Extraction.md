---
layout: post
title: Android · Website and Article Extraction
description: Ideas and solutions when trying to extract article content from a website
date: 2016-09-05 15:00:00 +0100
image: '/images/posts/whatsapp-empty.jpg'
tags: [dev, software, apps, android]
featured: false
---

## What's this about?

I was working on extracting article contents for our chat features in [Bria](https://www.counterpath.com/bria-enterprise), so I started researching the topic of website content extraction. A lot of chat interfaces have that tiny image preview and a short website description inside of a chat bubble -- so that's exactly what we wanted to do.

Given that our app is an enterprise app, the constraints can be quite difficult to manage... one of the constraints in enterprise software is often that there's no guarantee a website will have a public access. This means that the extraction won't be as easy as simply pulling [Open Graph](https://ogp.me) attributes from the page's header.

Luckily, [Gravity Labs](https://gravity.com) gave me a lot of inspiration and hard base work was already done for their backend implementation, so I was able to write the **Goose** article extractor for Android on top of their work.

Sources are here:

  - [GitHub repository](https://github.com/milosmns/goose)

## How does this work?

It's a multi-step process:

  1. Look for Open Graph attributes, use if found
  1. If not found, look for the article through HTML
  1. Clean up the article text
  1. Find the best image that goes with the article
  1. Pack text attributes and the preview image together and return the result

On to the exciting part -- the steps after step #1, i.e. there's no Open Graph configuration.

#### Document cleaning

When you pass a URL to **Goose**, the first thing it does is to the HTML is to clean up the document and make it easier to parse. It will go through the whole document and remove comments, common social network elements, convert `em` and other tags to plain text DOM nodes, convert `div`s with text to paragraphs, and run a general cleanup sequence (removing spaces, new lines, quotes, encodings, etc).

#### Content and image extraction

While the process might be imperfect, let's preface the next part with this: **Goose runs locally, on the user's phone.** It shares no data with any server, nor does it require any database or protocol away from the given URL.

When dealing with random article links, it's inevitable to come across the craziest of HTML files. Some sites even like to include 2 or more HTML files per page, one below the other. _(does make sense to parse that site?)_ Anyway, Goose uses a scoring system based on clustering of English "stop" words, among other factors, all of which you can find in the source code. Goose also does descending scoring, meaning -- as the DOM nodes are detected in the "bottom parts" of pages (later in the DOM iteration), the lower their scores become. The goal here is to find the "strongest" cluster of text nodes inside the page, and therefore assume that cluster is the most relevant group of content. It's somewhat expected that articles with a lot of "stop" words near the top of the page are the most relevant ones on that page.

Image extraction is the sequence that takes the longest to complete. Trying to find the most "important" image on a page proved to be challenging. To be sure, it requires downloading all of the images and manually inspecting them using some external bitmapping tools. In addition to that, not all images are considered -- Goose checks each image's MIME type, dimensions, byte size, compression quality, etc. Java's internal image-related APIs were just too unreliable and inaccurate, especially on Android where performance and precision need to go hand-in-hand. Goose uses the `BitmapFactory` class to analyze images; it is well documented, heavily tested, fast and quite accurate in what it does.

Images are analyzed from the first DOM node in which Goose finds the content (not the absolute top of the DOM). From there, we have a recursive run outwards to the node's parents, trying to find other good images "nearby". This part of the sequence also checks if those images are maybe ads, banners, author logos, and ignores the bad quality ones.

#### Output

Once Goose has the correct DOM node where it thinks the content is, it will try to reformat the text content of that node to get the output. For example, for NLP-type applications, Goose's output formatter will just suck all the text and ignore everything else. It is possible to attach custom parsers and custom formatters onto Goose, for example to offer a more Flipboardy-type experience with more titles and less descriptions.

Obviously, if Open Graph nodes are found, those will represent the results verbatim.

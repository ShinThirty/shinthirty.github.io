---
layout: post
title:  "Use AmazonDrive to Host Images"
date:   2019-06-27
categories: [note]
tags:   [utility]
---
## Question

I'm hosting a a logo for my team on a public directory on AmazonDrive, and I'd like to embed that logo (a PNG image) into our team wiki.

Is there any way I can **hotlink my PNG file in such a way that it returns a image**, and not the "photo gallery" interface, and that wiki understands it as an image, or I can add it as an image on Sage or SIM?

## Answer

**Yes, you just need to *copy the "View" link of the image* and not click on the image name itself** so Drive doesn't serve the whole "Document" viewer interface.

You also need to make sure that **the permissions on the file you want to embed are "Anyone can view"**, by clicking on the "Share" link. I have created a "Sage" folder with that permission set, so everything I put in it can be linked into Sage/Wiki/SIM easily.

You need to **right click and copy the view link (don't click it)** otherwise you'll get a redirect to a s3 link (that expires).

### Sage/SIM/CRUX (markdown) syntax

You can use the simple syntax:

```general
![Image Alt Text](https://drive.corp.amazon.com/view/diglesia@/pub/sage/embed-me.png)
```

Or you can use the reference-style syntax: (not supported by SIM at the time of writing)

```general
![Image Alt Text][1]
​[1]: https://drive.corp.amazon.com/view/diglesia@/pub/sage/embed-me.png
```

In Sage you also click on the embed image icon and paste your image URL:

![embed-image-from-drive-on-sage](https://i.imgur.com/0KmVfnH.png)

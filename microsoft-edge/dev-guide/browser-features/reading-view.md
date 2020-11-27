---
ms.assetid: 2bc29371-4f2e-4b59-a588-30b107d751f6
description: See how Microsoft Edge provides a Immersive Reader for webpages to enable add-free reading.
title: Immersive Reader - Dev guide
author: MSEdgeTeam
ms.author: msedgedevrel
ms.date: 11/27/2020
ms.topic: article
ms.prod: microsoft-edge
keywords: edge, web development, html, css, javascript, developer
---

# Immersive Reader

Microsoft Edge provides Immersive Reader for a more streamlined, book-like reading experience of webpages without the distraction of unrelated or other secondary content on the page. Immersive Reader can be toggled on or off from the **Immersive Reader** button on the address bar or with `F9`.

## Force Immersive Reader for a web page

Currently Immersive Reader icon will only be shown on compatible pages, but if you want to force Immersive Reader bypassing our eligibility checks, you can use the following meta tag.

```html
<meta name="EDGE_READABLE_FRAME">
```

This is a preview feature and to use, you have to enable the flag `Immersive Reader for Readable Frame` from **edge://flags**

This will show Immersive Reader icon in your web page even if the page is not compatible. The content extracted might not be as good as that of other compatible pages but we try to show the best possible content.

## Enable Immersive Reader for specific content

If you want to display curated content in Immersive Reader, you can use the **EDGE_READABLE_FRAME** meta tag and add **edgeReadable** attribute to the HTML Elements that needs to be shown in Immersive Reader:

```html
<html>
    <head>
        <title>Immersive Reader for specific nodes example</title>
        <meta name="EDGE_READABLE_FRAME">
    </head>
    <body>
        <div>
            <p edgeReadable>I will appear in immersive reader</p>
            <p>I will NOT appear in immersive reader</p>
            <p edgeReadable>I will also appear in immersive reader</p>
        </div>
    </body>
</html>
```
This is a preview feature and to use, you have to enable the flag `Immersive Reader for Edge Readable Elements` from **edge://flags**

-   With this meta tag and attribute, you can choose the content that should be displayed on Immersive Reader, we bypass all the checks and only show the content marked as edgeReadable.
-   If only EDGE_READABLE_FRAME meta tag is present without any HTML Elements having edgeReadable attribute we try to force Immersive Reader on entire page and if page is not compatible, the content displayed might not be as good as other compatible pages.
-   Any HTML Element can be marked as edgeReadable except iframe.

## Enable Immersive Reader for specific iframe

If you want to display content from an iframe in Immersive Reader instead of main page, you can use the **EDGE_READABLE_FRAME** meta tag and add **content** attribute to the meta tag with value of **iframe name** that specifies which iframe content should be shown in Immersive Reader.

```html
<html>
    <head>
        <title>Iframe Reading View</title>
        <meta name="EDGE_READABLE_FRAME" content="irFrame">
    </head>
    <body>
        <h1>Immersive Reader for iframe example</h1>
        <iframe
            id="testFrameId"
            src="/reading/test.html"
            name="testFrame"
        >
        </iframe>
        <iframe
            id="irFrameId"
            src="/reading/this_is_visible_in_ImmersiveReader.html"
            name="irFrame"
        >
        </iframe>
    </body>
</html>
```

This is a preview feature and to use, you have to enable the flag `Immersive Reader for Readable Frame` from **edge://flags**

-   With this meta tag and iframe name in content attribute, you can choose which iframe we should consider while extracting content.
-   You can even specify edgeReadable attribute to HTML Elements in the mentioned iframe, then only edgeReadable elements in that iframe are shown in Immersive Reader.
-   If only EDGE_READABLE_FRAME meta tag is present without specifying which iframe to consider, we try to force Immersive Reader on entire page and if page is not compatible, the content displayed might not be as good as other compatible pages.

## Opting out of Immersive Reader

If you feel your content is not a good fit for Immersive Reader, you can use the following meta tag to opt out of this feature:

```html
<meta name="IE_RM_OFF" content="true">
```

With this tag, the **Immersive Reader** button will not appear in the address bar when your users view your page.

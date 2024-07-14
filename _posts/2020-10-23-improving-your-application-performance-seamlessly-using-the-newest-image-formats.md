---
layout: post
title:  "Improving your application performance seamlessly using the newest image formats"
tags: webp avif Adevinta Image Optimization
date:   2023-10-23 13:12:00 +0100
excerpt_separator: <!--more-->
---

> Published in [Medium](https://medium.com/adevinta-tech-blog/improving-your-application-performance-seamlessly-using-the-newest-image-formats-9b592c837b59)

The importance of images in connecting users with your products has been proven, so it’s crucial to include them on your website. However if your website takes a long time to load, users are more likely to abandon it - and this can drastically increase your bounce rate and eventually affect your conversions.

If you are able to reduce the size of your images without reducing image quality, then it will have a direct and positive impact on page load speeds and user experience. Join me to see how image formats like WebP and AVIF can help you with this challenge, and how Adevintans can do it seamlessly thanks to YAMS.

*YAMS (Yet Another Media Service) is a media content delivery service provided by Adevinta’s Data & Privacy tribe. More than 20 marketplaces in [Adevinta](https://adevinta.com/) rely on it to deliver 230 million images and videos daily.*

<!--more-->

## What is WebP?

[WebP](https://developers.google.com/speed/webp/) is an image format developed by Google. It encodes images in both lossless and lossy formats, making it a versatile format for any type of visual media and a great alternative to both PNG and JPEG. WebP’s visual quality is often comparable to heavier formats in size. Below is a comparison of a lossy WebP image and a JPEG image:

![JPEG file](/assets/img/1_0_REX2jgmZo-SrZyMl.webp "JPEG format")
*JPEG source*

![WebP file](/assets/img/2_0_TyYjORv9QWX-2Yqz.webp "WebP format")
*WebP source*

The visual differences are nearly imperceptible, but the differences in file size are substantial. The JPEG version on the left weighs in at 1359 KB, and the **WebP version**, on the right, **is nearly 47% smaller** at 720 KB. Not too bad, especially when the visual quality between the two is comparable.

This is one of the main features of WebP: **reduced file size without a perceptible drop in quality**. How much smaller WebP files are than their JPG equivalents varies by a number of factors, but Google [says that they are between 25% and 35% smaller](https://developers.google.com/speed/webp/docs/webp_study).

Another appeal is that the format combines features that no other format has brought together before: incorporating the distinctive benefits of JPG, PNG and GIF extensions. You will have the best of three in one. For example, the ability to add a transparency channel, much like a PNG.

However, unlike its lossless counterpart, you can often get a usable WebP image to around one-tenth the size of its PNG equivalent. This is a real standout use for WebP, allowing more options and features that would otherwise need huge file sizes. In the next example, you can see how a 176 KB PNG has been compressed down to 73 KB - a reduction of 59%.

![PNG file](/assets/img/3_0_T6fcDt9q8qC5n86o.webp "PNG format")
*PNG source*

![WebP alpha file](/assets/img/4_0_jwnfLV4dbwOGwTZ9.webp "WebP alpha format")
*WebP alpha: Source*

Naturally, the next question is *“why are websites using other formats instead of WebP?”*. The reason is that not all browsers support it. Only [80% of the browsers](https://caniuse.com/#search=webp) in use support WebP. It is natively supported in Chrome, Firefox, Opera, Edge and the Android browser. Other browsers don’t have native support yet, although they are adding it in the latest version.

It’s important to mention that WebP is not a replacement for JPEG and PNG images. It’s a format you can serve to browsers that can use it, but you should keep older image formats on hand for other browsers.

Enough with the disclaimers. **Let’s optimise!**

## Converting images to WebP

There are lots of [ways to convert](https://developers.google.com/speed/webp/docs/using) your images to WebP: using WebP Photoshop / GIMP Plugin, using the Node package called [imagemin](https://www.npmjs.com/package/imagemin) or using existing online tools. In order to convert images effortlessly, we use an internal service, **YAMS**.

## YAMS — Yet Another Media Service

![YAMS logo](/assets/img/yams_O8OdkgRKjOzKM_7knJok4A.webp)

YAMS is an Adevinta internal service to store images and get on-the-fly transformations. It’s a mature service storing more than **3.15PB of images** from [leboncoin](https://www.leboncoin.fr/), [Subito](https://www.subito.it/), [habitaclia](https://www.habitaclia.com/), kufar, and all of the [Schibsted](https://schibsted.com/) sites. It **delivers more than seven billion images and videos each month**.

Once you upload your images into the service, you can request a great variety of transformations without creative restraints. This includes resizing, cropping, watermarking, file format conversion, and many more!

YAMS has the ability **to transform the original image into any supported file format on-the-fly** and it supports WebP and AVIF transcoding (from JPEG/PNG to WebP/AVIF and vice versa).

Let’s imagine we have uploaded some images in several formats, and after reading this article we want to deliver them in WebP to improve our page load time. In this case, we just need to create a rule to deliver WebP transformed images. Rules are defined in a well documented JSON-based [rule language](https://yams.mpi-internal.com/documentation/transformation-rules), and they can be named with an alias (in this example *to-webp* and *to-jpeg* will be used):

![to-webp](/assets/img/5_0_HenkRBio_2arJcHE.webp)

![to-jpeg](/assets/img/6_0_XsPbaUOEMUZv4O8X.webp)

To use this rule we just need to build a URL following this pattern:

```
https://cdn.your-domain/api/v1/{bucket-alias}/images/{object-id}[?rule=(rule-id|rule-alias)]
```

As you can see, the last query parameter is the rule used to create the transformation, in our case the previous one to convert any file type in WebP.

Let’s go to the second part, inserting converted images on your website.

## Implementing WebP Support on Your Website

Creating WebP versions of your images can be pretty straightforward as we have seen. On the other hand, showing WebP images on your website can be a bit tricky.

There are many ways to integrate WebP, but the underlying principle of all of them is that, if users’ browsers support WebP, they’ll get a WebP image. Otherwise, they’ll get a JPEG version of the image, all of this happening seamlessly behind the scenes.

The simplest method is encoding the HTML of each image to use a template such as:

```
<picture>
  <source srcset="{YAMS_URL?rule=to-webp}" type="image/webp">
  <source srcset="{YAMS_URL?rule=to-jpeg}" type="image/jpeg">
  <img src="{YAMS_URL?rule=to-jpeg}">
</picture>
```

The `<picture>` element above shows a WebP image in browsers that support it and shows a JPEG (could also be a PNG) when WebP isn’t supported. I think this is the best route for progressive enhancement as it has a fallback image as the backup.

In the example above, we are using YAMS to get the image in the desired format, but you can use the same technique with different versions of your image.

Of course, you can find other convenient ways to do it, for example [setting rules on your server](https://github.com/vincentorback/WebP-images-with-htaccess) or running [javascript on the page](https://scottjehl.github.io/picturefill/).

## What about my mobile apps?

When it comes to supporting native apps, WebP is supported by Android (since it’s made by Google). Lossy WebP images are supported in Android 4.0 and higher, while lossless and transparent WebP images are supported in [Android 4.3 and higher](https://developer.android.com/studio/write/convert-webp). WebP can also be implemented in iOS by using a dedicated library to encode and decode images. The library, called libwebp, is available as precompiled binaries for iOS or as [source code](https://developers.google.com/speed/webp/download).

It’s worth highlighting that everything we have shared about WebP could be meaningful to deliver the [AVIF format](https://aomediacodec.github.io/av1-avif/). The AV1 Image File Format (AVIF) **produces files that are about 50% smaller than JPEGs** and AVIF even significantly outperforms WebP.

While WebP was compatible with [some users](https://caniuse.com/?search=webp), the AVIF format [is supported by different ones](https://caniuse.com/?search=avif). Newer image extensions (like AVIF) take some months to be widely available for users. So to improve the page speed of your website and the quality of your images for all your users, you should use three different versions of the same image: JPEG, WebP and AVIF.

**How much does it cost?** In our case just a new rule in YAMS to get your pictures in AVIF format.

![to-webp](/assets/img/5_0_HenkRBio_2arJcHE.webp)

![to-jpeg](/assets/img/6_0_XsPbaUOEMUZv4O8X.webp)

![to-avif](/assets/img/7_0_dkjIk_3OZnjd2m4l.webp)

```
<picture>
  <source srcset=”{YAMS_URL?rule=to-avif}” type=”image/avif”>
  <source srcset=”{YAMS_URL?rule=to-webp}” type=”image/webp”>
  <source srcset=”{YAMS_URL?rule=to-jpeg}” type=”image/jpeg”>
  <img src=”{YAMS_URL?rule=to-jpeg}”>
</picture>
```

## Wrapping up

They say a picture is worth a thousand words and I totally agree with that. To provide rich content, images are key. But today’s websites know that every millisecond impacts on the user’s experience. So, page load time is one of the first things to improve. WebP and AVIF could bring a substantial improvement on the perceived and real page load times for your site.

Managing images can be challenging because supporting the same image with different sizes and formats for adapting it to every device requires significant development effort. Still, since images comprise [60 to 65 percent](https://httparchive.org/reports/page-weight) of the average website, the savings are significant and therefore automating the process makes a lot of sense. Luckily all of **this can be done on-the-fly using YAMS**, so Adevintans can benefit from the advantages that WebP and AVIF provide without requiring additional development effort on their side to support it.
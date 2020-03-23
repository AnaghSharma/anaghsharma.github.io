---
layout: post
title: Color Science for Digital Design
description: Understanding color profiles and how they affect your design document. Learn about what is a color space, gamut and color profile management in this article.
imageurl: assets/images/sm-previews/pre-home.jpg
keywords: design, colours, colors, colour models, color models, color space, gamut, rgb, hsb, hsl, srgb, display p3, color profile
author: Anagh Sharma
read-time: 6m 56s
permalink: '/blog/color-science-for-digital-design/'
comments: true
---

### Understanding color profiles and how they affect your design document.

<br>
Assessing the difference in the colors you see while designing and what you get after exporting assets is crucial. Professional design tools give you the authority to select color profiles. Have you ever heard about sRGB, Display P3, Adobe RGB or L\*a\*b\*?   In the [last article]({{ site.url }}/blog/rgb-vs-hsb-vs-hsl-demystified/){:target="_blank" aria-label="Go to the article"}{:.active .font-medium}, I tried to describe the different color models in brief. In this article, we will head towards unveiling the mysteries of color profiles.

<br>
###### **COLOR SPACES**
Before coming to color profiles, there are some terms that I would like to explain. In the [last article]({{ site.url }}/blog/rgb-vs-hsb-vs-hsl-demystified/){:target="_blank" aria-label="Go to the article"}{:.active .font-medium}, I mentioned how different color models are represented geometrically, to be specific -
* {: .lh-copy }RGB by a cube
* {: .lh-copy }HSB by a cone
* {: .lh-copy }HSL by a bi-cone

These geometric shapes are actually the color spaces. The term ‘space’ is used because of the fact the all the colors that can be represented by the model are present in that space. For example - in RGB, any triplet that represents a color is a coordinate in the cube. Imagine this space as a physical space in real life and now you are in this giant cube full of different colors (of course you can breathe). Any point in this space is a color that can be represented by the RGB triplet (r, g, b).

But now the question arises - why are there different geometrical shapes - cube, cone, bi-cone? They are different because each of them is derived from different characteristics and relationships among these characteristics. RGB is derived out of just Red, Green and Blue colors. HSB/L are derived out of Hue, Saturation, Brightness/Lightness. The need for the latter arose because of the way humans perceive colors.

<br>
###### **CIE CHROMATICITY DIAGRAM**
The human eye can perceive colors up to a certain extent. Scientists in the early 20th century conducted experiments and plotted a color space perceivable by the eye. All visible colors are in a **horseshoe** shaped cone in the X-Y-Z space which when projected to an X-Y plane comes out to be like following -

![CIE Chromaticity Diagram]({{ site.url }}/assets/images/posts/color-science/cs-1.jpg){: .slb }

Notice the pure Red, Green and Blue lying on the edges. Inside this shape, we have all the possible combinations of these colors. This diagram helps us in understanding the different gamuts that are being used today such as sRGB, Display P3, Adobe RGB, etc. since they all fall inside this geometric shape.

<br>
###### **GAMUT**
The term Gamut is associated with display devices. The gamut of a display device corresponds to the range of the colors that it can render. The gamut of a display device is usually smaller than the full range of colors that can be perceived by humans. This is because of the hardware limitations as the display devices can not produce the pure Red, Green and Blue colors. So if someone inputs a color that is outside the gamut, the device would show a somewhat similar color that lies inside the gamut.

There is just a slight difference between a color space and gamut. Gamut is the subset of colors within a color space. A color space can have so many colors but gamut is the subset of those colors that a display device can produce. This is also the reason why sRGB, Display P3, etc. are also referred to as color spaces.

<br>
###### **COLOR PROFILE MANAGEMENT IN CURRENT DESIGN TOOLS**
Understanding all these jargons can be a bit perplexing. Yet, they help us in understanding how the current design tools offer color profile management. Color profile is the set of data that is embedded with images so that the final medium can interpret the colors accurately. The color profile also determines how the colors are displayed on the screen. I’ll be discussing some of the current design tools and the provision of color profiles in them.

<br>
**SKETCH**

Sketch can render documents in two color profiles — sRGB and Display P3. By default, Sketch uses an Unmanaged color profile which means that it uses your system’s default color profile. Although it is good performance-wise, however when you export assets, the colors may look different from what you see on your Mac. Sketch offers a concise guide for deciding [when to choose a color profile or go Unmanaged](https://www.sketch.com/support/troubleshooting/color-management/){:target="_blank" aria-label="Go to the article"}{:.active .font-medium}. The simple rule of thumb is to choose the color profile based on the final medium on which your work will appear. You can edit the color profile using the **cmd(⌘)+shift+k** shortcut.

![Color profiles in Sketch]({{ site.url }}/assets/images/posts/color-science/cs-2.jpg){: .slb }

**sRGB Color Profile**

The color profile that should be used when designing for Web or wide variety for display devices. sRGB is a standard that has been in use for quite a while now. This is the most used profile supporting a wide variety of devices, hence it is recommended that you set this as your default color profile in Sketch preferences. This profile is appropriate for the situation when you want to perfectly match the colors that you see in Sketch with the colors in the exported assets.

<br>
**Display P3 Color Profile**

Thanks to the recent advent in technology, display devices can now render more vibrant colors, colors which are outside the sRGB gamut. Display P3 was created by Apple and it covers a wider area of the CIE Chromaticity diagram than the sRGB gamut and hence able to render a wider range of colors especially deeper reds and greens.

![Display P3 versus sRGB color space]({{ site.url }}/assets/images/posts/color-science/cs-3.jpg){: .slb }

You can set this color profile if you want to target devices that use Display P3 color space - newer Mac, iOS & Android devices, and make use of all these additional vibrant colors. Two points that you must keep in mind while designing for Display P3 -

1. {: .lh-copy }You need a screen that supports Display P3. Otherwise, you won’t be able to see these vibrant colors while designing.
2. {: .lh-copy }While exporting, do not check ‘Save for Web’ as it will discard the color profile information. Without the explicit embedded color profile, most systems assume the asset to be in sRGB.

The real challenge comes in when you want to update the color profile of an existing document. Sketch offers two methods for the same - 
* {: .lh-copy }**Assign** - In this method, the underlying RGB values remain the same but the colors might appear slightly different because the same RGB values can point to different colors in different color spaces. This method is most appropriate when you want to preserve the RGB values of your brand. This method is a non-destructive operation is Sketch and you may undo as many times as you want. Following is an example where the same hex code value points to a vibrant red in Display P3 (I hope the difference is noticeable on your display).

![Assign method in color profile management]({{ site.url }}/assets/images/posts/color-science/cs-4.jpg){: .slb }

* {: .lh-copy }**Convert** - This method is the opposite of Assign, and keeps the appearance of the colors same for which it converts the underlying RGB values accordingly. This method is most appropriate when you want to preserve the appearance of the colors. This method is a destructive operation and hence you should probably backup your document before converting.

<br>
**FIGMA**

At the time of writing, Figma does not support the Display P3 color profile. By default, Figma -

1. {: .lh-copy }Uses sRGB in the browser
2. {: .lh-copy }Uses Unmanaged in the Desktop app to use your system’s default color profile just like in Sketch. The Desktop app also provides the option to switch to sRGB.

![Color profile management in Figma]({{ site.url }}/assets/images/posts/color-science/cs-5.jpg){: .slb }

<br>
**AFFINITY DESIGNER**

Affinity Designer provides a lot of color profile options to work with. Depending on the color format of the document (RGB, CMYK, etc.), there are a plethora of options to choose from. For digital design (color format - RGB), it gives you the following options -

![Color profile management in Affinity Designer]({{ site.url }}/assets/images/posts/color-science/cs-6.jpg){: .slb }

<br>
###### **WRAPPING UP**
Phew, it’s the wrap-up. If you do not understand all of this at once and find it complicated, it’s fine. I would suggest you go through my [previous article]({{ site.url }}/blog/rgb-vs-hsb-vs-hsl-demystified/){:target="_blank" aria-label="Go to the article"}{:.active .font-medium} first and then come back to this one. If you still feel perplexed, there is some really good content on Khan Academy about colors. The course ‘Pixar in a Box’ by Pixar Animation Studios contains an intriguing section - Color Science (hence the title here 😉). Go through it and the other references for detailed information about colors and color profiles.

Next, I’ll be sharing how to generate an accessible color palette for any of your project or even for your Design System.


<br>
<strong>// KEEP MAKING.<strong>

<br>
<br>
###### **REFERENCES**

1. {: .lh-copy }[Pixar in a Box](https://www.khanacademy.org/partner-content/pixar){:target="_blank" aria-label="Go to the article"}{:.active .font-medium}
2. {: .lh-copy }[CIE Chromaticity Diagram](https://users.cs.cf.ac.uk/Dave.Marshall/Multimedia/node187.html){:target="_blank" aria-label="Go to the article"}{:.active .font-medium}
3. {: .lh-copy }[Get Started with Display P3 - WWDC 2017 - Videos - Apple Developer](https://developer.apple.com/videos/play/wwdc2017/821/){:target="_blank" aria-label="Go to the article"}{:.active .font-medium}
4. {: .lh-copy }[Sketch - What color profile should I use?](https://www.sketch.com/support/troubleshooting/color-management/){:target="_blank" aria-label="Go to the article"}{:.active .font-medium}
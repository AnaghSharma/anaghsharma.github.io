---
layout: post
title: RGB vs HSB vs HSL - Demystified
description: Delving into color models and some of the types that are out there. Learn about what is a color model and some of the color models in this article.
imageurl: assets/images/sm-previews/pre-home.jpg
keywords: design, colors, colours, color models, colour models, rgb, hsb, hsl
author: Anagh Sharma
read-time: 8m 09s
permalink: '/blog/rgb-vs-hsb-vs-hsl-demystified/'
comments: true
---

### Delving into color models and some of the types that are out there.

<br>
When I started working as a Designer, I had a vague idea about the color models. I had studied them in college as part of the Computer Graphics subject but never thought that I would be in a situation to explore and use them. When you start your journey as a Designer, there are many articles out there to teach you about the color theory and all, but hardly anyone would explain about color models or the better part of them - how to use the color models. I was familiar with RGB, HSB, CMYK and others, or so I thought, but when I began working on the design system for [Innovaccer](https://www.innovaccer.com){:target="_blank" aria-label="Go to innovaccer.com"}{:.active .font-medium}, I realised that I do not have enough knowledge of the color models to generate a consistent and accessible color palette. If you have come across these color models and are kinda curious about them, read on.

<br>
###### **ONE WORD AT A TIME**
Let's go through some of the jargons that we will be using -

**HUE** - The term used for the *pure colors* which appear in the hue wheel or bar. It is basically THE color when we talk about a color omitting how bright/dark or rich/pale it is.

![Hue Wheel]({{ site.url }}/assets/images/posts/color-models/cm-1.jpg){: .slb }

**BRIGHTNESS** - Umm, it is the brightness of a color. Usually goes from 0 to 100, with 100 being the brightest variant of the color and 0 being the darkest (read — the black color).

**SATURATION** - The richness of a color. Usually goes from 0 to 100, with 0 being the palest variant of the color (read - a grey color) and 100 being the richest variant of the color.

<br>
###### **WHAT IS A COLOR MODEL**
Computers understand binary language i.e. 0s and 1s. Colors are also 0s and 1s inside a computer. But while designing anything digital you do not tell the computer that hey, I want to use 01011101 color. Obviously, we do not use the binary code. Here we use a color model to specify a color in terms of some parameters which in turn will send the 0's and 1's to the display and tell it what color has to be shown for each desired pixel.

Putting it simply, a color model is a system to represent a color. For example, in RGB (0–255, 0–255, 0–255) model, a color can be represented by how much Red, Green and Blue it is.

Similarly, the same color can be represented by some other color system say HSB by depicting what hue it carries (which ranges from 0º to 360º), how much saturated it is and the brightness it has. This type of system is more human-friendly since this is how we perceive colors actually.

Let's go through the 3 color models which are used for various display devices such as monitors, mobiles, etc.

<br>
###### **THE RGB MODEL**
As I mentioned earlier, in RGB (0–255, 0–255 ,0–255) system, a color can be represented by how much Red, Green and Blue it is. This essentially means a color can be represented by the combination of these three primary colors. Each of these Red, Green and Blue can range from 0–255 to represent a color.

Graphically, the RGB color model is represented by a cube. You can find more information about it [here](https://www.geeksforgeeks.org/computer-graphics-the-rgb-color-model/){:target="_blank" arial-label="Go to geeksforgeeks.org to read more about RGB color model"}{:.active .font-medium}.

Take an example of the following color -

![RGB Model in Sketch]({{ site.url }}/assets/images/posts/color-models/cm-2.jpg){: .slb }

You can clearly see the R, G and B values here. You can alter these values to get different colors. Although it is one of the most used models, the problem with this model is that if you are generating variants of a color and want a lighter/darker or paler/richer shade you do not know which value out of R, G or B you should alter. Thanks to some geniuses, we have the HSB and HSL color models.

<br>
###### **THE HSB MODEL**
So there is this other model out there which deals with the Hue (H), Saturation (S) and Brightness (B). If you have never heard about it or never used it, don't worry. I am going to cover what it is and how it can be used. This model was conceived to represent colors in a somewhat human-friendly way and not a combination of primary colors - Red, Green and Blue.

In this model, a color can be represented by the hue it carries, how much saturated it is and the brightness it has. Let's take the example of the same color as we did with the RGB model -

![HSB Model in Sketch]({{ site.url }}/assets/images/posts/color-models/cm-3.jpg){: .slb }

The H(ue) parameter takes value from 0 to 360, whereas the S(aturation) and B(rightness) parameters take value from 0 to 100. This model is also alternatively known as HSV where V stands for Value and ranges from 0 to 100.

Seems uncomplicated, eh? Hold my beer. Graphically, the HSB color model is represented by a cone - yes, just like the ice-cream cone.

![HSB Cone]({{ site.url }}/assets/images/posts/color-models/cm-4.jpg){: .slb }

The Hue lies on the circumference of the cone and this is why it takes value from 0º to 360º. The saturation lies along the radius of the base whereas the Brightness or Value lies along with the height of the cone. Now let's have some observations - 

* {: .lh-copy }Saturation is 0 at the centre of the base and goes up to 100 at the circumference.
* {: .lh-copy }Brightness is 0 at the tip of the cone and goes up to 100 at the centre of the base.

If we look at the combinations here -
* {: .lh-copy }At the centre of the base - Saturation is 0 while the Brightness is 100 which gives us the color - **White** irrespective of the hue.
* {: .lh-copy }On the opposite side - at the tip of the cone, Saturation is 0 and the Brightness is 0 too which gives us the color - **Black** irrespective of the Hue.

Interestingly, if only the Brightness is 0 (at the tip of the cone) the color is going to be Black irrespective of the Hue and the Saturation. Easy to remember, if there is no Brightness the color is going to be Black (think of it as the darkness). Sketch color picker makes it really easy to explain -

![Brightness and Saturation ranges in Sketch for HSB model]({{ site.url }}/assets/images/posts/color-models/cm-5.jpg){: .slb }

Intriguingly, White color is only at the top left corner while the Black color is on the entire floor. This implies that here White color is not entirely the opposite of Black.

HSB model is an underused model basis on what I have seen. If you have never used the model, try to use it with some hit and trial. You'll be surprised to know how easy it is to generate different variations of a color. All of the parameters (Hue, Saturation and Brightness) of the HSB model can come handy when you are generating the variations.

<br>
###### **THE HSL MODEL**
This one is somewhat complex and often confused with the HSB model. L in HSL stands for Lightness while H and S are the same. Graphically, the HSB model is represented by a cone while the HSL model is represented by a double cone (bi-cone). Go play with this [3D model](https://sketchfab.com/3d-models/hsl-color-space-bicone-4b80b8cef67a44998b8fec292f7865d1){:target="_blank" aria-label="Go to sketchfab.com to explore the 3D model for HSL"}{:.active .font-medium} to get to know how much similar and different it is to the HSB model.

![HSL Bi-cone]({{ site.url }}/assets/images/posts/color-models/cm-6.jpg){: .slb }

Yeah, the above image is quite intimidating and as I said before - complex. There is a subtle difference between HSL and HSB. Since it is a bi-cone -
* {: .lh-copy }The Lightness is exactly half, i.e. 50 at the centre of the base, unlike HSB where Brightness is 100 at that point.
* {: .lh-copy }Lightness is 0 at one tip of the cone whereas it is 100 at the other tip of the cone. This makes the color White laying at the opposite end of the Black.

To elaborate this using above image, Lightness is 100 at the top tip of the cone and hence the color is White irrespective of the Hue and Saturation whereas Lightness is 0 at the bottom tip and hence the color is Black irrespective of the Hue and Saturation.

Hence, the only difference is that in HSB, 100% Brightness can give you the White color only when the Saturation is 0 while in HSL 100% Lightness will give you the White color irrespective of the Saturation.

Look at the following images of the color Picker from Sketch. The left one is using the HSB model and the right one is using the HSL model. Notice the slight difference between the color range here. Also, at the extreme top right, the Brightness is 100 in HSB while the Lightness is 50 in HSL which aligns with our earlier observation of the bi-cone image.

![HSB vs HSL in Sketch]({{ site.url }}/assets/images/posts/color-models/cm-7.jpg){: .slb }

<br>
Take the example of Affinity Designer, which provides HSL color wheel unlike Sketch to alter these values -

<iframe src="https://player.vimeo.com/video/363287332" width="100%" height="508" frameborder="0" allow="autoplay; fullscreen" allowfullscreen></iframe>

<br>
The wheel represents the Hue since it goes from 0º to 360º. The Saturation and Lightness can be altered from the triangle portion. These two color pickers are examples of how the 3-dimensional cone space has been transformed and represented into a 2-dimensional plane. If you are looking at this kind of color picker for the first time, it can be overwhelming and confusing. I would like you to start playing with it so that you are able to understand how changing Hue, Saturation and Lightness brings variations in the color. I'll also be sharing how I used HSL color model to generate a color palette for the design system at [Innovaccer](https://www.innovaccer.com){:target="_blank" aria-label="Go to innovaccer.com"}{:.active .font-medium}.

<br>
###### **COLORING UP**
If you have reached this far without banging your head against the wall, congratulations. We are doing great here. Soon, I'll be sharing how to generate a color palette using the HSL color model. I hope all of this *theory* is still there with you when I walk you through the *practical*.

<br>
<strong>// KEEP MAKING.<strong>
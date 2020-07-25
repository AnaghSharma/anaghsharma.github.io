---
layout: post
title: Creating a hyperlink control for Xamarin.Mac
description: While developing a product, there can be a requirement of using a custom control i.e. a control which is not offered as a part of the SDK. Developing such controls can be quite intimidating. Learn how to build a custom hyperlink control for Xamarin Mac in this article.
imageurl: assets/images/sm-previews/pre-home.jpg
keywords: design, side projects, macos, cocoa, xamarin, custom control, hyperlink, user interface
author: Anagh Sharma
read-time: 4m 12s
permalink: '/blog/creating-a-hyperlink-control-for-xamarin-mac/'
comments: true
---

###### **OVERVIEW**
While developing a product, there can be a requirement of using a custom control i.e. a control which is not offered as a part of the SDK. Developing such controls can be quite intimidating. I remember circa 2013 I had a really hard time developing custom controls for my Windows Phone apps. Even when I was able to do so, those controls were not reusable. It was a complex process since I did not know much about the how-to. I used to rely on dev articles and of course the good old [stackoverflow.com](https://www.stackoverflow.com){:target="_blank" aria-label="Go to stackoverflow.com"}{:.active .font-medium}. With this article, I tend to give back to the dev community so that it could help someone just like someone's article did back in the days.

<br>
###### **THE NEED FOR A CUSTOM CONTROL**
While developing [Carol](https://github.com/AnaghSharma/Carol){:target="_blank" aria-label="View Carol on GitHub"}{:.active .font-medium} I had the requirement of a hyperlink text control. I wanted to use it on the About window. Could not find the same in the AppKit, so I decided to build a custom one.

![The About window using the custom hyperlink control]({{ site.url }}/assets/images/posts/hyperlink-1.jpg){: .slb }

<br>
###### **THE HOW-TO**
Building a hyperlink text control for your macOS app in Xamarin is not that complicated. We will go step by step to get it done - 
1. {: .lh-copy }Add a new class to your project and name it accordingly. For the article purpose, we will be using the name - ```HyperlinkTextField```.
2. {: .lh-copy }Inherit from ```NSTextField``` and put a ```using AppKit``` directive on top.
3. {: .lh-copy }Since we will be using this control through Xcode, we need to make sure that our class is visible there at the design time. To do so, use the following attributes - 
```[Register("YourClassName"), DesignTimeVisible(true)]```
    * Register("YourClassName") attribute is used to register a class to the Objective-C runtime.
    * DesignTimeVisible(true) attribute makes sure that the class is visible in Xcode at design time.
4. {: .lh-copy }Create three private members viz. 
    ```csharp
    String href;
    NSTrackingArea hoverarea;
    NSCursor cursor;
    ```

    * href will be used for the link element of the hyperlink. The rest will be used for changing cursor to pointing hand on hover.
5. {: .lh-copy }Create a String property Href which gets and sets the value of href. We will also have to use the Export attribute here.
    ```csharp
    [Export("Href")]
    public String Href
    { 
        get 
        { 
            return href; 
        } 
        set => href = value;
    }
    ```
    * {: .lh-copy }Export("PropertyName") attribute exports a property to Objective-C world.


6. {: .lh-copy }Now we need to style the text field so that it looks like a hyperlink. To do this we override the AwakeFromNib() method as below - 
    ```csharp
    public override void AwakeFromNib()
    { 
        base.AwakeFromNib();
        AttributedStringValue = new NSAttributedString(StringValue, new NSStringAttributes()
        { 
            // You can change the color of link after uncommenting the following 
            // ForegroundColor = NSColor.Red,
            UnderlineStyle = NSUnderlineStyle.Single.GetHashCode()
        }); 
        
        hoverarea = new NSTrackingArea(Bounds, NSTrackingAreaOptions.MouseEnteredAndExited | NSTrackingAreaOptions.ActiveAlways, this, null);
        AddTrackingArea(hoverarea);
        cursor = NSCursor.CurrentSystemCursor;
    }
    ```
    * To give the text field an underline, we are using NSAttributedString. You may also change the color of the text.
    * [NSTrackingArea](https://developer.apple.com/documentation/appkit/nstrackingarea){:target="_blank" aria-label="Read more about NSTrackingArea on developer.apple.com"}{:.active .font-medium} is region of a view that generates mouse-tracking and cursor-update events when the pointer is over that region. Here we are tracking the mouse entering and exiting events so that we can update the cursor accordingly.

7. {: .lh-copy }In order to change the cursor to pointing hand on hover and vice versa, we are going to override two methods which is pretty straight-forward.
    ```csharp
    //Method override to change cursor to pointing hand on Mouse Enter (Hover)
    public override void MouseEntered(NSEvent theEvent)
    {
        base.MouseEntered(theEvent);
        cursor = NSCursor.PointingHandCursor;
        cursor.Push();
    }
    //Method override to change cursor back to pointing arrow on Mouse Exit
    public override void MouseExited(NSEvent theEvent)
    {
        base.MouseEntered(theEvent);
        cursor.Pop();
    }
    ```

8. {: .lh-copy }Now we only require one last method which will be used to open the URL on clicking the hyperlink control. This method is also an override.
    ```csharp
    //Method override to open url on click of HyperlinkTextField
    public override void MouseDown(NSEvent theEvent)
    {
        NSWorkspace.SharedWorkspace.OpenUrl(new NSUrl(href));
    }
    ```
    * [NSWorkspace](https://developer.apple.com/documentation/appkit/nsworkspace){:target="_blank" aria-label="Read more about NSWorkspace on developer.apple.com"}{:.active .font-medium} is a workspace that can launch other apps and perform a variety of file-handling services. There is one shared NSWorkspace object per app which has a method named OperUrl. We pass a new NSUrl object intialized by the member href.  

9. {: .lh-copy }That's it. Your hyperlink control is now ready to use. To do so - 
    1. Open Main.storyboard and drag a Text Field object from Objects Library to wherever you want to put the hyperlink. Let's use it on About View Controller.
    2. In the Identity inspector, set the Custom Class to HyperlinkTextField and set the Title.
    3. Set an Outlet with Type set to HyperlinkTextField. Let's name it as AboutLink.
    4. In the respective .cs file, override ViewDidLoad to set the href property of the control -
    ```csharp
    public override void ViewDidLoad() 
    {
            base.ViewDidLoad(); 
            AboutLink.Href = "your link here"; 
    }
    ```
    Build and Run. You should be able to see a working hyperlink control.

<br>
###### **WRAPPING UP**
This is all you need to build a custom hyperlink control for Xamarin.Mac. I have used this control in two of my projects - [Carol](https://github.com/AnaghSharma/Carol){:target="_blank" aria-label="View Carol on GitHub"}{:.active .font-medium} and [Ambar](https://github.com/AnaghSharma/Ambar){:target="_blank" aria-label="View Ambar on GitHub"}{:.active .font-medium}. You can access the [source code here](https://github.com/AnaghSharma/Carol/blob/master/Carol/Controls/HyperlinkTextField.cs){:target="_blank" aria-label="Explore the source code on GitHub"}{:.active .font-medium}. Let me know if you need some help or think this artcle can be improved in one way or the other. 

<br>
<strong>// KEEP MAKING.<strong>
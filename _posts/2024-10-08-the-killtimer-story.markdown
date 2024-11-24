---
layout: post
title:  "The KillTimer Story"
date:   2024-10-08 11:08:45
categories: development storytelling
excerpt_separator: <!--more-->
comments: true
feature-img: "/assets/ktweb1.png"
---

When I was a teenager, I wrote a small, but popular, [AOL add-on](https://github.com/readme/featured/aol-programming-culture), called KillTimer. In fact, the web page [still exists](http://members.tripod.com/~cbajgier). This is remarkable since I've had no access to the site for over twenty years and didn't keep with any updates. Apparently [Lycos](https://www.lycos.com), who now owns Tripod, found a way to inject it with enough ads to keep it living forever.

My family purchased our first computer in late 1996 and we got on the internet, via America Online, the year afterward. Getting connected to something broader than my then cloistered existence was a wondrous thing. This was right around the time that AOL went unlimited for a flat monthly fee, bringing a surge of new customers, like ourselves, that their [infrastructure was not prepared to handle](https://time.com/vault/issue/1997-02-10/page/56/). 

In the days of dial-up internet, this meant that you'd sit and wait for your modem to connect as it cycled through busy signals. In response, AOL started instituting timed log-offs for customers who were "inactive" on the network. This was the Netflix ["Are you still watching?"](https://www.howtogeek.com/685919/why-netflix-asks-are-you-still-watching-and-how-to-stop-it/) message of the day, and someone would have to respond to a popup window prompt in time to avoid getting logged off. Of course, this wasn't an accurate thing, and completely disregarded whether bandwidth was being used to complete a long download.

![AOL Prompt](/assets/TIMER.GIF)

And so, a marketplace sprung up for add-ons that would monitor for popup window and respond in time -- usually shareware, written in Visual Basic with an unreliable "SendKeys" way of responding. I recall how this struck me. A large corporation makes a play to quickly grow before they could fully understand the consequences, finding themselves unable to deliver the value that customers expected. They put measures in place after the fact that dilute this for their customers, leaving them to recover what they can through paid solutions for a manufactured problem. As a kid from a poor family struggling with the basic subscription costs to AOL, this felt wrong and had me wondering what it would take to write an add-on of my own.

<!--more-->

### The Development

My programming knowledge at that time was primarily self-taught. The seed was planted in my high school, where I learned typing alongside GW-BASIC on the outdated computers there, but afterward I [relied on books](/development/storytelling/2014/04/01/the-bookshelf.html) to teach myself Visual Basic, C, and Delphi. Some of these books came with old or limited versions of compilers. One, [Learn Visual C++ Now](https://archive.org/details/learnvisualcnowt0000andr), promised to show me how to develop for Windows using the Microsoft Foundation Classes (MFC). At this time, I'd only written C programs for DOS.

For whatever reason, I couldn't grasp the mental model that object-oriented programming at that level required. There was an example within the book of a traditional C Windows "Hello, world!" program, meant to showcase the cryptic nature of engaging the Windows API directly and all the overhead involved. This example, with an ongoing message loop, I could understand, and from this single example I was able to write the first version of _KillTimer_.

![KillTimer screenshot](/assets/screenshot.gif)

KillTimer used the Windows API to identify the AOL frame and monitor for the window using the handle of the window. When detected, it responded with a button click message sent directly to that window to dismiss it, emulating the customer's response. To make this seem more "human", I varied the response times to the popup. There was no interface, other than the presence of the icon in the system tray. Eventually, I added features to combat other nuisances within the AOL experience, including one to rapidly dismiss IMs (Instant Messages) in the case of a "punting" attack. 

![Initial KillTimer Homepage](/assets/ktweb1.png){: .galleryThumb}

There were three compelling advantages that KillTimer had over similar programs: it was freeware, much less resource-intensive. and more reliable. I set up a website with a download link and promoted it via different AOL and Usenet forums, and eventually via [LinkExchange](https://en.wikipedia.org/wiki/LinkExchange). I was participating in the AOL beta testing program and shared with my community of testers -- this also gave me the access I needed to keep the software current with new AOL versions, in case any of the identifying characteristics of the timeout dialog changed.

```cpp
    while (FindWindowEx(AOLTimerhWnd, NULL, "_AOL_Button", "OK") != 0)
        {
        if (RandomWait)
            {
                int a;
                srand((unsigned)time(NULL));
                do
                    {
                    a = rand();
                    } while (a > 1000);
                Sleep(1000 + a);
            }
            else
                Sleep(1000);
        if (FindWindowEx(AOLTimerhWnd, NULL, "_AOL_Button", "OK") != 0)
            SendMessage(FindWindowEx(AOLTimerhWnd, NULL, "_AOL_Button", "OK"), WM_CHAR, 13, NULL); // Presses the button, therby closing the Timer window
        Sleep(1000);
        }
    if (FindWindow("_AOL_Palette", NULL) == 0)
        {
        if (PlaySounds)
            MessageBeep(MB_ICONASTERISK); // Plays a sound to inform us it closed the window
```
<figcaption>A sample of KillTimer's code</figcaption>

### Supporting KillTimer

My aims for creating and releasing KillTimer must've been embedded deep within my subconscious. When I think back, I can't think of any other reason other than I had created something that solved a problem better than anything else available. This didn't seem right to keep to myself, and I was inspired, as I still am, by the concept of freely available software. I submitted KillTimer to the free software directories to raise its profile, such as [TUCOWS](https://www.tucows.com/about-us/history).

What I could glean from those sites, as well as the rudimentary website statistics I had access to in the day, was how many people were using KillTimer and where it stood against its competition. 

![KillTimer Listing on NONAGS.com](/assets/KillTimer6Ducks.png){: .galleryThumb}

I set up an additional e-mail address through a free service, Juno, to respond to requests for help. Simple polls gave me an view into which features were meaningful (the most requested: a version for Windows 3.1, an operating system I've never used) and I kept to those which most aligned to the philosophy of KillTimer and preserved the footprint I was going for.

### Recognition for KillTimer

KillTimer was listed in the resource appendix of the early editions of [eBay for Dummies](https://www.amazon.com/eBay-Dummies-Roland-Woerner/dp/0764506102), and it was a thrill to see mention of it in print. I still remember visiting Waldenbooks with my father, retrieving a copy from the shelf and browsing for its entry toward the back.

![KillTimer as Kim's Shareware Pick of the Week](/assets/ktpick.png){: .galleryThumb}

It also was highlighted on the [Kim Komando Radio Show](https://www.komando.com/) as a _Shareware Pick of the Week_, which brought an influx of new users into the fold and was a memorable time in itself.

### KillTimer X and KillTimer Pro

For a time toward the end, I was working on updates to the main KillTimer program alongside its successor, _KillTimer X_. KillTimer X was intended to be sort of a final edition, with a new, clean code base that would incorporate some of the better practices I've learned over time. It would also have an actual user interface for configuring options.

![KillTimer X screenshot](/assets/kttray.gif)

The biggest feature, though, was an option to automatically respond to new IMs should the user be away. This wasn't yet natively built into the AOL messenger service (though would be an integral part of the [nostalgic AIM experience](https://kyleseeley23.itch.io/emilyisaway)). This worked, and I used it to handle my own incoming messages for the time it was in active development.

![KillTimer Pro screenshot](/assets/KillTimer16bit.gif)

_KillTimer Pro_ would be a shareware program, relenting to the needs of those who required a 16-bit version of the program. Because there was no system tray in Windows 3.1, the interface was a stubby movable ribbon of sorts with the KillTimer icon and title. This was being developed with Delphi, which increased the end executable size considerably (since all Delphi component dependencies were compiled, instead of requiring a separate runtime library). To operate the same way KillTimer did to respond to the idle popups, I had to wrap the needed Windows API calls in special functions, as they couldn't be accessed directly. 

Neither of these editions would be completed, though. KillTimer 4.9 would be the last.

### The End

There was no concrete decision to stop developing KillTimer, but working on it did eventually take a backseat as I faced the challenges that come as one approaches adulthood. When I first got online, the computer and the internet was my gateway to the world. I was largely signed out of school and spending the majority of my time alone in my room. The internet communities I found were my only source for social interaction outside of my family, and programming was my focus. That changed over the course of time.

The problem KillTimer solved wasn't long-term, either. Even though AOL kept the idle popup prompt for years after they remedied their network usage issues, broadband was on the horizon and the proprietary AOL experience was starting to decline.

In addition, I started to frequently encounter angry emails from people who were scammed by bad actors on eBay who were charging for KillTimer. With my goal of keeping it free and accessible for everyone, this created a feeling of moral injury that I had trouble getting past. Exploring charging for the program myself, to shut this activity down with a legitimate shareware licensing model, was a cynical exercise I had no energy for.

### The Impact

KillTimer gave me some unique exposure. These were the ["dot-com" days](https://www.historynewsnetwork.org/article/the-internet-at-50-how-the-dot-com-bubble-burst), and every so often I fielded calls from internet startups that would try to recruit me, each of which destined for [fuckedcompany.com](https://en.wikipedia.org/wiki/Fucked_Company) when the initial boom subsided. It gave me, an insecure kid, the chance to peer into some of the hype and excitement the business world of software had to offer. I was too intimidated by the prospect of leaving my home to pursue any of this seriously, and it made it even more clear that I needed to build up to my independence by enrolling in college first. 

In hindsight, and through the lens of the [digital product management](https://soberproduct.com) work I do professionally, the things I did intuitively as a teenager to build, market, and support KillTimer still form the core of how I operate today. The reasons why I launched it, the disempowering style of problem I tried to help through my efforts still resonate within me. And the experience is one of many that equip me for the work I want to do now -- combating extractive patterns in tech products and industry.
---
created: 2020-06-28T11:40Z
title: WWDC 2020
type: page
updated: 2020-06-28T11:40Z
---

Commenting on contemporary announcements is an abnormal writing project for me. As an Apple user, [WWDC](https://en.wikipedia.org/wiki/Apple_Worldwide_Developers_Conference) is an event that I have always followed, as I consider it the most important yearly event for my personal technological world. For the next year, Apple's platforms are defined by what is announced and what one can read in between the lines to deduce.

WWDC is also the event that makes me consider whether I want to look at other platforms as a possible escape route from Apple land. I am and have been happy with macOS since I started using it, but given how large Apple has become over the past decade, there are back-of-the-mind worries that the Apple experience will suffer due to how much ground they cover. WWDC's ability to show where the platforms are headed for the next year is the perfect time to evaluate if I ever did want to switch to another platform, as I could not make any changes to my current workflow and move things over to a new platform piece-by-piece, all before the current Mac experience is worsened.

That said, while this worry is present, WWDC has always made me feel good about staying with the platform.

## The WWDC 2020 Format

Before getting into the technological details that I found important this year, I have one specific thought about the format that Apple used for WWDC: this pre-recored format is an improvement over previous years' live recordings.

Previous WWDC talks were conducted as keynote presentations before a live audience. Much like how I have enjoyed the format of late-night shows much more without the audience, pre-recorded WWDC sessions have a much faster flow than live sessions. Pertinent information can be moved to quickly, and there is no filler content to make each talk last at least a half hour. A lot of sessions this year were under 30 minutes, with a few being less than 10 minutes long. The quality of production was high, allowing the presenters to do multiple takes until what they said was said in a way to be best understood.

It is unlikely that Apple will run the event in this manner again, unless the coronavirus pandemic is still present next year, but all the same, I wish they would keep the format for those of us who have no interest in attending in person.

## Apple Silicon

By far, the biggest announcement this year was Apple's announcement to moving the Mac line to the [A-series of chips](https://en.wikipedia.org/wiki/Apple_Silicon).

My first Apple computer was a [PowerBook G4](https://krueger.report/technology/past-computing-devices/), one of the last Macs to use the PowerPC architecture. The platform was still new to me, so adjusting back then was easier, as experimentation with new applications was something I was already doing, and I had yet to form any strong attachment to specific tools. Rumors of Apple transitioning to using their own [A-series of ARM CPUs](https://en.wikipedia.org/wiki/Apple_Silicon) has been around for years, which has always given me mixed feelings, since it was hard to know exactly what another such transition would entail.

The way that Apple is handling this transition mirrors how they did the PowerPC to Intel transition, which eases most concerns that I have. The backbone of this approach is Universal 2, a new version of [universal binaries](https://en.wikipedia.org/wiki/Universal_binary) from the Intel transition, and [Rosetta 2](https://en.wikipedia.org/wiki/Rosetta_(software)), an emulator for translating x86 code to the ARM instruction set.

Rosetta 2 is interesting, since it is taking a much smarter approach to translation than the original Rosetta did. Rosetta 2 will translate an app either when it is first installed or when it is first run, depending on the source of the application's install. This will make installation or first run slower than before, but should give vastly improved performance on subsequent uses of the application. It is able to translate code live should the need arise, useful for interpreters that do not use pre-compiled code.

Of note is that Apple is not allowing Rosetta 2 to be used for all functionality. Particularly, kernel extensions and hypervisor modules will not work. Both of these fall into the realm of tasks that would have massive performance loss if translated, or lead to potential bugs due to working with such low-level hardware functionality. Apple's [hypervisor framework](https://developer.apple.com/documentation/hypervisor) will be compatible with virtual machines that are compiled for [AArch64](https://en.wikipedia.org/wiki/AArch64), so running Linux in a virtual machine is still possible. It is unknown if the ARM edition of Windows 10 will run in this manner.

Apple showed off Rosetta 2 using [Parallels](https://en.wikipedia.org/wiki/Parallels_Desktop_for_Mac) and the [Unity game engine](https://en.wikipedia.org/wiki/Unity_(game_engine)). Both were impressive results, and Parallels working as it did gives me hope that I will not have to adjust what I use on my Mac that heavily.

New consumer hardware was not announced. Apple's Developer Transition Kit is the A12Z, used in the current generation iPad Pro, inside the enclosure of a Mac Mini. Not ideal hardware, but the same kit used during the Intel transition was a Pentium 4, a chip that Apple never used in any retail product.

The A12Z does give an idea of what that hardware will look like. For the past few years, Apple has used a CPU architecture that uses "efficient" and "performance" cores. Apple was explicit in the WWDC sessions that this will be coming to the Mac as well, although it will be something that is largely controlled by the operating system. For desktop Macs, there won't be as much need for the "efficient" cores for power reasons, although thermal needs might keep them around. But the mix of cores will shine on laptops.

This is one area where I have some trepidation. Apple's current CPUs are performant with Intel's in single-core performance. Multiple cores would allow to scale up to be on equal grounds, so an overall CPU regression would be surprising. The big unknown is in GPU performance. Apple's GPUs are great in the phone and tablet space, but Apple has yet to prove if they can create anything even remotely close to what AMD offers. And as of my writing this, there is no official word one way or the other as to whether AMD GPUs will be supported on systems running Apple's CPUs.

Another area of concern for me is the announcement that iPadOS apps can run on macOS without needing to be recompiled. This is a feature specific to Macs running the A-series of chips, and not Intel Macs. My fear with this move is that developers will use it as an excuse to not create proper Mac ports, and just let the iPadOS versions of their apps run unmodified. I searched out a few examples of what this looks like, and the results are not always great. I have a strong dislike for Electron apps as they do not feel native to the Mac experience, and these iPadOS apps feel the same way. The Mac ecosystem has long had developers who go through the proper effort of porting their apps to the Mac, and those apps should remain. This just opens the potential for there to be a lot of [shovelware](https://en.wikipedia.org/wiki/Shovelware) present on the platform.

The plans that Apple has laid out for this transition look promising, and the potential for custom solutions for the Mac platform could make for even better machines. As someone who loves the Mac Mini line of computers, this is of particular interest to me, as these machines have the most to gain from Apple CPUs compared to the rest of the desktop line. That said, I will not be getting the first generation of Mac Mini running these chips, or possibly not even the second generation. My current Mac Mini has a lot of life left in it, and I will wait until the true limits of external monitor support is known for the new GPUs.

## macOS 11 Big Sur

Rest in peace, OS X.

The macOS announcements this year centered around two things: a design overhaul, and a greater emphasis on cross-platform frameworks.

The new macOS design language brings the look closer to the current iOS look, with the exception of iconography. Icons are using a design-style that has been called "neumorphism", which is a take on the old skeuomorphic design of having digital interface objects mimic the look of real-life objects. The classic example of this on Apple platforms is the old version of Calendar.app looking like a physical leather calendar, complete with leather and stitching textures. Neumorphic design aims to look realistic in lighting and shadowing, and with designs similar to real-life objects but not being exactly the same. It is a trend that has been building for the past couple of years, and macOS is now the first operating system to embrace it wholeheartedly.

Of note for myself, since I create custom color themes for the text editors that I use, the native system colors for macOS have been changed to exactly match the RGB values of those same colors on iOS and iPadOS. Now all of Apple's platforms will use the same colors.

The other big change involves improving cross-platform technologies to allow easier transition of iPadOS apps to macOS, and to allow the creation of cross-platform apps from their initial inception. This is accomplished using two different frameworks: Catalyst and SwiftUI.

Catalyst has been around for a year, and the early versions of it were functional but imperfect. Catalyst apps compiled against last year's XCode brought iPadOS apps to macOS, but they did not translate many of the UI idioms to something Mac-friendly. An example of this is Catalyst apps still used the rotating date picker that is used on iPadOS. This year, Apple is both opening more features up to Catalyst, and hooking Catalyst into native AppKit calls so that Catalyst apps look more Mac-like. These improvements look like it will allow Catalyst to be a more viable option for creating a Mac-like experience, but I will still take a wait-and-see approach before I trust its output completely. Of note, Catalyst is being [dogfooded](https://en.wikipedia.org/wiki/Eating_your_own_dog_food) by Apple, as it is being used in the operating system itself: the new Control Center present in Big Sur uses Catalyst for its rendering layout.

SwiftUI was launched last year alongside Catalyst. The improvements for SwiftUI this year are two-fold. The first improvement is expanding out the capabilities of SwiftUI by providing more UI functionality and wrappers for views that were previously limited to AppKit and UIKit. This allows more seamless integration with things such as maps and 3d-rendered views without having to write some translation code. The second improvement is providing an interface where a cross-platform app can be written entirely in SwiftUI, with all UI elements shared if so desired. This is exemplified in the new Xcode project template called "Multiplatform", which creates an app in this manner that will compile to iOS, iPadOS, and macOS targets using the same SwiftUI ContentView. This will mostly apply to new SwiftUI projects and would take considerable effort to translate older projects to this format, but it shows the direction that Apple wants UI development to move towards.

## Beta Plans

Every year, I evaluate which devices will be upgraded when to the beta releases of the operating system. Since each device used differently, stability of the beta plays a large role of deciding the timeline for upgrading.

My iPad is the most disposable device that I use, so iPadOS beta 1 was installed the day after Apple released it. Usability is what I expect from a beta 1: present, but with significant usability and visual issues. The most egregious has been when I woke up the iPad the other day, the wakeup animation was looping repeatedly and at a high rate of speed, requiring me to power cycle the iPad to make it usable again.

macOS is the centerpiece of my technological world, and consequently is the one where stability is the most important factor to upgrading. It does not have to be a perfect experience, just stable. Due to the aforementioned issue with iPadOS, I will be waiting until a later time to upgrade macOS. Since there are not any major new features that I need right away, the public betas are the most likely point for me to upgrade.

My iPhone is not disposable, but I can tolerate buggier behavior from it. Due to my heavy use of CarPlay while driving an electric vehicle, upgrading sooner would let me take advantage of some of the features specific to that usage. Additionally, the new springboard widgets are something I will take advantage of for my personal programming projects, so upgrading will sooner allow me to test those out. Due to the behavior I saw on iPadOS, I will wait a few releases before upgrading, but it will be before the public beta test period.

On watchOS, reliability of health tracking is important, and I do not want to do anything that interrupts that. This will be the only device that I do not upgrade to any beta release, and will wait until the final version is released to the public.

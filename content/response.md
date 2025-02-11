+++
title = "Why are AppImages unpopular. Response comment to reddit post"
date = "2025-02-12"
description = "Cuz reddit comment doesn't accept it"
[taxonomies]
tags = ["Linux", "AppImage", "Flatpak", "Snap", "Containers", "Linux Desktop"]
+++

For context: <https://www.reddit.com/r/AppImage/comments/1hk4xpg/why_are_appimages_not_popular>

The problem is very simple: the design of appimage was developed in the mid-2000s and has remained there. It uses outdated logic where there is a program that needs to be downloaded from the manufacturer's website, which you know in advance, then you need to download the program, grant permissions to run, move it to the desktop folder in the file manager and it will be integrated: the program will appear on the desktop, in the menu and wherever needed, instead of a modern user experience, where the user has a Software Center from where he downloads an application that is automatically integrated into the desktop (by copying the desktop file to the `/usr/share/applications` directory) and updates there when needed.
AppImage has an appstream, although it is not entirely clear why it is needed if AppImage avoids Application Centers that use these files for show info about application
For various reasons, AppImage isolation tools were not supported (I think because they were not integrated into any build system, and the rules for appimage isolation also need to be written like scripts, that is, invent everything from scratch, but this is just my opinion, [Matthew Gordon](https://github.com/mgord9518) probably has a different opinion)

As we said, AppImage does not have its own Software Center because it is believed that AppImage does not need it, although when building an application, appimagetool offers you to add your application to the list on appimage.github.io where half of the applications are no longer used, a third of the supported ones do not have a download button and good data parsing, which is then packed into a json file and Software Centers like AppImagePool were used, but since appimage.github.io is poorly supported, they felt bad and quickly became archieved projects, or like Nitrux SC, for which AppImage is an important part now use AppImageHub.

AppImage maintains compatibility with old build tools, and lazy developers (e.g. electron-builder where the code depends on the appimage-maker package that uses appbuilder-libs that has not been updated for 100500 years, in whose releases lies the old appimage-runtime, older than mammoths and almost the same age as t-rex) do not update scripts for years, as a result, a lump of problems accumulates, developers abandon AppImage and switch to Flatpak

To summarize all of the above, for AppImage to become popular, need make next steps:

1. Native integration into the desktop
2. A reliable build infrastructure, for example, on recipes, with multiple build parameters like repackaging, builds from scratch and more features (by the way, the closest competitor has this part developed best)
3. Update all important existing build infrastructures like electron-builder (it is unlikely that this will happen, but then you need to invest in forks like Reforged), switch to using a static runtime, which will solve a billion problems users (almost a panacea, I even have gimp running on musl without any problems!)
4. Software Center or plugins to existing ones, because Linux users are used to getting applications from there, rather than going to the manufacturer's website

But wait, why are we talking about AppImage? It's simple: it's the BEST thing that's ever happened to Linux packaging (maybe except makeself+mojosetup which helps games and some programs like DaVinci Resolve)

Flatpak is anything but a method of packaging an application, the closest description is something like a way to deploy another Linux distribution inside yours with a GUI and good promotion, and at the same time eat up your entire disk

Snap is a mix of AppImage and Flatpak - it's not one separate git-like file system (like in flatpak) but squashfs, only one with a full distribution, and the second, which your application depends on, everything would be fine but it's mounted at system startup and not on click, so your good computer will turn on for about a minute while it mounts your snap packages. The isolation system is tightly tied to apparmor (solus developers, if I remember correctly, said that in order to provide the same experience as on ubuntu, it is necessary to support about 60 patches for apparmor, which are not always updated with each kernel release) and works well only on ubuntu, and since the format is closed, few users will dare to drag into their system something that is not isolated, it is unclear how it was assembled and who did it

That's basically it. In conclusion, I want to thank all those who are trying to promote and improve AppImage, you are doing an incredibly great job. I could try to call you by name, but your happiness is growing every day. Almost every day I see new projects on appimage and it makes me very happy
---
title: Fedora Silverblue Setup
date: 2023-01-01 00:00:00 +0000
categories: [Tech, Linux]
---

### Introduction

Fedora Silverblue is a Fedora spin that offers an immutable base managed by rpm-ostree.
Here I will present my Siverblue set-up, with the main layered packages I have on top of the base image and some other modifications I have needed both for work and other projects. While this is mainly for my own records, I figured someone could benefit from it, so here we go!

### Layered Packages

- **Visual Studio Code**: While a Flatpak version exists, layering VS Code results in a better integrated application and doesn't require of certain workarounds.
- **Gnome-tweaks**: A MUST HAVE for customizing the GNOME desktop environment. The Extension Manager flatpak pairs with it greatly.
- **gstreamer1-plugin-openh264**: Adding media playback codecs for seamless multimedia experiences.
- **Onedrive**: [OneDrive Client for Linux](https://github.com/abraunegg/onedrive) project, which to my experience has been the most reliable FOSS Onedrive client in Linux.
    - Setup synclist. Config file can remain unset since defaults work. 
- **ZSH**: Current shell of choice.
- **Openssl**: This would be the least important one. Mainly used as a dependency by GSConnect (GNOME extension implementing KDEConnect)

### Shell Configuration

- Install ZSH using `rpm-ostree` and set it as the default shell with the following command: `sudo lchsh $USER`.
- **Oh My Zsh** to manage zsh. I like to go with the **Powerlevel10k** theme and the patched Meslo font.
    - Don't forget to set the it as the default font in your terminals
    - Customize the theme by modifying the `P10k.zsh` file.
- Micromamba is also a great drop-in replacement for conda. Much faster and easier to deploy (install) in cloud environments too!

### Containers with Toolbox and Podman

General notes:

- Utilize Toolbox containers for isolated development environments and easy management of software dependencies.
- Consider using Podman instead of Docker for running containers within Toolbox.

MacOS Virtual Machine: I really wished I didn't have to it, but in my research group we use mac-specific vector editing software for figure making so it's a necessary evil. Note though that, for non collab projets, I have fully moved to SVG files and Inkscape as the editor (and haven't really found any major issues except some tiny quirks).

- Explore the alternative of running macOS applications using the GitHub project [OSX-KVM](https://github.com/kholia/OSX-KVM) or running Docker-based solutions within a Toolbox container.
    - OSX-KVM seemed like the best fit.
    - Follow the optimization guide provided by Sick Codes on GitHub to optimize your virtual machine for Big Sur or other macOS versions.
- Create a general Fedora Toolbox container, install Zsh and Oh-My-Zsh, and set up KVM and associated virtual machine dependencies.

### Misc.

Dropbox: Setup up with the flatpak app. Sadly there is no smart sync functionality so beware of disk usage! 

Also installed (Dropbox nautilus integration)[https://www.dropbox.com/install-linux].
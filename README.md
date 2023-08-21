![](./images/banner.png)

# vmConsole

A free and open-source application that enables you to run [Alpine Linux]
distribution in a virtual machine on your Android device. Thousands of packages
available for installation from online repositories make vmConsole a powerful
tool for software developers, testers, system administrators and just Linux
fans.

This application is built on top of [QEMU] x86_64 system emulator and should
be compatible with majority of devices running Android 7.0 and higher. Your
device is not required to be rooted or have custom firmware installed. KVM
acceleration is not supported meaning that performance will be low.

vmConsole is exactly console, aka "terminal" application. Input and output are
being performed through Xterm-compatible terminal screen. Don't beg for Xorg
or Wayland support.

<p align="center">
  <a href="https://github.com/sylirre/vmConsole/releases/latest">
    <img src="docs/files/get-it-on-github.png" width="256px">
  </a>
</p>

**Proper Linux administration skills are needed in order to use vmConsole!**

Typical use-cases of vmConsole application:

- Exploring the world of Linux =)
- Programming
- Testing software
- Hacking
- Running TOR hidden services
- Crawling / archiving web sites

The most important information about application usage is embedded as MOTD
shown during vmConsole login. Other information is easily discoverable if
you have some mid-level Linux skills. Also there is a [Wiki] which describes
some basics.

It is highly recommended to visit [Alpine Linux Wiki].

<p align="center">
  <img src="docs/files/demo_btop.png" width="256px">
  <img src="docs/files/demo_docker.png" width="256px">
  <img src="docs/files/demo_metasploit.png" width="256px">
</p>

## About project

The main idea of this project is to combine a terminal emulator, good Android
port of [QEMU] and a tiny, but production-grade Linux distribution. Think of
it as of a headless virtual PC that can run all command line software available
on normal computers. So far the vmConsole works much better than analogs like
[Limbo PC] or [UserLAnd].

vmConsole is based on [Termux]. Many GUI elements and terminal features are
forked from it. The source code is distributed either by same or compatible
license (GPL v3.0). Please consider this when forking vmConsole app.

Since this is more a personal project, I really do not accept pull requests or
feature suggestions. Though you can report issues like app crashes or other
runtime issues via the bug report form. Also I may do Git rebase or change the
APK file delivery way at any time, if consider necessary.

Remember that [author] does not owe anything for you. Use vmConsole as is or
do not use at all, I do not care.

## Credits

- [Alpine Linux]: the operating system used in vmConsole.
- [ConnectBot]: the recommended SSH client for use with vmConsole.
- [QEMU]: the emulator and virtualizer, a core of vmConsole.
- [Termux]: the famous terminal emulator for [Android OS], vmConsole uses
  certain parts of it.

[author]: https://github.com/sylirre
[Android OS]: https://www.android.com
[Alpine Linux]: https://alpinelinux.org
[Alpine Linux Wiki]: https://wiki.alpinelinux.org/wiki/Main_Page
[ConnectBot]: https://github.com/connectbot/connectbot
[Limbo PC]: https://github.com/limboemu/limbo
[QEMU]: https://qemu.org
[Termux]: https://termux.dev
[UserLAnd]: https://github.com/CypherpunkArmory/UserLAnd
[Wiki]: https://github.com/sylirre/vmConsole/wiki


https://dl-cdn.alpinelinux.org/alpine/v3.18/releases/x86_64/alpine-virt-3.18.1-x86_64.iso
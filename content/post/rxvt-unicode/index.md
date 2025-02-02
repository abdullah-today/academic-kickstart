---
# Documentation: https://sourcethemes.com/academic/docs/managing-content/

title: 'URXVT - Terminal for Geeks'
subtitle: ""
summary: ""
authors: []
tags: [ 'rxvt', 'terminal', 'commandline', 'urxvt', 'rxvt-unicode']
categories: []
slug: rxvt
date: 2019-09-19T15:55:29+05:00
lastmod: 2019-09-19T15:55:29+05:00
comments: true
featured: false
draft: false

# Featured image
# To use, add an image named `featured.jpg/png` to your page's folder.
# Focal points: Smart, Center, TopLeft, Top, TopRight, Left, Right, BottomLeft, Bottom, BottomRight.
image:
  caption: "ncmpcpp running inside urxvt"
  focal_point: "Smart"
  preview_only: false

# Projects (optional).
#   Associate this post with one or more of your projects.
#   Simply enter your project's folder or file name without extension.
#   E.g. `projects = ["internal-project"]` references `content/project/deep-learning/index.md`.
#   Otherwise, set `projects = []`.
projects: []
---


#### What's URxvt?  

As a linux user, I spend most of my time in terminal emulators. There are alot of emulators available today but none can beat rxvt-unicode.

The biggest problem most new linux users face is how to configure it. Today I'll explain how you can use it to your needs.

Most distributions package it with less features enabled. I always compile it from source. So let's start and in the end you'll end up with a perfect terminal emulator.

Get the source and compile it.

```
$ wget http://dist.schmorp.de/rxvt-unicode/Attic/rxvt-unicode-9.22.tar.bz2
$ tar xvf rxvt-unicode-9.22.tar.bz2
$ cd rxvt-unicode-9.22
$ ./configure --enable-everything --enable-256-color
$ make
# make install
```

--enable-everything will compile all things for us except 256 color support. So keep that in mind.  

So now rxvt-unicode is installed, just execute it. You won't like it out of the box. We have to configure it.

#### Configuration  


rxvt-unicode reads the configuration from two files, ~/.Xresources or ~/.Xdefaults. So here I'm gonna put my ~/.Xdefaults, just copy it to your home directory as ~/.Xdefaults. You can always get the latest one [here](https://gitlab.com/Abdullah/cfg/-/blob/master/etc/.Xresources).

```
$ cat ~/.Xresources

! In the name of Allah, the most Gracious, the most Merciful.
! 
!  ▓▓▓▓▓▓▓▓▓▓
! ░▓ Author ▓ Abdullah <https://abdullah.today>
! ░▓▓▓▓▓▓▓▓▓▓
! ░░░░░░░░░░
! 
! ░█░█░█▀▄░█▀▀░█▀▀░█▀█░█░█░█▀▄░█▀▀░█▀▀░█▀▀
! ░▄▀▄░█▀▄░█▀▀░▀▀█░█░█░█░█░█▀▄░█░░░█▀▀░▀▀█
! ░▀░▀░▀░▀░▀▀▀░▀▀▀░▀▀▀░▀▀▀░▀░▀░▀▀▀░▀▀▀░▀▀▀


! Colors

!black
*color0                    : #1C1C1C
*color8                    : #4d4d4d
!red
*color1                    : #D81860
*color9                    : #F00060
!green
*color2                    : #B7CE42
*color10                   : #BDE077
!yellow
*color3                    : #FEA63C
*color11                   : #FFE863
!blue
*color4                    : #66AABB
*color12                   : #AACCBB
!magenta
*color5                    : #B7416E
*color13                   : #BB4466
!cyan
*color6                    : #5E7175
*color14                   : #A3BABF
!white
*color7                    : #DDEEDD
*color15                   : #6C887A
*.foreground  : #fffaf4
*.background  : #0e1019
*.cursorColor : #ff0018

! URxvt 

! if remote host is having problems with rxvt-unicode, copy
! /usr/share/terminfo/r/rxvt-unicode at hosts ~/.terminfo/r/rxvt-unicode

URxvt*font                 : xft:FantasqueSansMono Nerd Font:Italic:size=21,
xft:Fantasque Sans Mono:Italic:size=21, xft:DejaVu Sans Mono for
Powerline:size=21, xft:Segoe UI Emoji:size=21, xft:SimHei:size=21
URxvt*boldfont             : xft:Bitstream Vera Sans
Mono:Bold:size=17:antialias=true
URxvt*bolditalicfont       : xft:Bitstream Vera Sans
Mono:Bold:italic:size=17:antialias=true
URxvt*utf                  : 1
URxvt*locale               : 1
URxvt.imlocale             : en_US.UTF-8
URxvt*letterSpace          : 0
URxvt*termName             : rxvt-unicode-256color
URxvt*geometry             : 96x30
URxvt*background           : #1B2B34
URxvt*reverseVideo         : 0
URxvt*loginShell           : 0
URxvt*jumpScroll           : 1
URxvt*skipScroll           : 1
URxvt*pastableTabs         : 1
URxvt*scrollstyle          : plain
URxvt*scrollBar            : 0
URxvt*scrollBar_right      : 0
URxvt*scrollBar_floating   : 0
URxvt*scrollBar_align      : centre
URxvt*thickness            : 0
URxvt*scrollTtyOutput      : 0
URxvt*scrollTtyKeypress    : 1
URxvt*scrollWithBuffer     : 1
URxvt*inheritPixmap        : 0
URxvt*transparent          : 0
URxvt*tintColor            : #ffffff
URxvt*shading              : 145
URxvt*blurRadius           : 1x65
URxvt*fading               : 25
URxvt*fadeColor            : #008B8B
URxvt*utmpInhibit          : 1
URxvt*urgentOnBell         : 1
URxvt*visualBell           : 0
URxvt*mapAlert             : 0
URxvt*meta8                : 0
URxvt*mouseWheelScrollPage : 0
URxvt*tripleclickwords     : 0
URxvt*insecure             : 0
URxvt*cursorUnderline      : 1
URxvt*cursorBlink          : 0
URxvt*pointerBlank         : 1
URxvt*iconFile             :
/usr/share/icons/Adwaita/16x16/apps/utilities-terminal-symbolic.symbolic.png
URxvt*pointerShape         : ul_angle
URxvt*intensityStyles      : 1
URxvt*saveLines            : 9999
URxvt*buffered             : 1
URxvt*depth                : 32
URxvt*visual               : 0x16f
URxvt*override-redirect    : 0
URxvt*externalBorder       : 15
URxvt*internalBorder       : 15
URxvt*borderLess           : 0
URxvt*lineSpace            : 0
URxvt*skipBuiltinGlyphs    : 0
URxvt*pointerBlankDelay    : 1
URxvt*print-pipe           : cat >  /tmp/$(echo urxvt.dump.$(date
+'%Y%M%d%H%m%S'))
URxvt*modifier             :
URxvt*cutchars             : BACKSLASH " "
'"'&()*,;<=>?@[]^{|}\"()*,<>[]{}|''"\
URxvt*secondaryScreen      : 1
URxvt*secondaryScroll      : 0
URxvt*perl-lib             : /home/ak/.urxvt/ext
URxvt*iso14755             : 1
URxvt*iso14755_52          : 1
URxvt*matcher.button       : 2
URxvt*url-launcher         : /usr/bin/google-chrome-stable
URxvt*url-select.underline : 1
URxvt*matcher.rend.0       : Uline Bold fg5
URxvt*selection.pattern-0  : ([[                           : word
: ]]+)
URxvt*keysym.M-C-c         : selection                     : rot13
URxvt*perl-ext-common      : vim,default,matcher,font-size
URxvt*vim-scrollback       : M-s
URxvt*vim-scrollback-paste : M-p
URxvt*clipboard.copycmd    : xsel -ib
URxvt.keysym.C-Up:     font-size:increase
URxvt.keysym.C-Down:   font-size:decrease
URxvt.keysym.C-S-Up:   font-size:incglobal
URxvt.keysym.C-S-Down: font-size:decglobal


! Polybar

polybar*background             : #24292A
polybar*foreground             : #ccd2be
polybar*fading                 : 15
polybar*fadeColor              : black
polybar*cursorColor            : #16A085
polybar*pointerColorBackground : #2B2C2B
polybar*pointerColorForeground : #16A085
polybar*urgent                 : #B34747

! black dark/light
polybar*color0                 : #24292A
polybar*color8                 : #3c4140

! red dark/light
polybar*color1                 : #ff8843
polybar*color9                 : #c48851

! green dark/light
polybar*color2                 : #7a8d5c
polybar*color10                : #aec199

! yellow dark/light
polybar*color3                 : #a69658
polybar*color11                : #c4b268

! blue dark/light
polybar*color4                 : #7b90a9
polybar*color12                : #91aac7

! magenta dark/light
polybar*color5                 : #aa6161
polybar*color13                : #e78484

! cyan dark/light
polybar*color6                 : #698885
polybar*color14                : #83a5a1

! white dark/light
polybar*color7                 : #a8b298
polybar*color15                : #ccd2be

! pink
polybar*color16                : #9181E7

! purple
polybar*color17                : #D7AFF9


! XTERM

XTerm.vt100.faceName         :Fantasque Sans
Mono:italic:size=15:antialias=true
XTerm.vt100.boldFont         :Fantasque Sans Mono:bold:italic:size=15
xterm.scaleHeight           : 1.01
xterm*termName              : xterm-256color
xterm*geometry              : 96x30
xterm*reverseVideo          : 0
xterm*loginShell            : 1

! Dmenu

dmenu.selforeground:      #474c57
dmenu.background:         #ffffff
dmenu.selbackground:      #4ec2e8
dmenu.foreground:         #474c57

! rofi

rofi.color-enabled: true
rofi.color-window: #ffffff, #ffffff, #ffffff
rofi.color-normal: #ffffff, #474c57, #ffffff, #ffffff, #4ec2e8
rofi.color-active: #ffffff, #fec7cd, #ffffff, #ffffff, #95c1c0
rofi.color-urgent: #ffffff, #f59335, #ffffff, #ffffff, #f59335  

! Cursor

Xcursor.size                : 16

! Xautolock

Xautolock.locker            : "/usr/bin/physlock -mp 'Aur tum apny Rab ki kon
kon c nematon ko jhutlawo gy?'"


```

After saving the file, we have to load it.

```
$ xrdb -load ~/.Xdefaults
```

Now execute it. You may not have the fonts I use so maybe you face some errors. Just install those fonts or change them.

I also have written a post about [fonts](https://abdullah.today/fonts.html).

Still have problems? Just lemme know and I'll be happy to assist you.

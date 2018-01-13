---
layout: default
title:  "Binding shortcuts to Spotify actions"
categories: Tools
---
# Foreword

Hello, my name is Leo. This is as you can see my very first blog post so I would
really like some feedback. A lot of future content will probably consist of
similar posts like this where I describe tools I discovered or setups I think
people would like. What do you guys think about this theme(not the Jekyll one)?
Is the format to concise or is it too verbose? Any feedback is highly appreciated! Please comment
[here](https://github.com/Zetagon/blog/issues/1)!

# Background
Shortcuts for [Spotify](https://wiki.archlinux.org/index.php/Spotify) from
whichever window you want using
[xbindkeys](https://wiki.archlinux.org/index.php/Xbindkeys) and dbus.

Xbindkeys is an useful program that allows you to define shortcuts to
bash-commands, independently of the window manager.

# The code
This code snippet toggles Spotify music between play and pause:
``` bash
dbus-send --print-reply --dest=org.mpris.MediaPlayer2.spotify /org/mpris/MediaPlayer2 org.mpris.MediaPlayer2.Player.PlayPause
```
And these is equivalent to pressing the arrows on the each side of the play button:

``` bash
dbus-send --print-reply --dest=org.mpris.MediaPlayer2.spotify /org/mpris/MediaPlayer2 org.mpris.MediaPlayer2.Player.Previous
dbus-send --print-reply --dest=org.mpris.MediaPlayer2.spotify /org/mpris/MediaPlayer2 org.mpris.MediaPlayer2.Player.Next
```

Use xbindkeys to bind play/pause keys to commands above(put this in your ~/.xbindkeysrc):
``` bash
"dbus-send --print-reply --dest=org.mpris.MediaPlayer2.spotify /org/mpris/MediaPlayer2 org.mpris.MediaPlayer2.Player.PlayPause"
XF86AudioPlay
# Previous spotify song
"dbus-send --print-reply --dest=org.mpris.MediaPlayer2.spotify /org/mpris/MediaPlayer2 org.mpris.MediaPlayer2.Player.Previous"
Mod4+XF86AudioLowerVolume # Super + raise lower volume

# Next spotify song
"dbus-send --print-reply --dest=org.mpris.MediaPlayer2.spotify /org/mpris/MediaPlayer2 org.mpris.MediaPlayer2.Player.Next"
Mod4+XF86AudioRaiseVolume # Super + raise raise volume
```


Don't forget to put the command xbindkeys in your initialization file for X before launching the
window manager

# If you are having trouble:

* Keycodes

```xbindkeys -k``` prompts you to press a key/keycombination and gives you the correct keycode

Example for super + L
```bash
    m:0x40 + c:133
    Mod4 + Super_L
```

You can choose either line if you want.

* Reloading keybindings

To reload ~/.xbindkeysrc you have to run the command ```xbindkeys``` again, but
first you have to kill previous instances. This is because each time you run
```xbindkeys``` a new instance is launched and the program can't handle conflicts

* Misc.

```xbindkeys -n``` is helpful for debugging non-working keybindings.

# Tips

Xbindkeys can rebind most keys, even the [Menu
key](https://en.wikipedia.org/wiki/Menu_key#/media/File:Kontextmen%C3%BC.jpg)
which is useless in my opinion. For now I have disabled it because I have not
found a better use for it.

```bash
# Unmap Menu
""
Menu
```
# [Comments on Github](https://github.com/Zetagon/blog/issues/1)

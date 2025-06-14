reflex -- a wrapper for searching selected text with surfraw
============================================================

Copyright (C) 2025 Nivyan Lakhani <mail@nivyan.xyz>

reflex is a shell script wrapper for surfraw. It searches for text in
the primary selection using a specified or chosen sr 'elvis'. It is
intended to be bound to a hotkey in a window manager.


* Dependencies
--------------

  - surfraw
  - rofi (or a dmenu-compatible chooser)
  - wl-clipboard (for Wayland; though see Configuration section)


* Installation
----------------

1. Place the `reflex` script in your `$PATH` (e.g., `/usr/local/bin`).
2. Make it executable: `chmod +x /path/to/reflex`.
3. Edit the script to configure your browser and clipboard utility.


* Configuration
-----------------

You must edit the script to suit your environment.

Browser:
Change the `-browser=` flag in the final `surfraw` command to your
preferred browser, or remove it to use the surfraw default.

Clipboard Utility (for X11):
The script defaults to `wl-paste` for Wayland. For X11, replace the
`query=$(wl-paste ...)` line with one of the following:

  `query=$(xsel -o -p)`
  `query=$(xclip -o -selection primary)`


* Usage
---------

  `reflex <elvis> [i]`
  `reflex -c|--choose [i]`

`elvis` is any valid surfraw elvis (e.g., `wolframalpha`, `wikipedia`).

The `-c` or `--choose` flags will present a `rofi` menu to select an
elvis.

The optional `[i]` argument (any string, e.g. "i" for interactive)
will prompt for a query via `rofi` instead of using the primary text
selection.


* Example Keybinds
--------------------

i3 / sway (`~/.config/i3/config`):

  bindsym $mod+s exec reflex duckduckgo
  bindsym $mod+Shift+s exec reflex --choose
  bindsym $mod+Ctrl+s exec reflex wikipedia i

bspwm (`~/.config/sxhkd/sxhkdrc`):

  super + s
      reflex google

  super + shift + s
      reflex -c

hyprland (`~/.config/hypr/hyprland.conf`):

  bind = $mainMod, S, exec, reflex github
  bind = $mainMod SHIFT, S, exec, reflex -c

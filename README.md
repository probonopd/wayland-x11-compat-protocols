# wayland-x11-compat-protocols

The missing Wayland protocols for features that are available in X11 (but are denied by the official Wayland protocols).

> Es gibt nichts Gutes ― außer man tut es.

Erich Kästner

## Protocols

Allow applications and desktop environments (and abstractions like [libxfce4windowing](https://gitlab.xfce.org/xfce/libxfce4windowing)) to do what they can do in X11...

- [x] Terminology: Handle _windows_ (not: "surfaces", "toplevels") like in X11 (_window_ ID, etc.) (for now we are assuming that `zwlr_foreign_toplevel_handle_v1` [for non-Wayland applications] and `xdg_toplevel` [for Wayland applications] is the Wayland equivalent of a window ID)
- [x] `screen_video_capture_v1`: Capture the screen (without Pipewire, Portals, etc. see [ext-screencopy-v1](https://gitlab.freedesktop.org/wayland/wayland-protocols/-/merge_requests/124))
- [x] `global_shortcuts_v1`: Set global keyboard shortcuts (without Portals, etc.)
- [x] `window_properties_v1` Get the process ID and other vital information (like in `xprop`) and kill other applications (like `xkill`) (for partial support see [ext-foreign-toplevel-list](https://gitlab.freedesktop.org/wayland/wayland-protocols/-/merge_requests/187) and [ext-foreign-toplevel-state](https://gitlab.freedesktop.org/wayland/wayland-protocols/-/merge_requests/196))
- [x] `window_properties_v1`: Set key-value combinations on windows (atoms)
- [x] `window_management_v1`: Position windows in a [prescriptive](https://www.youtube.com/watch?v=relxcJiHBnA&t=1230s) way (also see [ext-placement](https://gitlab.freedesktop.org/wayland/wayland-protocols/-/merge_requests/247)). Also see [river_layout_v3](https://codeberg.org/river/river/src/branch/master/protocol/river-layout-v3.xml) and [ext_placement_v1](https://gitlab.freedesktop.org/wayland/wayland-protocols/-/merge_requests/247)
- [ ] Drag-and-drop between applications (There is `wl_data_offer`, but why can't we drag files from an archive manager to the file manager in Raspberry Pi OS then? We need a solution [without kludges like Portals and FUSE](https://gitlab.gnome.org/AlynxZhou/file-roller/-/commit/80f53ece6714c89f604a80d60a2153e7599060fd)) 
- [ ] Client data query (e.g., window/surface positions, cursor position with xhot/yhot position, keyboard state, window geometries; AT-SPI2 is very limited)
- [ ] An equivalent to XTEST (ability to send keystrokes, move the cursor, move/resize windows and so on; `ydotool` is somewhat limited)
- [ ] Frame callback-less rendering (ability to submit new frames at any time) (assuming it doesn't exist yet)
- [ ] (Feel free to suggest additional candidates)

...unencumbered, and without additional software besides the Wayland compositor (such as Pipewire, Portals, .desktop files, etc.).

Already being implemented upstream:

- [x] [`ext_toplevel_icon_v1`](https://gitlab.freedesktop.org/wayland/wayland-protocols/-/merge_requests/269) Set arbitrary window icons with no need for `.desktop` files (thanks [__ximion__](https://github.com/ximion); also see [The case for an icon protocol](https://www.youtube.com/watch?v=yNSdIvdJeSw))

## Motivation

The official [wayland-protocols](https://gitlab.freedesktop.org/wayland/wayland-protocols) project has not provided protocols for essential functionality known from X11, hence preventing application developers and desktop environment developers from having a smooth transition path from X11 to Wayland with feature parity.

## What is this?

* This is a namespace for Wayland protocols (goverened outside of the existing Wayland projects)
* It is not expected that all Wayland compositors will implement these protocols, but most likely _some_ will
* Whenever people ask for something that works in X11 but not in Wayland, we add it there (ideally in a way that makes it trivially easy for people to port existing X11 applications to the x11-compat_... Wayland protocols)
* The only requirement for a protocol to be added to this namespace is: Functionality that works in X11 but does not work in Wayland due to Wayland policy decisions
* The protocols must not draw in additional dependencies besides the Wayland compositor itself (such as D-Bus, Pipewire, Portals, etc.)
* Parameters should ideally be the same as in the corresponding X11 API
* This is a volunteer-based community effort. Your contributions are highly welcome!
* `wayland-x11-compat-protocols` is a working title. Suggestions, anyone?

## But... security.

The windowing system is not the place to restrict what applications are and are not allowed to do.

If you want to restrict what applications can do, use a sandbox (or disallow these protocols in your compositor via a configuration setting).

## Also see

https://gitlab.freedesktop.org/wlroots/wlr-protocols/ - it seems to be addressing a few of the missing Wayland protocols. Unfortunately not all Wayland compositors are built on wlroots yet, so those may or may not work on your desktop.

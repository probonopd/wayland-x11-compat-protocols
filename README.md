# wayland-x11-compat-protocols

The missing Wayland protocols for features that are available in X11 (but are denied by the official Wayland protocols).

> Es gibt nichts Gutes ― außer man tut es.

Erich Kästner

## Protocols

Allow applications and desktop environments (and abstractions like [libxfce4windowing](https://gitlab.xfce.org/xfce/libxfce4windowing)) to do what they can do in X11...

- [ ] Handle _windows_ (not: "surfaces") like in X11 (window ID, etc.)
- [ ] Capture the screen (without Pipewire, Portals, etc.)
- [ ] Set global keyboard shortcuts (without Portals, etc.)
- [ ] Get the process ID and other vital information (like in `xprop`) and kill other applications (like `xkill`)
- [ ] Set arbitrary window icons with no need for `.desktop` files (see [ext-window-icon](https://gitlab.freedesktop.org/wayland/wayland-protocols/-/merge_requests/269))
- [ ] Set key-value combinations on windows (atoms)
- [ ] Arbitrarily position windows (see [ext-placement](https://gitlab.freedesktop.org/wayland/wayland-protocols/-/merge_requests/247))
- [ ] Drag-and-drop between applications (without Portals, etc.)
- [ ] Client data query (e.g., window/surface positions, cursor position with xhot/yhot position, keyboard state, window geometries; AT-SPI2 is very limited)
- [ ] An equivalent to XTEST (ability to send keystrokes, move the cursor, move/resize windows and so on; `ydotool` is somewhat limited)
- [ ] Frame callback-less rendering (ability to submit new frames at any time) (assuming it doesn't exist yet)
- [ ] (Feel free to suggest additional candidates)

...unencumbered, and without additional software besides the Wayland compositor (such as Pipewire, Portals, .desktop files, etc.).

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

If you want to restrict what applications can do, use a sandbox.

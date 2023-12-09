# wayland-x11-compat-protocols

The missing Wayland protocols for features that are available in X11 (but are denied by the official Wayland protocols).

## Motivation

The official [wayland-protocols](https://gitlab.freedesktop.org/wayland/wayland-protocols) project has not provided protocols for essential functionality known from X11, hence preventing application developers and desktop environment developers from having a smooth transition path from X11 to Wayland with feature parity.

## What is this?

* This is a namespace for Wayland protocols (goverened outside of the existing Wayland projects)
* Whenever people ask for something that works in X11 but not in Wayland, we add it there (ideally in a way that makes it trivially easy for people to port existing X11 applications to the x11-compat_... Wayland protocols)
* The only requirement for a protocol to be added to this namespace is: Functionality that works in X11 but does not work in Wayland due to Wayland policy decisions
* The protocols must not draw in additional dependencies besides the Wayland compositor itself (such as D-Bus, Pipewire, Portals, etc.)
* Parameters should ideally be the same as in the corresponding X11 API
* This is a volunteer-based community effort. Your contributions are highly welcome!
* `wayland-x11-compat-protocols` is a working title. Suggestions, anyone?

## Protocols wanted

* Allow applications to capture the screen just like in X11
* Allow applications to set global keyboard shortcuts just like in X11
* Allow applications to kill other applications just like in X11
* Allow applications to set arbitrary window icons just like in X11
* Allow applications to set key-value combinations on windows (atoms) like in X11
* Allow windows to position themselves just like in X11
* (Feel free to suggest additional candidates)

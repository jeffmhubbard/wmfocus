# wmfocus - Visually focus windows by label

[![Build Status](https://travis-ci.com/svenstaro/wmfocus.svg?branch=master)](https://travis-ci.com/svenstaro/wmfocus)
[![AUR](https://img.shields.io/aur/version/wmfocus.svg)](https://aur.archlinux.org/packages/wmfocus/)
[![Crates.io](https://img.shields.io/crates/v/wmfocus.svg)](https://crates.io/crates/wmfocus)
[![dependency status](https://deps.rs/repo/github/svenstaro/wmfocus/status.svg)](https://deps.rs/repo/github/svenstaro/wmfocus)
[![license](http://img.shields.io/badge/license-MIT-blue.svg)](https://github.com/svenstaro/wmfocus/blob/master/LICENSE)

This tool that allows you to rapidly choose a specific window directly without having to use the mouse or directional keyboard navigation.

![Screen cast](cast.apng)

Thanks to cairo, it should work on all kinds of screens and automatically display at the correct size according to your DPI.


## Installation

**On Arch Linux**: [Get it from AUR](https://aur.archlinux.org/packages/wmfocus/)

**With Cargo**: `cargo install --features i3 wmfocus`

## Usage

Draw labels on the upper-left corner of all windows:

    wmfocus

Completely fill out windows and draw the label in the middle (try it with transparency!):

    wmfocus --fill

Use a different font (as provided by fontconfig):

    wmfocus -f "Droid Sans":100

Change up the default colors:

    wmfocus --textcolor red --textcoloralt #eeeeee --bgcolor "rgba(50, 50, 200, 0.5)"

wmfocus will make use of a compositor to get real transparency.

## Full help
```
wmfocus 1.1.2
Sven-Hendrik Haase <svenstaro@gmail.com>


USAGE:
    wmfocus [FLAGS] [OPTIONS]

FLAGS:
        --fill         Completely fill out windows
    -h, --help         Prints help information
    -p, --printonly    Print the window id only but don't change focus
    -V, --version      Prints version information

OPTIONS:
        --textcolor <text_color>           Text color (CSS notation) [default: #dddddd]
        --textcoloralt <text_color_alt>    Text color alternate (CSS notation) [default: #666666]
        --bgcolor <bg_color>               Background color (CSS notation) [default: rgba(30, 30, 30, 0.9)]
        --halign <horizontal_align>        Horizontal alignment of the box inside the window [default: left]  [possible
                                           values: left, center, right]
        --valign <vertical_align>          Vertical alignment of the box inside the window [default: top]  [possible
                                           values: top, center, bottom]
    -f, --font <font>                      Use a specific TrueType font with this format: family:size [default: Mono:72]
    -c, --chars <hint_chars>               Define a set of possbile values to use as hint characters [default:
                                           sadfjklewcmpgh]
    -m, --margin <margin>                  Add an additional margin around the text box (value is a factor of the box
                                           size) [default: 0.2]
    -o, --offset <offset>                  Offset box from edge of window (x,y) [default: 0,0]
```


## Compiling

You need to have recent versions of `rust`, `cargo`, `xcb-util-keysyms`, `libxkbcommon-x11` and `cairo` installed.

Then, just clone it like usual and `cargo run` to get output:

    git clone https://github.com/svenstaro/wmfocus.git
    cd wmfocus
    cargo run --features i3


## Window manager support

While this tool is window manager-independent, an implementation for your favorite window manager might not yet be available. Current support:

- i3

If you want to implement support for more window managers, have a look at the [i3 implementation](https://github.com/svenstaro/wmfocus/blob/master/src/wm_i3.rs).

This tool is heavily inspired by [i3-easyfocus](https://github.com/cornerman/i3-easyfocus).


## Releasing

This is mostly a note for me on how to release this thing:

- Update `README.md`, `Cargo.toml`.
- `git commit` and `git tag -s`, `git push`.
- `cargo publish`
- Update AUR package.

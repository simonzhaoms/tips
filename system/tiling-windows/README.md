# Window Tiling Manager #

## On Windows ##

There are 4 shortcuts for simple window tiling:

* `Win-left`: Put the window to left half
* `Win-right`: Put the window to right half
* `Win-up`: Put the window to (left/right) top
* `Win-down`: Put the window to (left/right) bottom

We also recorded a [video for demo](media/Win-Arrows.mp4).

### FancyZones ###

Microsoft also provides a tool called
[PowerToys](https://github.com/microsoft/PowerToys) for tuning
Windows.  It contains several utilities:

* [FancyZones](https://github.com/microsoft/PowerToys/tree/master/src/modules/fancyzones):
  A window manager
* [Shortcut](https://github.com/microsoft/PowerToys/tree/master/src/modules/shortcut_guide):
  Windows key shortcut guide
* [PowerRename](): Renaming tool

#### Installation ####

**NOTE** To use PowerToys, Windows build 17134 or higher is needed.
To find the build version of your Windows, `Win-r` and type `winver`.

Go to
[PowerToys Release](https://github.com/Microsoft/powertoys/releases)
to download and install PowerToys.  See
[PowerToys Installation](https://github.com/microsoft/PowerToys#installation)
for more details.

#### Usage ####

**NOTE** To use FancyZones, it needs to be enabled in the setting of
PowerToys where you can find the setting options for FancyZones as
well, such as the shortcut to redesign FancyZones' layout.

1. Select a layout by `Win-~`
   * By default, `Win-~` is used for opening FancyZones' layout
     setting where the layout of windows is designed.
1. Move window to a cell of the layout by dragging it with `Shift`
   holded
   * Then you can invoke automatic layout of windows by holding
     `Shift` while dragging the window you want to rearrange.

A [demo video](media/FancyZones.mp4) is also provided.


### Other Alternatives ###

* [AquaSnap](https://www.nurgo-software.com/products/aquasnap)
* [TidyTabs](https://www.nurgo-software.com/products/tidytabs)


## On Linux ##


# Configuring LeftWM

 _All code snippets in this section refer to the file `~/.config/leftwm/config.toml`_  
 All entries require a modifier, even if blank: `modifier = []`

***Important: You will need to reload (recommended SoftReload, as it tries to preserve the WM state as far as possible) in order to apply changes to `config.toml`.***

## Terms

- _Default_ refers to the original `config.toml` specified when LeftWM first runs.  
- _Partial Default_ refers to a command that is in the original `config.toml` but is not the only instance of that command.  
- _Example_ refers to a snippet that is not in the original `config.toml` but can be added or modified for additional features.

# Table of contents

- [Configuring LeftWM](#configuring-leftwm)
- [Autostart](#autostart)
- [Modkey](#modkey)
- [Mousekey](#mousekey)
- [Tag Behaviour](#tag-behaviour)
- [Focus Behaviour](#focus-behaviour)
- [Layouts](#layouts)
- [Layout Mode](#layout-mode)
- [Tags](#tags)
- [Max Window Width](#max-window-width)
- [Workspaces](#workspaces)
- [Scratchpads](#scratchpads)
- [Keybind](#keybind)
- [Keybind Commands](#keybind-commands)
  - [Execute](#execute)
  - [HardReload](#hardreload)
  - [SoftReload](#softreload)
  - [CloseWindow](#closewindow)
  - [MoveToLastWorkspace](#movetolastworkspace)
  - [MoveWindowToNextWorkspace](#movewindowtonextworkspace)
  - [MoveWindowToPreviousWorkspace](#movewindowtopreviousworkspace)
  - [FloatingToTile](#floatingtotile)
  - [TileToFloating](#tiletofloating)
  - [ToggleFloating](#togglefloating)
  - [MoveWindowUp](#movewindowup)
  - [MoveWindowDown](#movewindowdown)
  - [MoveWindowTop](#movewindowtop)
  - [MoveToTag](#movetotag)
  - [FocusWindowUp](#focuswindowup)
  - [FocusWindowDown](#focuswindowdown)
  - [FocusWindowTop](#focuswindowtop)
  - [NextLayout](#nextlayout)
  - [PreviousLayout](#previouslayout)
  - [SetLayout](#setlayout)
  - [RotateTag](#rotatetag)
  - [FocusWorkspaceNext](#focusworkspacenext)
  - [FocusWorkspacePrevious](#focusworkspaceprevious)
  - [GotoTag](#gototag)
  - [FocusNextTag](#focusnexttag)
  - [FocusPreviousTag](#focusprevioustag)
  - [SwapTags](#swaptags)
  - [IncreaseMainWidth](#increasemainwidth)
  - [DecreaseMainWidth](#decreasemainwidth)
  - [SetMarginMultiplier](#setmarginmultiplier)
  - [ToggleFullScreen](#togglefullscreen)
  - [ToggleScratchPad](#togglescratchpad)

# Autostart

Actually not part of `config.toml` but kind of belongs here:
There is basically three ways to autostart applications with `LeftWM` session login (and restart them when executing `SoftReload`/`HardReload`)
1. XDG_AUTOSTART: to use this, place a `.desktop` file in `~/.config/autostart` (more info about desktop entries can be found in the [ArchWiki](https://wiki.archlinux.org/title/Desktop_entries))
2. `up`/`down` scripts in [the theme](https://github.com/leftwm/leftwm/wiki/Themes#requirements-for-a-theme---up-and-down-scripts)
3. the same scripts can be placed in `~/.config/leftwm/` in order to be theme agnostic
*Note: there is no override rules between "theme-scripts" and "config-scripts", as they are agnostic of each other.*

# Modkey

The modkey is the most important setting. It is used by many other settings and controls how key bindings work.
For more info please read [this](https://stackoverflow.com/questions/19376338/xcb-keyboard-button-masks-meaning) post on x11 Mod keys.

Default: `modkey = "Mod4"`  (windows key)

Example: `modkey = "Mod1"`  

# Mousekey

The mousekey is similarly quite important. This value can be used to determine which key, when held, can assist a mouse drag in resizing or moving a floating window or making a window float or tile.
For more info please read [this](https://stackoverflow.com/questions/19376338/xcb-keyboard-button-masks-meaning) post on x11 Mod keys.

Default: `mousekey = "Mod4"`  (windows key)

Example: `mousekey = "Mod1"`  

# Tag Behaviour

Starting with LeftWM 0.2.7, the behaviour of [SwapTags](#swaptags) was changed such that if you are on a tag, such as tag 1, and then SwapTags to tag 1, LeftWM will go to the previous tag instead. This behaviour can be disabled with `disable_current_tag_swap`:

Default: `disable_current_tag_swap = false`

Example: `disable_current_tag_swap = true` (returns to old behaviour)

# Focus Behaviour

LeftWM now has 3 focusing behaviours (Sloppy, ClickTo, and Driven) and one option (focus_new_windows), which alter the way focus is handled.
These encompass 4 different patterns:
1. Sloppy Focus. Focus follows the mouse, hovering over a window brings it to focus.
2. Click-to-Focus. Focus follows the mouse, but only clicks change focus.
3. Driven Focus. Focus disregards the mouse, only keyboard actions drive the focus.
4. Event Focus. Focuses when requested by the window/new windows.

Default:

```toml
focus_behaviour = "Sloppy" # Can be Sloppy, ClickTo, or Driven
focus_new_windows = true
```
**Note: This is only available in LeftWM >=0.2.8.**

# Layouts

Leftwm supports an ever-growing amount layouts, which define the way that 
windows are tiled in the workspace.

Default (all layouts, check [this enum](https://github.com/leftwm/leftwm/blob/main/leftwm-core/src/layouts/mod.rs#L21)
for the latest list):

```toml
layouts = [
    "MainAndDeck",
    "MainAndVertStack",
    "MainAndHorizontalStack",
    "GridHorizontal",
    "EvenHorizontal",
    "EvenVertical",
    "Fibonacci",
    "CenterMain",
    "CenterMainBalanced",
    "Monocle",
    "RightWiderLeftStack",
    "LeftWiderRightStack",
]
```

Example:

```toml
layouts = [
    "MainAndVertStack",
    "Monocle",
]
```

# Layout Mode

Leftwm now has 2 layout modes, Workspace and Tag. These determine how layouts are remembered. When in Workspace mode, layouts will be remembered per workspace. When in Tag mode, layouts are remembered per tag.

Default:

```toml
layout_mode = "Workspace" # Can be Workspace or Tag
```

# Tags

Tags are the names of the virtual desktops were windows live. In other window managers these are sometimes just called desktops. You can rename them to any unicode string including symbols/icons from popular icon libraries such as font-awesome.

Default: `tags = ["1", "2", "3", "4", "5", "6", "7", "8", "9"]`

Example: `tags = ["Browser ♖", "Term ♗", "Shell ♔", "Code ♕"]`

# Max Window Width
> This feature was introduced in PR [#482](https://github.com/leftwm/leftwm/pull/482)

You can configure a `max_window_width` to limit the width of the tiled windows (or rather, the width of columns in a layout). This feature comes in handy when working on ultra-wide monitors where you don't want a single window to take the complete workspace width.

**Demonstration**

Without `max_window_width`
```text
+-----------------------------------------------+
|+---------------------------------------------+|
||                                             ||
||                     1                       ||  [49' monitor]
||                                             ||
|+---------------------------------------------+|
+-----------------------------------------------+
```
```text
+-----------------------------------------------+
|+----------------------+----------------------+|
||                      |                      ||
||          1           |          2           ||  [49' monitor]
||                      |                      ||
|+----------------------+----------------------+|
+-----------------------------------------------+
```

With `max_window_width`
```text
+-----------------------------------------------+
|               +---------------+               |
|               |               |               |
|               |       1       |               |  [49' monitor]
|               |               |               |
|               +---------------+               |
+-----------------------------------------------+

                ^^^^^^^^^^^^^^^^^
                MAX_WINDOW_WIDTH
```

```text
+-----------------------------------------------+
|        +--------------+--------------+        |
|        |              |              |        |
|        |       1      |       2      |        |  [49' monitor]
|        |              |              |        |
|        +--------------+--------------+        |
+-----------------------------------------------+

         ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
              MAX_WINDOW_WIDTH * 2
```

This setting can be configured either globally, per workspace, or both. The workspace specific configuration always takes precedence over the global setting.

Values: An `int` value for absolute pixels (`2200` means `2200px`), or a decimal value for fractions (`0.4` means `40%`).\
Default: Has no default value. No value means no width limit.

Example:

```toml
# global configuration: 40%
max_window_width = 0.4

[[workspaces]]
y = 0
x = 0
height = 1440
width = 2560
# workspace specific configuration: 1200px
max_window_width = 1200
```

**Note: This is only available in LeftWM >=0.2.9. It is currently only available through aur/leftwm-git or building from source.**

# Workspaces

Workspaces are how you view tags (desktops). A workspace is a area on a screen or most likely the whole screen. in this areas you can view a given tag.

Default: `workspaces = []` (one workspace per screen)

Example (two workspaces on a single ultrawide):

```toml
[[workspaces]]
y = 0
x = 0
height = 1440
width = 1720

[[workspaces]]
y = 0
x = 1720
height = 1440
width = 1720
```

Or with short syntax:
```toml
workspaces = [
    { y = 0, x = 0, height = 1440, width = 1720 },
    { y = 0, x = 1720, height = 1440, width = 1720 },
]
```
Some features in your theme can be set for specific workspaces, such as gutters. If you have multiple workspaces defined in your `config.toml` and wish to apply workspace-specific settings, you need to add an ID field to your workspaces definition:

```toml
[[workspaces]]
y = 0
x = 0
height = 1440
width = 1720
id = 0

[[workspaces]]
y = 0
x = 1720
height = 1440
width = 1720
id = 1
```

Or with short syntax:
```toml
workspaces = [
    { y = 0, x = 0, height = 1440, width = 1720, id = 0 },
    { y = 0, x = 1720, height = 1440, width = 1720, id = 1 },
]
```
After specifying id in `config.toml`, you can refer to it by wsid in `theme.toml` like below:
```toml
[[gutter]]
side = "Left" # set a 20 pixel margin on the left side of workspace id 0
value = 20
wsid = 0

[[gutter]]
side = "Right"
value = 20
wsid = 0
```
Note that leftwm will consider a configuration that assigns only some, but not all, workspaces an ID to be invalid. The following would result in logging a warning message and falling back to the default config:

```toml
[[workspaces]]
y = 0
x = 0
height = 1440
width = 1720

[[workspaces]]
y = 0
x = 1720
height = 1440
width = 1720
id = 1
```

Or with short syntax:
```toml
workspaces = [
    { y = 0, x = 0, height = 1440, width = 1720 },
    { y = 0, x = 1720, height = 1440, width = 1720, id = 1 },
]
```

# Scratchpads

A scratchpad is a window which you can call to any tag and hide it when not needed. These windows can be any application which can be run from a terminal. To call a scratchpad you will require a keybind for [ToggleScratchPad](#togglescratchpad).

Example:

```toml
# Create a scratchpad for alacritty
[[scratchpad]]
name = "Alacritty" # This is the name which is referenced when calling (case-sensitive)
value = "alacritty" # The command to load the application if it isn't started
# x, y, width, height are in pixels when an integer is inputted or a percentage when a float is inputted.
# These values are relative to the size of the workspace, and will be restricted depending on the workspace size.
x = 860
y = 390
height = 300
width = 200
```
Or with float values:
```toml
[[scratchpad]]
name = "Alacritty"
value = "WINIT_X11_SCALE_FACTOR=1 alacritty -o font.size=14"
x = 0.46
y = 0.20
height = 0.80
width =  0.54
```

Or with short syntax:
```toml
scratchpad = [
    { name = "Alacritty", value = "alacritty", x = 860, y = 390, height = 300, width = 200 },
]
```
**Note: This is only available in LeftWM >=0.2.8.**

# Keybind

All other commands are keybindings. you can think of key bindings as a way of telling LeftWM to do something when a key combination is pressed. There are several types of key bindings. In order for the keybind event to fire, the keys listed in the modifier section should be held down, and the key in the key section should then be pressed. [Here is a list of all keys LeftWM can use as a modifier or a key](https://github.com/leftwm/leftwm/blob/main/leftwm-core/src/utils/xkeysym_lookup.rs#L46).

**Note: As it is a comon pitfall for users of AZERTY keyboards you can find the relevant keysyms fo tag related keybinds [here](https://github.com/leftwm/leftwm/wiki/Troubleshooting#azerty-mapping).**

Example:

```toml
[[keybind]]
command = "Execute"
value = "vlc https://www.youtube.com/watch?v=oHg5SJYRHA0"
modifier = []
key = "XF86XK_AudioPlay"
```

You can use the short syntax here as well:
```toml
keybind = [
    { command = "Execute", value = "vlc https://www.youtube.com/watch?v=oHg5SJYRHA0", modifier = [], key = "XF86XK_AudioPlay" },
    { command = "HardReload", modifier = ["modkey", "Shift"], key = "b"},
    { command = "CloseWindow", modifier = ["modkey", "Shift"], key = "q" },
]
```

**Note: even if blank, a modifier must be present! Use `modifier = []` for no modifier**

# Keybind Commands

## Execute

Execute a shell command when a key combination is pressed.

Partial default:

```toml
[[keybind]]
command = "Execute"
value = "rofi -show run"
modifier = ["modkey"]
key = "p"
```

**Note: This command requires a value field to be specified**.

## HardReload

Completely restarts LeftWM.

Example:

```toml
[[keybind]]
command = "HardReload"
modifier = ["modkey", "Shift"]
key = "b"
```

## SoftReload

Restarts LeftWM but remembers the state of all windows. This is useful when playing with the config file or themes.

Default:

```toml
[[keybind]]
command = "SoftReload"
modifier = ["modkey", "Shift"]
key = "r"
```

## CloseWindow

Closes the window that is currently focused. This is not a forceful quit. It is equivalent to clicking the (x) in the top right of a window normally.

Default:

```toml
[[keybind]]
command = "CloseWindow"
modifier = ["modkey", "Shift"]
key = "q"
```

## MoveToLastWorkspace

Takes the window that is currently focused and moves it to the workspace that was active before the current workspace.

Default:

```toml
[[keybind]]
command = "MoveToLastWorkspace"
modifier = ["modkey", "Shift"]
key = "w"
```

## MoveWindowToNextWorkspace

Takes the window that is currently focused and moves it to the next workspace.

Example:

```toml
[[keybind]]
command = "MoveWindowToNextWorkspace"
modifier = ["modkey", "Shift"]
key = "Right"
```

## MoveWindowToPreviousWorkspace

Takes the window that is currently focused and moves it to the previous workspace.

Example:

```toml
[[keybind]]
command = "MoveWindowToPreviousWorkspace"
modifier = ["modkey", "Shift"]
key = "Left"
```

## FloatingToTile

Snaps the focused floating window into the workspace below.

Example:

```toml
[[keybind]]
command = "FloatingToTile"
modifier = ["modkey", "Shift"]
key = "t"
```

## TileToFloating

Switch the focused window to floating mode when it is tiled

Example:

```toml
[[keybind]]
command = "TileToFloating"
modifier = ["modkey", "Shift"]
key = "f"
```

## ToggleFloating

Switch the focused window between floating and tiled mode.

Example:

```toml
[[keybind]]
command = "TileToFloating"
modifier = ["modkey", "Ctrl"]
key = "f"
```

## MoveWindowUp

Re-orders the focused window within the current workspace (moves up in order).

Default:

```toml
[[keybind]]
command = "MoveWindowUp"
modifier = ["modkey", "Shift"]
key = "Up"
```

## MoveWindowDown

Re-orders the focused window within the current workspace (moves down in order).

Default:

```toml
[[keybind]]
command = "MoveWindowDown"
modifier = ["modkey", "Shift"]
key = "Down"
```

## MoveWindowTop

Re-orders the focused window within the current workspace (moves to the top of the stack).

Default:

```toml
[[keybind]]
command = "MoveWindowTop"
modifier = ["modkey"]
key = "Return"
```

## MoveToTag

Moves a window to a given tag.

Partial default:

```toml
[[keybind]]
command = "MoveToTag"
value = "1"
modifier = ["modkey", "Shift"]
key = "1"
```

**Note: This command requires a value field to be specified**.

## FocusWindowUp

Focuses the window that is one higher in order on the current workspace.

Default:

```toml
[[keybind]]
command = "FocusWindowUp"
modifier = ["modkey"]
key = "Up"
```

## FocusWindowDown

Focuses the window that is one lower in order on the current workspace.

Default:

```toml
[[keybind]]
command = "FocusWindowDown"
modifier = ["modkey"]
key = "Down"
```

## NextLayout

Changes the workspace to a new layout.

Default:

```toml
[[keybind]]
command = "NextLayout"
modifier = ["modkey", "Control"]
key = "Up"
```

## PreviousLayout

Changes the workspace to the previous layout.

Default:

```toml
[[keybind]]
command = "PreviousLayout"
modifier = ["modkey", "Control"]
key = "Down"
```

## SetLayout

Changes the workspace to the specified layout.

Example:

```toml
[[keybind]]
command = "SetLayout"
value = "Monocle"
modifier = ["modkey"]
key = "m"
```

**Note: This command requires a value field to be specified**.

## RotateTag

Rotates the tag/layout. If the layout supports it, the tag will flip horizontally, vertically, or both. 
For example the fibonacci layout rotates in the four different directions.

Example:

```toml
[[keybind]]
command = "RotateTag"
modifier = ["modkey"]
key = "z"
```

## FocusWorkspaceNext

Moves the focus from the current workspace to the next workspace (next screen).

Default:

```toml
[[keybind]]
command = "FocusWorkspaceNext"
modifier = ["modkey"]
key = "Right"
```

## FocusWorkspacePrevious

Moves the focus from the current workspace to the previous workspace (previous screen).

Default:

```toml
[[keybind]]
command = "FocusWorkspacePrevious"
modifier = ["modkey"]
key = "Left"
```

## GotoTag

Changes the tag that is being displayed in a given workspace.

Partial default:

```toml
[[keybind]]
command = "GotoTag"
value = "9"
modifier = ["modkey"]
key = "9"
```

**Note: This command requires a value field to be specified**.

## FocusNextTag

Moves the focus from the current tag to the next tag in a given workspace.

Example:

```toml
[[keybind]]
command = "FocusNextTag"
modifier = ["modkey"]
key = "Right"
```

## FocusPreviousTag

Moves the focus from the current tag to the previous tag in a given workspace.

Example:

```toml
[[keybind]]
command = "FocusPreviousTag"
modifier = ["modkey"]
key = "Left"
```

## SwapTags

Swaps the tags in the current workspace with the tags in the previous workspace.

Default:

```toml
[[keybind]]
command = "SwapTags"
modifier = ["modkey"]
key = "w"
```

## IncreaseMainWidth

Increases the width of the currently focused window.

Example:

```toml
[[keybind]]
command = "IncreaseMainWidth"
value = "5"
modifier = ["modkey"]
key = "a"
```

**Note: This command requires a value field to be specified**.
**Note: This command does not apply to all layouts**.

## DecreaseMainWidth

Decreases the width of the currently focused window.

Example:

```toml
[[keybind]]
command = "DecreaseMainWidth"
value = "5"
modifier = ["modkey"]
key = "x"
```

**Note: This command requires a value field to be specified**.
**Note: This command does not apply to all layouts**.


## SetMarginMultiplier

Set the multiplier applied to the configured margin value.

Example:

```toml
[[keybind]]
command = "SetMarginMultiplier"
value = "2.5"
modifier = ["modkey"]
key = "m"
```

**Note: This command requires a value field to be specified**.
*Note: The value needs to be a positive float, use "0.0" for no margins at all, use "1.0" to reset.*
**Note: This command does not apply to all layouts**.

## ToggleFullScreen

Toggles the currently focused window between full screen and not full screen.

Example:

```toml
[[keybind]]
command = "ToggleFullScreen"
modifier = ["modkey"]
key = "f"
```
**Note: This is only available in LeftWM >=0.2.8.**

## ToggleScratchPad

Toggles the specified scratchpad.

Example:

```toml
[[keybind]]
command = "ToggleScratchPad"
value = "Alacritty" # Name set for the scratchpad
modifier = ["modkey"]
key = "p"
```
**Note: This command requires a value field to be specified**.
**Note: This is only available in LeftWM >=0.2.8.**

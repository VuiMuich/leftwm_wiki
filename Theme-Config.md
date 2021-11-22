# Configuring Your Themes

_All code snippets in this section refer to the file `~/.config/leftwm/themes/THEME/theme.toml`_  
Where THEME is the theme you want to configure, you can use 'current' if you are modifying the theme you are using.

## Terms

- _Default_ refers to the original `theme.toml` specified when LeftWM first runs.
- _Example_ refers to a snippet that is not in the original `theme.toml` but can be added or modified for additional features.

# Table of contents

- [Border Width](#border-width)
- [Margins](#margins)
- [Gutters](#gutters)
- [Border Colors](#border-colors)
- [On New Window Command](#on-new-window-command)
- [Minimal Requirements](#minimal-requirements)

# Border Width

This allows you to set the width of the border around each of the windows.

Default: ```border_width = 1```

# Margins

You can set the gap around each normal window and the gap around the working area of the workspace (where space isn't assigned for docks). The value can either be a single unsigned-integer or a array of up to 4 values with HTML format ([top, right, bottom, left]).

Defaults: 

```
margin = 10
workspace_margin = 10
```

Examples:

```
margin = [4, 5]              # Expands to [4, 4, 5, 5]
workspace_margin = [4, 5, 6] # Expands to [4, 5, 6, 6]
```
**Note: workspace_margin is only available in LeftWM >=0.2.8. It is currently only available through aur/leftwm-git or building from source.**

# Gutters

Gutters allow you to set a dedicated area for your dock if LeftWM cannot set this up automatically. Gutters can be set for each side, however if multiple gutters are set for the same side only the first one will be used. If you have multiple workspaces defined in `config.toml` you can specify a particular workspace on which to apply a specific gutter.

Examples:

```
[[gutter]]
side = "Top"
value = 20

[[gutter]]
side = "Left"
value = 20
```
The above settings will apply to all workspaces. If you want to only apply the left gutter to a specific workspace use this configuration:
```
[[gutter]]
side = "Left"
value = 20
wsid = 1
```
This assumes your `config.toml` includes a workspace definition with an id of 1.

**Note: This is only available in LeftWM >=0.2.8. It is currently only available through aur/leftwm-git or building from source.**

# Border Colors

You can set the color of the borders when a window is tiled or floating while unfocused, and for when a window is focused. The values should be hex values.

Defaults:

```
default_border_color = '#000000'
floating_border_color = '#000000'
focused_border_color = '#FF0000'
```

# On New Window Command

This is a command to run every time a new window is opened.

Example : ```on_new_window = 'echo Hello World'```

# Minimal Requirements
In order to be parsable a theme at minimum must contain the fields: 
`default_border_color`, `floating_border_color`, `focused_border_color`, `border_width` and `margin`
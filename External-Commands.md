This is a brief overview of the available external commands and their possible arguments.

You can pass the string of the external command directly to the pipe file. The file will be named "command-{display number}.pipe", where the display number can be found using ```echo $DISPLAY```.
For example from a shell you could use:
```shell
echo "SetLayout CenterMain" > $XDG_RUNTIME_DIR/leftwm/command-0.pipe
```
when on display 0.
If you are on the leftwm 0.2.8 or above, external commands can be passed in using leftwm-command. Commands that contain arguments require quotes.
For example:
```shell
leftwm-command "SetLayout CenterMain"
```
Commands can also be chained together, for example:
```shell
leftwm-command "SendWindowToTag 2" "SendWorkspaceToTag 0 2"
```
|Command | Arguments (if needed) | Notes |
|-|-|-|
| Reload | | Reloads leftwm |
| LoadTheme | `Path-to/theme.toml` | usually used in themes `up` script to load a theme |
| UnloadTheme | | usually used in themes `down` script to unload the theme |
| SetLayout | `LayoutName` | |
| NextLayout | | |
| PreviousLayout | | |
| RotateTag | | |
| SetMarginMultiplier | `multiplier as float` | set a factor by which the margin gets multiplied, use "1.0" to reset, negative values will be abs-converted |
| SwapScreen | | swaps two screens/workspaces |
| SendWorkspaceToTag | `workspace index` `tag_index` | both indices as integer, focuses `Tag` on `Workspace` |
| SendWindowToTag | `tag_index` | index as integer, sends currently focused window to `Tag` |
| MoveWindowToLastWorkspace | | moves currently focused window to last used workspace |
| MoveWindowToNextWorkspace | | moves currently focused window to next workspace |
| MoveWindowToPreviousWorkspace | | moves currently focused window to previous workspace |
| MoveWindowDown | | moves currently focused window down once |
| MoveWindowUp | | moves currently focused window up once |
| MoveWindowTop | | moves currently focused window to the top |
| FloatingToTile | | pushes currently focused floating window back to tiling mode |
| TileToFloating | | Switch currently focused tiled window to floating mode |
| ToggleFloating | | Switch currently focused window between tiled and floating mode |
| CloseWindow | | closes currently focused window |
| FocusWindowDown | | |
| FocusWindowUp | | |
| FocusWindowTop | `toggle` | Focus to top (main) window. If `toggle` is true, select the previous window if already on the top window. Only available in LeftWM >=0.2.11. |
| FocusNextTag | | |
| FocusPreviousTag | | |
| FocusWorkspaceNext | | |
| FocusWorkspacePrevious | | |
| ToggleFullScreen | | Makes currently focused window fullscreen/non-fullscreen |
| ToggleSticky | | Makes currently focused window sticky/non-sticky |
| ReturnToLastTag| | Switch back to the last visited tag |
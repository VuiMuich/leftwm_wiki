# Troubleshooting
## Table of contents

- [Configuration](#configuration)
- [Environment](#environment)

## Configuration
| Issue | Description | Solution |
|-|-|:-:|
| No config.ron file exists | LeftWM does not always ship with a `config.ron`. You will need to execute LeftWM at least once for one to be generated. | Try the following: ``` leftwm-worker ``` |
| Config.ron is not being parsed | LeftWM ships with a binary called leftwm-check. It might not be installed by the AUR. | Try the following: ``` leftwm-check ``` |
| Keybinding doesn't work/foreign keyboards | You may need to set the modifier (`modifier = []`) or to specify the name of the key, e.g. `eacute` for é. If it is a keypad number, use a modkey with value `lock`.| Refer to [this](https://github.com/leftwm/leftwm/blob/master/leftwm-core/src/utils/xkeysym_lookup.rs) list of keys |
| Keybinding doesn't work | It's likely you need to specify a value, a modifier, or have a typo. | Refer to the definition above or open an issue |

*Note: until the final deprecation of `toml` if no `config.ron` is found, leftwm will try to load a legacy `config.toml` only if that isn't found either it will write a new `config.ron` based on the intelnal `default` config.*

## Environment
| Issue | Description | Solution |
|-|-|:-:|
| Leftwm-check works, but I still get a black screen | You may not have a theme. | Attempt to execute a keybinding (e.g. terminal: modkey+Shift+Return). |
| Leftwm-check works, but I still get a black screen and keybindings don't work | You may not have XDG_RUNTIME_DIR set. | Install elogind or follow the guide. |

## Azerty mapping
| Key | Keysyms |
|-|:-:|
| & | ampersand |
| é | eacute |
| " | quotedbl |
| ' | apostrophe |
| ( | parenleft |
| è | egrave |
| _ | underscore |
| ç | ccedilla |
| à | agrave |

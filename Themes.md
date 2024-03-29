# Why have themes

With LeftWM, there are two types of configs:
* **LeftWM Configuration files:** LeftWM configurations are specific to you and don’t change for different themes. These are settings like keybindings, workspace locations, and names of desktops/tags. These settings can be found in `~/.config/leftwm/config.ron`.

* **Theme Configuration files:** The appearance of your desktop is different. It’s fun to try new looks and feels. It’s fun to tweak and customize the appearance (AKA: [ricing](https://www.reddit.com/r/unixporn/comments/3iy3wd/stupid_question_what_is_ricing/)). It’s fun to share so others can experience your awesome desktop! LeftWM is built around this concept. By pulling all these settings out into themes, you can now easily tweak, switch, and share your experiences. This configuration is spread between `theme.ron` and related files contained within a theme's folder.

**Important note:** *the `toml` language for config and theme files is about to be debrecated. Please consider migratin to our new standard language `ron`. For legacy docomentation have a look at the according wiki pages.*

# We want your themes

We are looking to expand the list of available themes for an upcoming release. If you enjoy making desktops look good please consider sharing by making a pull request on [the community themes repository](https://github.com/leftwm/leftwm-community-themes).


# Requirements for a theme - `up` and `down` scripts

A theme has only two requirements. An `up` and a `down` executable/script. They can be written in whatever makes you happy. The `up` script you guessed it starts up all the things that make your theme unique and awesome. The `down` script restores the environment to an un-themed state. A theme should be self contained if possible so that it can be shared and doesn’t interfere with other themes. For example when booting an application with a config file, put the config file in the theme folder instead of ~/.config. This way other themes can use the same application 

**Important note:** *as a convention unloading a theme should happen with a `down` script, which undos all of the things the `up` script had launched and should be symlinked or copied to `/tmp/leftwm-down-theme`. The following snippet is widely used:*
```bash
export SCRIPTPATH="$( cd "$(dirname "$0")" ; pwd -P )"

# Down the last running theme
if [ -f "/tmp/leftwm-theme-down" ]; then
    /tmp/leftwm-theme-down
    rm /tmp/leftwm-theme-down
fi
ln -s $SCRIPTPATH/down /tmp/leftwm-theme-down
```
Minimal `down` script:
```bash
#!/usr/bin/env bash

leftwm command "UnloadTheme"

# add kill commands for anything you launched in the 'up' script e.g.:
# pkill polybar
# pkill picom
```
*Note: for theme agnostic autostart you can use the `~/.config/autostart/` directory or a pair of `up`/`down` scripts in your `~/.config/leftwm/` directory.*

# Setup / selection of theme

There are two ways to setup a theme: you can use [leftwm-theme](https://github.com/leftwm/leftwm-theme/) or you can set a symlink yourself.

## Using LeftWM-theme
Install LeftWM-theme, as per the directions on [its Github](https://github.com/leftwm/leftwm-theme).

Update your list of themes:
```bash
leftwm-theme update
```
Install the theme you like:
```bash
leftwm-theme install "THEME NAME GOES HERE"
```
Apply the theme you like as the current theme:
```bash
leftwm-theme apply "THEME NAME GOES HERE"
```

## Using symlinks

To select a theme all that is required is that it’s located at: `~/.config/leftwm/themes/current`
It is strongly recommended that you do this with a symlink rather than creating a folder. Using a symlink makes it easy to save all your themes in the folder `~/.config/leftwm/themes` and switch between them using a symlink easily.

The following command would set the included basic_polybar to the current theme:

```bash
ln -s ~/.config/leftwm/themes/basic_polybar ~/.config/leftwm/themes/current
```



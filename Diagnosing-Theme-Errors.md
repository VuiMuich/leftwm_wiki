# Leftwm-theme Errors

## This theme is incompatible with the installed version of LeftWM.
This error signifies that a theme does not properly work with the installed version of leftwm as reported by the repository containing the theme. You can forcefully override this error to apply the theme with the -o or --override_checks flags, i.e. `leftwm-theme apply -o {THEME}` but note that this will not fix the underlying issue(s). See below for how to fix your theme:

1. See if the theme's git repo has any pull requests, if it does, you can pull those PRs into your local copy (located usually at ~/.config/leftwm/themes/{Theme Name}` and see if the theme works properly.
2. See below for specific changes that need to be made when migrating from a theme's compatible `leftwm_versions` available in `~/.config/leftwm/themes.toml`
3. Once you've made the change to your local copy of the theme, you can attempt to apply it using `leftwm-theme apply -o {Theme Name}`

Migrating from 0.2.7 or lower to higher versions (e.g. 0.3.0):
- change instances of `echo "UnloadTheme" > $XDG_RUNTIME_DIR/leftwm/commands.pipe` in `down` to `leftwm command "UnloadTheme"`
- change instances of `echo "LoadTheme $SCRIPTPATH/theme.toml" > $XDG_RUNTIME_DIR/leftwm/commands.pipe` to `leftwm command "LoadTheme $SCRIPTPATH/theme.toml"`
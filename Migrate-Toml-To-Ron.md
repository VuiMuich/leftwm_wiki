# Migtrating from `TOML` to `RON`

With LeftWM release 0.4.0 we introduced `RON` as config language and made it our default.
To smooth the transition `config.toml` is supported in a legacy mode, which means it can be loaded when no `config.ron` is found and `leftwm-check` will run its tests in the same case or when specifically pointed to a `toml` file.

Same goes for `theme.toml`.

To attempt automated migration of your `config` you can use the command `leftwm-check --migrate-toml-to-ron`/`leftwm-check -m` and remove the old `config.toml` at you own convenience.
We plan to add a equvalent feature to `leftwm-theme` soon. 

## Manual migration

### General

There are some aspects that apply to `config` and `theme` files, so lets have a look at those first:

1. The config/theme needs to be wrapped in `( ... )`
  Note: this is a stuct in Ron and it optionally can come with a name like `config( ... )`, we are not making any use of named stucts so for leftwm it can be omitted.
1. Before the main struct it is recommended to add a line with `#![enable(implicit_some)]` so the parser can infer a lot of cases, where wrapping the value into `Some( ... )` would be needed for any optional fields.
1. Comments use `//` so you can replace any `#` that does not belong to the previous bullet or to a color value
1. The assignement symbol is `:` so you can safely replace any occurence of `=` (or ` =` if you want to clean up the appearence in one go) with `:`
1. Inline-tables from `toml` become a struct in `ron` so you need to replace all the `{}` with `()`
1. `array`s in `toml` become `list`s in `ron`, both use `[ ... ]` so no change needed here
1. trailing commas are not bothering `ron` so you can safely add one after each `struc`, `list` or `key value pair`

### Config specific

1. The ron parser knows the types associated with a field, that means we don't need to use `Strings` for assigning those fields. This applies to:
  - `focus_behaviour` values: `Sloppy`, `ClickTo`, `Driven`
  - `layout_mode` values: `Tag`, `Workspace`
  - `Layout` values: `CenterMain`, `Fibonacci`, `Monocle` etc.
  - `Command` values: `SoftReload`, `GoToTag`, `ToggleSticky` etc.
    Node: The `value` field in keybinds still uses a `String` as its value
1. If you used `inline arrays` for keybinds in `toml` (often referred to as "compact notation or syntax") this step might already been taken care of by the replacement of `{}` with `()`
  Otherwise you need a couple of extra steps:
  - remove all the `[[keybind]]` lines
  - wrap each keybind in `( ... ),` (Note the comma as all keybinds will form a list)
  - wrap all the keybinds in a `keybind: [ ... ]` list item

### Theme specific 

Currently there are not many points to follow for themes specifically:
- `Gutters` are simply a list of `gutter` structs and their `side` fields use the values `Bottom`, `Left`, `Right`, `Top` with no quotes needed
- change the `up` script to load `theme.ron`

### Usefull tips

- as `ron` is inherently rusty, using `Rust` syntax highlighting works in many editors, on github or discord just fine
- ron doesn't care about whit spaces, so feel free to format your file to your liking
- most steps can be easily recorded into a macro (see documentation of you editor of choice) or be applied to the whole file at once

# Underglow (tuicr)

A dark colour scheme for [tuicr](https://github.com/michelegera/tuicr), derived from a photo of a
dark desk lit by RGB keyboard underglow: violet/lavender glow, electric blue underglow, a teal-cyan
terminal glow, and an amber and a crimson trackball on a near-black desk surface.

The scheme ships two files:

| File | Purpose |
| --- | --- |
| `underglow.toml` | The tuicr theme: panel chrome, diff colours, file-status markers, messages, mode indicator. |
| `underglow-syntax.tmTheme` | The syntax highlighting theme, referenced by `underglow.toml` via `syntax_theme`. |

## Palette

| Role | Colour |
| --- | --- |
| Background | `#0B0D14` |
| Raised background / panel | `#12141F` |
| Surface | `#191C2A` |
| Surface highlight | `#222739` |
| Selection background | `#2A2F47` |
| Text | `#C6CADF` |
| Text bright | `#E7EAF6` |
| Text muted | `#98A0B8` |
| Text dim | `#646C88` |
| Violet accent (underglow) | `#9D8CFF` / bright `#C3BAFF` |
| Blue (underglow) | `#4C8DF6` / bright `#89B7FF` |
| Cyan (terminal glow) | `#35B6D8` / bright `#7BDCF3` |
| Teal-green | `#45C2A0` / bright `#7EE4C6` |
| Amber (trackball) | `#E0A93C` / bright `#F5CE7E` |
| Crimson (trackball) | `#E2515F` / bright `#FF8B96` |
| Magenta | `#C26BE8` / bright `#E4A9FF` |
| Black / white | `#14161F` / `#B9BED4` |

Diff and syntax backgrounds use tints of the palette mixed 22% over the background: tint green
`#183533`, tint red `#3A1C24`, tint blue `#192946`, tint violet `#2B2948`, tint cyan `#14323F`,
tint amber `#3A2F1D`.

## Install

Copy both files into your tuicr themes directory:

```sh
mkdir -p ~/.config/tuicr/themes
cp underglow.toml underglow-syntax.tmTheme ~/.config/tuicr/themes/
```

Then set the theme in `~/.config/tuicr/config.toml`:

```toml
theme = "underglow"
```

tuicr reads its config from `~/.config/tuicr/config.toml` and honours `$XDG_CONFIG_HOME`, so the
config path becomes `$XDG_CONFIG_HOME/tuicr/config.toml` when that variable is set.

### The `syntax_theme` path

`underglow.toml` points at its syntax theme with:

```toml
syntax_theme = "underglow-syntax.tmTheme"
```

This path is resolved **relative to the theme file**, not to the current working directory and not to
the config directory. Keeping the `.tmTheme` file next to `underglow.toml` in
`~/.config/tuicr/themes/` is what makes the relative path resolve. If you rename or move either file
independently, update `syntax_theme` to match.

The theme name used in `config.toml` is the file's base name without the extension, so the file
`underglow.toml` is selected as `theme = "underglow"`. Local theme names shadow bundled themes with
the same name; `underglow` does not collide with a bundled tuicr theme.

## Preview

Run tuicr with the theme selected for that session only:

```sh
tuicr --theme underglow
```

The theme applies to the whole TUI, so open a diff or a file to see the syntax colours. For example,
to annotate a single file:

```sh
tuicr --theme underglow --file path/to/file.rs
```

## Switching at runtime

Inside the TUI, press `:` to open the command palette and run `:theme` to pick a colour theme from a
list that includes `underglow`. Choosing it applies the theme for the current session without
editing `config.toml`.

## Verification

The theme was validated against tuicr 0.28.0:

- `underglow.toml` parses as flat TOML with exactly the 44 keys of tuicr's `Theme` struct, each a
  `#RRGGBB` string. tuicr rejects a local theme that is missing any of them.
- `underglow-syntax.tmTheme` parses as a valid XML plist with the expected metadata
  (`Underglow Syntax`, `theme.dark.underglow.syntax`, author `Underglow`, `sRGB`) and the same scope
  coverage as the reference theme it was ported from.
- Loading the theme end-to-end with
  `XDG_CONFIG_HOME=<temp> tuicr --theme underglow --no-update-check --file <file>` succeeds and
  renders in the Underglow palette.
- A copy of the theme with a single key removed is rejected with a non-zero exit and the message
  `Error: Theme key 'fg_dim' is required`.

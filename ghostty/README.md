# Underglow

A Ghostty colour scheme derived from a photo of a dark desk with RGB keyboard
underglow: violet/lavender glow, electric blue underglow, teal-cyan terminal
glow, an amber trackball and a crimson trackball on a near-black desk.

Palette inspired by a photograph by [ZSA](https://www.zsa.io/) — [see the source image](../screenshots/underglow.jpg).

The background is near-black (`#0B0D14`), the ANSI palette is built from the
glow colours, and the 256-colour range is generated from the base 16 with
`palette-generate = true`.

## Install

Copy the theme file to Ghostty's themes directory. The file name is the theme
name and must not have an extension:

```sh
mkdir -p ~/.config/ghostty/themes
cp ghostty/underglow ~/.config/ghostty/themes/underglow
```

Then reference the theme in your Ghostty config file, `~/.config/ghostty/config`:

```ini
theme = underglow
```

A snippet with the same content is available in [`config`](config) in this
directory.

## Reload

After installing the theme or editing the config, reload Ghostty's
configuration with `Cmd+Shift+,` on macOS.

## Verify

Confirm that Ghostty sees the theme:

```sh
ghostty +list-themes
```

`underglow` should appear in the output.

To check the colours in a running terminal, print one line per ANSI colour:

```sh
printf '\033[0m  normal\n\033[1m  bold\n\033[4m  underline\n\033[7m  reverse\n\033[38;5;196m  bright red\n'
```

The bright variants of each base colour are palette indices 8-15.

## Notes

- Ghostty rejects 8-digit hex colours with an alpha channel (`#RRGGBBAA`).
  Colours must be 6-digit hex (`#RRGGBB`). Use the `background-opacity` option
  to make the background transparent instead of embedding alpha in the colour.
- The theme file must live in `~/.config/ghostty/themes/`. A theme name
  containing a path separator is an error, and relative paths are not allowed.
- Your own `~/.config/ghostty/config` settings override the values in the
  theme file.
- A theme file cannot set `theme` or `config-file`; those options are silently
  ignored there.

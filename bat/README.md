# Underglow (bat)

A dark syntax theme for [bat](https://github.com/sharkdp/bat), derived from a
photo of a dark desk lit by RGB keyboard underglow: violet and electric-blue
light bleeding across the desk edge, a teal-cyan terminal glow, an amber
trackball and a crimson one on a near-black surface.

The palette leans on violet and cyan accents over a near-black background
(`#0B0D14`), with amber for constants and crimson for deletions in diffs.

## Requirements

- `bat` >= 0.16

## Install

Copy the theme into bat's theme directory:

```sh
cp Underglow.tmTheme "$(bat --config-dir)/themes/"
```

Then rebuild bat's asset cache so it picks up the new file:

```sh
bat cache --build
```

## Usage

Select the theme on the command line:

```sh
bat --theme="Underglow" README.md
```

Or via the `BAT_THEME` environment variable:

```sh
export BAT_THEME="Underglow"
```

Or permanently, by adding the option to bat's config file:

```sh
echo '--theme="Underglow"' >> "$(bat --config-file)"
```

## Verification

Confirm the theme is registered:

```sh
bat --list-themes | grep Underglow
```

Render a file with it:

```sh
bat --theme="Underglow" --color=always README.md
```

## Palette

| Role | Colour |
| --- | --- |
| Background | `#0B0D14` |
| Text | `#C6CADF` |
| Text bright | `#E7EAF6` |
| Text muted | `#98A0B8` |
| Text dim | `#646C88` |
| Violet accent | `#9D8CFF` |
| Blue | `#4C8DF6` |
| Cyan | `#35B6D8` |
| Teal-green | `#45C2A0` |
| Amber | `#E0A93C` |
| Crimson | `#E2515F` |
| Magenta | `#C26BE8` |

## Licence

MIT

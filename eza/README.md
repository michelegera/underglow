# Underglow — an eza colour scheme

Underglow is a colour scheme for [eza](https://github.com/eza-community/eza), derived from a
photograph of a dark desk lit by RGB keyboard underglow: violet and lavender light spilling across
a near-black surface, an electric-blue underglow strip, a teal-cyan terminal glow, and an amber
and a crimson trackball.

The theme is a single YAML file, `theme.yml`, covering file kinds, permissions, sizes, users,
links, Git status, security contexts, file types, and the scalar metadata colours.

## Requirements

- `eza` 0.21 or newer, with YAML theme file support.
- A terminal that supports 24-bit (truecolor) escape sequences. eza emits truecolor codes for the
  hex values in this theme, so 8- and 16-colour terminals will approximate them.

Check your version with:

```sh
eza --version
```

The theme file format is version-specific. On eza 0.23.x the file is read from the config
directory; older or newer releases may add, rename, or remove keys.

## Install

Copy `theme.yml` into your eza config directory:

```sh
mkdir -p ~/.config/eza
cp theme.yml ~/.config/eza/theme.yml
```

`eza` looks for `~/.config/eza/theme.yml` (or `~/.config/eza/theme.yaml`) by default.

Alternatively, keep the file anywhere and point `EZA_CONFIG_DIR` at the directory that contains
it:

```sh
export EZA_CONFIG_DIR="$HOME/.config/eza"
```

`EZA_CONFIG_DIR` takes precedence over the default location. Inside that directory, `eza` reads
`theme.yml` first and falls back to `theme.yaml`.

To use the scheme without touching your config directory, point `EZA_CONFIG_DIR` at a directory
holding a copy of this file:

```sh
mkdir -p ~/themes/underglow
cp theme.yml ~/themes/underglow/theme.yml
export EZA_CONFIG_DIR="$HOME/themes/underglow"
```

Add that `export` line to your shell profile to make it persistent.

## Overriding individual colours

`EZA_COLORS` and `LS_COLORS` take precedence over the values in `theme.yml`. Use them to tweak a
single colour without editing the file, for example to make directories red:

```sh
EZA_COLORS="di=01;31" eza -la
```

`EZA_COLORS` uses the same key syntax as `LS_COLORS`, with a few eza-specific extensions such as
`ur` (user read), `uw` (user write), and `ux` (user execute). For the full list, see
`man eza_colors` and `man eza_colors-explanation`.

Keys that you do not set in `EZA_COLORS` or `LS_COLORS` continue to use the colours from
`theme.yml`.

To ignore the theme file entirely, point `EZA_CONFIG_DIR` at an empty directory:

```sh
EZA_CONFIG_DIR="$(mktemp -d)" eza -la
```

## Verifying the installation

List a directory and inspect the escape sequences. `#C6CADF` should appear as `38;2;198;202;223`,
`#4C8DF6` as `38;2;76;141;246`, and `#E0A93C` as `38;2;224;169;60`:

```sh
eza --color=always -la /tmp | head -4 | cat -v
```

Confirm the theme file is being picked up from a non-default location:

```sh
mkdir -p /tmp/eza-underglow
cp theme.yml /tmp/eza-underglow/
EZA_CONFIG_DIR=/tmp/eza-underglow eza --color=always -la /tmp | head -4 | cat -v
```

Check Git status colours inside a repository:

```sh
EZA_CONFIG_DIR=/tmp/eza-underglow eza --color=always -la --git
```

`eza` warns on stderr about any key it does not recognise. A clean installation produces no such
warnings:

```sh
EZA_CONFIG_DIR=/tmp/eza-underglow eza --color=always -la /tmp 2>&1 >/dev/null
```

The command above should print nothing.

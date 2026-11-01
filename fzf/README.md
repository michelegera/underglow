# Underglow · fzf

`fzf.conf` is the [fzf](https://github.com/junegunn/fzf) colour scheme for **Underglow**, a dark
palette derived from a photo of a dark desk lit by RGB keyboard underglow: violet/lavender glow,
electric blue underglow, teal-cyan terminal glow, an amber trackball and a crimson trackball on a
near-black desk.

Palette inspired by a photograph by [ZSA](https://www.zsa.io/) — [see the source image](../screenshots/underglow.jpg).

fzf has no theme-file format. The portable way to ship a scheme is an **options file** that fzf
reads through the `FZF_DEFAULT_OPTS_FILE` environment variable ("The location of the file that
contains the default options" — `man fzf`). The file contains plain fzf command-line options, one
per line, exactly as if they were typed at the shell. That means it is not an `export
FZF_DEFAULT_OPTS=...` line, and it is not shell syntax.

## Palette

| Role | Hex |
| --- | --- |
| background | `#0B0D14` |
| raised background | `#12141F` |
| surface | `#191C2A` |
| surface highlight | `#222739` |
| selection bg | `#2A2F47` |
| selection fg | `#E7EAF6` |
| text | `#C6CADF` |
| text bright | `#E7EAF6` |
| text muted | `#98A0B8` |
| text dim | `#646C88` |
| accent (violet underglow) | `#9D8CFF` |
| accent bright | `#C3BAFF` |
| blue (blue underglow) | `#4C8DF6` |
| blue bright | `#89B7FF` |
| cyan (teal terminal glow) | `#35B6D8` |
| cyan bright | `#7BDCF3` |
| teal-green | `#45C2A0` |
| teal-green bright | `#7EE4C6` |
| amber (trackball) | `#E0A93C` |
| amber bright | `#F5CE7E` |
| crimson (trackball) | `#E2515F` |
| crimson bright | `#FF8B96` |
| magenta | `#C26BE8` |
| magenta bright | `#E4A9FF` |
| black | `#14161F` |
| white | `#B9BED4` |

## Install

Copy the file to the conventional location:

```sh
mkdir -p ~/.config/fzf
cp fzf/fzf.conf ~/.config/fzf/fzf.conf
```

Then point fzf at it in `~/.zshrc`:

```sh
export FZF_DEFAULT_OPTS_FILE=~/.config/fzf/fzf.conf
```

Any path works — `FZF_DEFAULT_OPTS_FILE` may point at the file wherever you keep it.

## Layering on top of an existing `FZF_DEFAULT_OPTS`

`FZF_DEFAULT_OPTS_FILE` and `FZF_DEFAULT_OPTS` are both read, with the options file applied after
the environment options, so the file's values win on conflicting keys. To keep the rest of your
setup and only take the colours from Underglow, source the file's colour line rather than the
whole file:

```sh
export FZF_DEFAULT_OPTS="--height=40% --info=inline-right $FZF_DEFAULT_OPTS"
export FZF_DEFAULT_OPTS_FILE=~/.config/fzf/fzf.conf
```

If you want the colours only and none of the file's layout options, extract them in your shell:

```sh
export FZF_DEFAULT_OPTS="--color=$(sed -n 's/^--color=//p' ~/.config/fzf/fzf.conf)"
```

To use the full file plus extra options, keep `FZF_DEFAULT_OPTS_FILE` set and add your flags on
the command line (`fzf --border=sharp`) or via `FZF_DEFAULT_OPTS` for the keys that should not be
overridden.

## Editing

The file is plain fzf options, so it can be edited freely with any text editor. Each line is one
option:

- `--color=...` — the colour scheme. The value is `[BASE_SCHEME][,COLOR_NAME[:ANSI_COLOR]]...`,
  comma-separated, base scheme first (`dark`, `light`, `base16`, `bw`). Colours accept `#rrggbb`,
  `0-255`, or names; ANSI attributes (`bold`, `dim`, `italic`, ...) apply to foreground colours only.
- `--layout`, `--height`, `--info`, `--border`, `--border-label`, `--marker`, `--pointer` — layout
  and glyph options.

Note: the `nth` key in fzf 0.74.5 accepts ANSI attributes only, not a colour, so it is not set here.
`border-label` is not a valid colour key; the key is `label`.

## Verification

Check the colour line parses (exit status 0 or 1 for "no match", and no error output):

```sh
fzf --color="$(sed -n 's/^--color=//p' fzf/fzf.conf)" --filter=zzz </dev/null
```

Check the whole file parses as options:

```sh
FZF_DEFAULT_OPTS_FILE="$PWD/fzf/fzf.conf" fzf --filter=zzz </dev/null
```

Both were verified against fzf 0.74.5. An unknown colour key makes fzf exit 2 with
`invalid color specification`, so a clean run is a real check.

To confirm the file is actually in effect, filter a list and look at the highlighted match, or run
fzf normally and check the window frame label reads `underglow`.

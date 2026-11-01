# Underglow — lazygit theme

A lazygit colour scheme derived from a photo of a dark desk lit by RGB keyboard
underglow: violet/lavender glow, electric blue underglow, teal-cyan terminal glow,
an amber trackball and a crimson trackball, on a near-black desk.

`config.yml` in this directory contains **only** the `gui.theme` block.

## Merge, don't replace

`config.yml` is a fragment, not a complete lazygit configuration. If you copy it
over your own `config.yml`, you will delete your keybindings, custom commands,
`git:` settings and everything else you have configured.

Merge the `gui.theme` mapping into your existing config instead. If your config
already has a `theme:` block, replace only that block with the one from this file.

### Merge example

Existing `~/.config/lazygit/config.yml`:

```yaml
git:
  overrideGpg: true
gui:
  nerdFontsVersion: "3"
  commitGraphStyle: "detailed"
  theme:
    activeBorderColor: ['#AABBCC', bold]
    # ... the rest of your current theme
```

After merging in Underglow:

```yaml
git:
  overrideGpg: true
gui:
  nerdFontsVersion: "3"
  commitGraphStyle: "detailed"
  theme:
    activeBorderColor: ['#9D8CFF', bold]
    inactiveBorderColor: ['#222739']
    searchingActiveBorderColor: ['#E0A93C', bold]
    optionsTextColor: ['#4C8DF6']
    selectedLineFgColor: ['#E7EAF6']
    selectedLineBgColor: ['#2A2F47']
    inactiveViewSelectedLineBgColor: ['#191C2A']
    cherryPickedCommitFgColor: ['#0B0D14']
    cherryPickedCommitBgColor: ['#C3BAFF']
    markedBaseCommitFgColor: ['#0B0D14']
    markedBaseCommitBgColor: ['#E0A93C']
    unstagedChangesColor: ['#E2515F']
    defaultFgColor: ['#C6CADF']
    authorColors:
      '*': '#C26BE8'
    branchColorPatterns:
      '^\*\s': '#45C2A0'
      '^\+\s': '#45C2A0'
      '^-\s': '#E2515F'
      ' -> ': '#E0A93C'
      '^remotes/': '#35B6D8'
      '^tags/': '#C26BE8'
```

To append the theme to a config that has no `theme:` block yet, copy it into a
temporary file and append:

```sh
cp ~/.config/lazygit/config.yml /tmp/lazygit-config.yml
cat underglow/lazygit/config.yml >> /tmp/lazygit-config.yml
lazygit --use-config-file=/tmp/lazygit-config.yml
```

Note that `cat >>` appends a second `gui:` key if your file already has one.
YAML duplicate keys are an error, so use the merge example above for an existing
config, and append only for a config that has no `gui:` section at all.

## Config file locations

lazygit reads its configuration from, in order of precedence:

| Platform | Path |
| --- | --- |
| Linux, macOS (XDG) | `~/.config/lazygit/config.yml` |
| macOS (native) | `~/Library/Application Support/lazygit/config.yml` |

The XDG location takes precedence on macOS when `XDG_CONFIG_HOME` is set or the
default `~/.config` path exists. You can confirm which directory lazygit is
actually using with:

```sh
lazygit --print-config-dir
```

## Testing without changing your config

The `--use-config-file` flag makes lazygit read the given file instead of your
own config, which is the safest way to preview the theme:

```sh
lazygit --use-config-file=/path/to/underglow/lazygit/config.yml
```

Combine it with a copy of your own config if you want to preview the theme
alongside your existing settings:

```sh
cp ~/.config/lazygit/config.yml /tmp/lazygit-config.yml
cat /path/to/underglow/lazygit/config.yml >> /tmp/lazygit-config.yml
lazygit --use-config-file=/tmp/lazygit-config.yml
```

To make it permanent, merge the `gui.theme` block into your own config file
using the merge example above.

## Palette

| Role | Colour |
| --- | --- |
| Background | `#0B0D14` |
| Raised background | `#12141F` |
| Surface | `#191C2A` |
| Surface highlight | `#222739` |
| Selection background | `#2A2F47` |
| Selection foreground | `#E7EAF6` |
| Text | `#C6CADF` |
| Text bright | `#E7EAF6` |
| Text muted | `#98A0B8` |
| Text dim | `#646C88` |
| Accent (violet underglow) | `#9D8CFF` |
| Accent bright | `#C3BAFF` |
| Blue (blue underglow) | `#4C8DF6` |
| Blue bright | `#89B7FF` |
| Cyan (teal terminal glow) | `#35B6D8` |
| Cyan bright | `#7BDCF3` |
| Teal-green | `#45C2A0` |
| Teal-green bright | `#7EE4C6` |
| Amber (trackball) | `#E0A93C` |
| Amber bright | `#F5CE7E` |
| Crimson (trackball) | `#E2515F` |
| Crimson bright | `#FF8B96` |
| Magenta | `#C26BE8` |
| Magenta bright | `#E4A9FF` |
| Black | `#14161F` |
| White | `#B9BED4` |

## Theme keys

The file sets all 15 keys of lazygit's `gui.theme` schema:

`activeBorderColor`, `inactiveBorderColor`, `searchingActiveBorderColor`,
`optionsTextColor`, `selectedLineFgColor`, `selectedLineBgColor`,
`inactiveViewSelectedLineBgColor`, `cherryPickedCommitFgColor`,
`cherryPickedCommitBgColor`, `markedBaseCommitFgColor`,
`markedBaseCommitBgColor`, `unstagedChangesColor`, `defaultFgColor`,
`authorColors`, `branchColorPatterns`.

Each key takes at most one colour plus any of the attributes `bold`, `dim`,
`reverse`, `underline` and `strikethrough`. Hex colours are quoted so that YAML
does not read the leading `#` as the start of a comment.

## Verification

The file has been checked against lazygit 0.66.2:

```sh
# The config parses as valid YAML
ruby -ryaml -e 'YAML.load_file(ARGV[0]); puts "yaml ok"' config.yml

# lazygit accepts the file and reports no configuration warnings
lazygit --use-config-file=/path/to/underglow/lazygit/config.yml --print-config-dir
lazygit --use-config-file=/path/to/underglow/lazygit/config.yml --version
```

Both commands exit `0` and print nothing to stderr.

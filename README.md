# Deseret News theme for Omarchy

A dark theme built from the official *Deseret News Brand Guide* (v.02-2, 8 Aug 2019).
The primary logo is black with a yellow period; this theme is that mark turned
into a desktop — an off-black newsroom surface with Deseret Yellow carrying
every accent.

## Palette

| Brand color | Hex | Role |
| --- | --- | --- |
| Deseret Yellow (Pantone 109U) | `#ffd217` | `accent` — cursor, selected rows, highlights |
| Off-Black | `#1e1e1e` | `background` |
| True Black | `#000000` | `darker_background` |
| Gray 1 | `#f2f2f2` | `bright_foreground` |
| Gray 2 | `#424242` | `muted` — inactive borders, rules |

The brand defines only yellow, grays and black, so the ANSI syntax colors are
derived: a warm, low-saturation set chosen to sit *under* the yellow rather
than compete with it. Window borders use a muted brass (`#a98d19`) rather than
full-strength yellow, since that chrome is on screen constantly.

## Install

```bash
omarchy theme install https://github.com/johnpipi/omarchy-deseret-news-theme
```

## Backgrounds

| File | |
| --- | --- |
| `0-honeycomb.png` | Futuristic honeycomb, dense top-left, dissolving toward the logo |
| `1-period.png` | A hairline rule ending in the yellow period |
| `2-beehive.png` | The beehive skep |
| `3-nameplate.png` | The wordmark between two yellow rules |

Editable SVG sources for all four are in `sources/`.

## Optional: themed branding

Omarchy reads its fastfetch logo from `branding/about.txt` and its screensaver
art from `branding/screensaver.txt`. Neither looks at the active theme, so a
theme cannot change them on its own. Two opt-in pieces close that gap.

**1. Sync the art with the theme.** This hook copies `about.txt` and
`screensaver.txt` from the active theme into branding on every theme switch,
and restores Omarchy's stock art for any theme that doesn't ship its own. It is
generic — any theme with those files at its root works, not just this one.

```bash
omarchy hook install theme-set ~/.config/omarchy/themes/deseret-news/theme-branding.hook
```

That gives you the box-drawing beehive as the fastfetch logo (21x8, so it stays
intact in narrow terminals) and the honeycomb screensaver.

To render the logo in the theme's yellow rather than Omarchy's green, copy
`/etc/fastfetch/config.jsonc` to `~/.config/fastfetch/config.jsonc` and change
`green` to `yellow`. Those are ANSI names, so they follow whatever theme is
active rather than pinning a hex.

**2. Paint the screensaver in brand gold.** `omarchy-screensaver` calls
`ttfx --random-effect`, which picks both the effect *and* its palette at
random. This shim rewrites only that one invocation, rotating through four
effects configured with brand golds; every other `ttfx` call passes through
untouched.

```bash
sudo install -m 755 ~/.config/omarchy/themes/deseret-news/ttfx-yellow-shim /usr/local/bin/ttfx
```

It has to live in `/usr/local/bin` because `/usr/share/omarchy/bin` comes first
on the Hyprland session PATH, so `omarchy-screensaver` itself can't be shadowed
— but `ttfx` (in `/usr/bin`) can. Remove with `sudo rm /usr/local/bin/ttfx`.

## Alternatives

`sources/` holds editable SVGs for the backgrounds plus swap-in variants:

| File | |
| --- | --- |
| `about-honeycomb.txt` | 7-hex honeycomb cluster logo (17x7) |
| `about-skep-solid.txt` | filled beehive logo (54x22) |
| `about-skep-outline.txt` | outline beehive logo (54x24) |
| `screensaver-wordmark.txt` | wordmark-only screensaver |

Copy one over `about.txt` or `screensaver.txt` and re-apply the theme.

## Trademarks

The Deseret News name, wordmark, and beehive are trademarks of Deseret News.
The MIT license below covers the theme configuration and the generated artwork
in this repository, not those marks.

## License

MIT — see [LICENSE](LICENSE).

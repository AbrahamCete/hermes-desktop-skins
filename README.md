<div align="center">

# Hermes Desktop Skins

**Pixel-art wallpaper themes for Hermes Desktop.**

Dithered, hand-tuned pixel art for the three art slots of the desktop app: the hero above the wordmark and the two sidebar panels.
Install once and switch themes from the theme picker.

<sub>FOR <a href="https://github.com/NousResearch/hermes-agent">HERMES DESKTOP</a> &nbsp;·&nbsp; 2 COLLECTIONS &nbsp;·&nbsp; 12 THEMES</sub>

<br /><br />

![Hermes Desktop with the GT3 RS Lava Orange theme](themes/gt3rs/lava/screenshot.png)

</div>

## Install

You need Hermes Desktop 0.22.2 or later.

1. In Hermes Desktop, open **Capabilities → Plugins**, click **Install from Git**, paste `https://github.com/AbrahamCete/hermes-desktop-skins` and install. From a terminal: `hermes plugins install AbrahamCete/hermes-desktop-skins`.
2. Flip the plugin's **Desktop** switch on. Desktop plugins installed from a package start turned off.
3. Pick a theme in the theme picker.

## Collections

Themes come in collections: one subject, several looks. Click a banner to see every theme of a collection applied to Hermes Desktop.

<!-- catalog:start -->
### [GT3 RS](themes/gt3rs) &nbsp;<sub>7 themes</sub>

<a href="themes/gt3rs"><img src="themes/gt3rs/banner.png" alt="GT3 RS: Guards Red, Lava Orange, Racing Yellow, Python Green, Shark Blue, Ruby Star, GT Silver" /></a>

Seven factory colours of the 992 GT3 RS. Same car, different paint. **[Browse the collection →](themes/gt3rs)**

<sub>`gt3rs-guards` `gt3rs-lava` `gt3rs-yellow` `gt3rs-python` `gt3rs-shark` `gt3rs-ruby` `gt3rs-silver`</sub>

### [Space Race](themes/space) &nbsp;<sub>5 themes</sub>

<a href="themes/space"><img src="themes/space/banner.png" alt="Space Race: Saturn V, Apollo 11, Voyager, Space Shuttle, Spacewalk" /></a>

Five moments of the space age, from the Saturn V to the spacewalk. **[Browse the collection →](themes/space)**

<sub>`space-saturn` `space-apollo` `space-voyager` `space-shuttle` `space-eva`</sub>

<details>
<summary><b>Every theme</b> (12)</summary>

| Collection | Theme | Id | Files |
|---|---|---|---|
| [GT3 RS](themes/gt3rs) | Guards Red | `gt3rs-guards` | [screenshot](themes/gt3rs/guards/screenshot.png) · [art](themes/gt3rs/guards/art) |
| [GT3 RS](themes/gt3rs) | Lava Orange | `gt3rs-lava` | [screenshot](themes/gt3rs/lava/screenshot.png) · [art](themes/gt3rs/lava/art) |
| [GT3 RS](themes/gt3rs) | Racing Yellow | `gt3rs-yellow` | [screenshot](themes/gt3rs/yellow/screenshot.png) · [art](themes/gt3rs/yellow/art) |
| [GT3 RS](themes/gt3rs) | Python Green | `gt3rs-python` | [screenshot](themes/gt3rs/python/screenshot.png) · [art](themes/gt3rs/python/art) |
| [GT3 RS](themes/gt3rs) | Shark Blue | `gt3rs-shark` | [screenshot](themes/gt3rs/shark/screenshot.png) · [art](themes/gt3rs/shark/art) |
| [GT3 RS](themes/gt3rs) | Ruby Star | `gt3rs-ruby` | [screenshot](themes/gt3rs/ruby/screenshot.png) · [art](themes/gt3rs/ruby/art) |
| [GT3 RS](themes/gt3rs) | GT Silver | `gt3rs-silver` | [screenshot](themes/gt3rs/silver/screenshot.png) · [art](themes/gt3rs/silver/art) |
| [Space Race](themes/space) | Saturn V | `space-saturn` | [screenshot](themes/space/saturn/screenshot.png) · [art](themes/space/saturn/art) |
| [Space Race](themes/space) | Apollo 11 | `space-apollo` | [screenshot](themes/space/apollo/screenshot.png) · [art](themes/space/apollo/art) |
| [Space Race](themes/space) | Voyager | `space-voyager` | [screenshot](themes/space/voyager/screenshot.png) · [art](themes/space/voyager/art) |
| [Space Race](themes/space) | Space Shuttle | `space-shuttle` | [screenshot](themes/space/shuttle/screenshot.png) · [art](themes/space/shuttle/art) |
| [Space Race](themes/space) | Spacewalk | `space-eva` | [screenshot](themes/space/eva/screenshot.png) · [art](themes/space/eva/art) |

</details>
<!-- catalog:end -->

## Download the art

Themes are grouped by collection under [`themes/`](themes), one folder per theme:

```text
themes/
└── gt3rs/                  a collection
    ├── README.md             its gallery
    ├── banner.png            every theme side by side
    ├── art-sheet.png         all its pixel art
    ├── collection.json       title, description, order
    └── lava/                 a theme (id gt3rs-lava)
        ├── art/              the three pixel images, at native size
        │   ├── hero.png        450×225 · above the wordmark
        │   ├── top.png         160×120 · top of the sidebar
        │   └── bottom.png      160×133 · bottom of the sidebar
        ├── raw/              the full-resolution source images (colour variants
        │                     reuse another theme's via "source" in theme.json)
        ├── screenshot.png    the theme applied to Hermes Desktop
        ├── preview.png       a quick layout mock
        └── theme.json        palette, colours and dither settings
```

The art is meant to be shown at 2× with nearest-neighbour scaling, which is how the app renders it.

## How the themes are made

```text
prompts.txt ──► raw/*.png ──► art/*.png ──► desktop/plugin.js
        generate.py      pixelate.py      build.py
        (Codex image     (crop, resize,   (embeds every theme
         generation)      4-colour         into one plugin)
                          ordered dither)
```

| Tool | What it does |
|---|---|
| `tools/generate.py <theme-dir>…` | Renders each theme's `prompts.txt` into `raw/` with Codex image generation, in parallel |
| `tools/pixelate.py <theme-dir>` | Crops and downsamples the raw images to each slot and dithers them onto the theme ramp |
| `tools/recolor.py <base-dir> <new-dir> <label> <body> <shadow> <highlight> [bg]` | Creates a colour variant that reuses the base theme's raw art |
| `tools/build.py` | Bundles every theme into `plugin.yaml` + `desktop/plugin.js` |
| `tools/screenshot.mjs [theme ids…]` | Takes a real Hermes Desktop screenshot of each theme from an isolated, empty profile |
| `tools/preview.py <theme-dir>` | Renders a quick layout mock without launching the app |
| `tools/sheet.py <collection-dir> <out.png>` | Renders the side-by-side art sheet of a collection |
| `tools/catalog.py` | Builds every collection's banner, art sheet and gallery page, and the collection index in this README |

Requirements: Python 3 with Pillow, and Node 22 for the screenshots.

## License

[MIT](LICENSE). The layout CSS is adapted from [Hermes Pantheon](https://github.com/Adolanium/hermes-pantheon) (MIT).

> **Community project**
>
> Hermes Desktop Skins is an independent fan project. It is not affiliated with, endorsed by, or sponsored by Nous Research, the Hermes Agent project, or Porsche AG. Hermes, Hermes Agent, Porsche, 911 and GT3 RS are names and trademarks of their respective owners. The artwork is original fan art and contains no manufacturer logos.

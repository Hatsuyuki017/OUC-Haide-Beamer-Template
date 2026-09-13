# OUC Smart Beamer Template

**English** | [中文](#ouc-smart-beamer-模板)

A polished XeLaTeX Beamer template for academic presentations.  
Features 24 built-in colour palettes, theorem-like environments, code listing styles, a clean title/closing page, a styled table-of-contents frame, and a circular page-progress ring next to the page number — all encapsulated in a single `.sty` file.

> **Current version:** v1.2 — see [Version History](#version-history) for changes.
>
> **Render preview** — compiled with palette 0 (OUC Default):
>
> ![OUC Smart Beamer Template Preview](OUC_Smart_Beamer_Template.png)
>
> *See `template-manual.pdf` for a full 55-page visual guide.*

---

## Table of Contents

1. [Folder Structure](#folder-structure)
2. [Prerequisites](#prerequisites)
   - [macOS](#macos)
   - [Windows](#windows)
   - [Linux](#linux)
3. [Quick Start](#quick-start)
4. [Compile](#compile)
5. [Font Notes for Windows & Linux](#font-notes-for-windows--linux)
6. [Customisation Reference](#customisation-reference)
7. [Palette Overview](#palette-overview)
   - [Complete Palette Quick Reference](#complete-palette-quick-reference)
   - [Appendix: Full Palette Descriptions](#appendix-full-palette-descriptions)
8. [Available Environments](#available-environments)
9. [Version History](#version-history)
10. [Licence](#licence)

---

## Folder Structure

```
beamertemplate/
├── oucsmartbeamer.sty        ← single style file; all template logic lives here
├── template-manual.tex       ← full user guide (compiles to 55-page PDF)
├── example.tex               ← minimal starter deck — copy & edit this
├── fonts/                    ← bundled fonts (loaded automatically)
│   ├── RobotoSerif-Regular.ttf
│   ├── RobotoSerif-Italic.ttf
│   ├── national-2-condensed-bold.ttf
│   ├── DFKaiSho-SB.ttf       ← Chinese Kai (楷体) for \textkai{...}
│   └── NISC18030.ttf
└── badge/                    ← bundled logo images
    ├── ouc.png
    └── AUlightbadge.png
```

> **You only need to edit `example.tex` (or your own `.tex` file) to create a new deck.  
> Never edit `oucsmartbeamer.sty` unless you need to change fonts for your OS.**

---

## Prerequisites

### macOS

| Requirement | How to get it |
|---|---|
| **MacTeX** (includes XeLaTeX + all packages) | [tug.org/mactex](https://tug.org/mactex/) — install the full ~5 GB distribution |
| **Latexmk** | Bundled with MacTeX |
| System fonts **Songti SC** and **Menlo** | Pre-installed on every Mac — no action needed |

MacTeX installs all required LaTeX packages automatically. After installing MacTeX, you can clone this repo and compile immediately — no further setup is needed on macOS.

```bash
# Install MacTeX via Homebrew (alternative)
brew install --cask mactex
```

---

### Windows

#### Step 1 — Install a TeX distribution

Choose **one**:

| Distribution | Download | Notes |
|---|---|---|
| **TeX Live** (recommended) | [tug.org/texlive](https://tug.org/texlive/) | Full install (~7 GB); includes every package |
| **MiKTeX** | [miktex.org](https://miktex.org/) | Lighter; downloads missing packages on-demand |

> **Important:** During TeX Live installation, choose *Full Scheme* (complete installation).  
> With MiKTeX, enable "Install missing packages on-the-fly" so any needed packages are fetched automatically.

#### Step 2 — Install a Chinese font

The template uses **Songti SC** (宋体), which is a macOS-exclusive font.  
On Windows, you must use a substitute CJK font.

**Option A — Use the freely available Noto Serif CJK (recommended):**

1. Download *Noto Serif CJK SC* from [Google Fonts / Noto](https://www.google.com/get/noto/) or [GitHub releases](https://github.com/notofonts/noto-cjk/releases).
2. Install the `.ttf` or `.otf` file by double-clicking it.

**Option B — Use Windows built-in SimSun (宋体) — already on every Windows PC, no download needed.**

#### Step 3 — Edit `oucsmartbeamer.sty` for Windows fonts

Open `oucsmartbeamer.sty` and change **lines 25–28**:

```latex
% ──────── BEFORE (macOS defaults) ────────
\setmonofont{Menlo}
\setCJKmainfont{Songti SC}
\setCJKsansfont{Songti SC}
\setCJKmonofont{Songti SC}

% ──────── AFTER — Option A: Noto Serif CJK ────────
\setmonofont{Consolas}
\setCJKmainfont{Noto Serif CJK SC}
\setCJKsansfont{Noto Serif CJK SC}
\setCJKmonofont{Noto Serif CJK SC}

% ──────── AFTER — Option B: SimSun ────────
\setmonofont{Consolas}
\setCJKmainfont{SimSun}
\setCJKsansfont{SimSun}
\setCJKmonofont{SimSun}
```

> `Consolas` is pre-installed on all Windows systems.  
> Only the four lines above need to change — everything else in `.sty` is platform-independent.

---

### Linux

1. Install **TeX Live** via your package manager:
   ```bash
   # Debian / Ubuntu
   sudo apt install texlive-full latexmk
   # Arch
   sudo pacman -S texlive-most texlive-lang latexmk
   # Fedora
   sudo dnf install texlive-scheme-full latexmk
   ```
2. Install a Chinese font, e.g.:
   ```bash
   # Debian / Ubuntu — installs Noto CJK
   sudo apt install fonts-noto-cjk
   ```
3. Edit `oucsmartbeamer.sty` lines 25–28 the same way as Windows (use `Noto Serif CJK SC` and `DejaVu Sans Mono` or `Liberation Mono`):
   ```latex
   \setmonofont{Liberation Mono}
   \setCJKmainfont{Noto Serif CJK SC}
   \setCJKsansfont{Noto Serif CJK SC}
   \setCJKmonofont{Noto Serif CJK SC}
   ```

---

## Quick Start

1. **Copy** `example.tex` to a new file, e.g. `my-presentation.tex`.
2. **Fill in** your title, author, institute, and date.
3. **Choose a palette** (optional, default is palette 0):
   ```latex
   \OUCSetPalette{7}   % 0–23, see Palette Overview section
   ```
4. **Add frames** with `\begin{frame}...\end{frame}`.
5. **Compile** (see next section).

Minimal deck:

```latex
\documentclass[aspectratio=169,10pt]{beamer}
\usepackage{oucsmartbeamer}

\title{My Presentation}
\subtitle{A Subtitle}
\author{Your Name}
\institute{Your Institution}
\date{2026}

\OUCBeamerSetup{
    marker=MY TALK,
    footer title=My Presentation,
    footer subtitle=Your Name,
    closing title=Thank You,
    closing note=Questions?
}

\begin{document}
\OUCTitleFrame

%% Optional: styled table of contents (sections appear as numbered pills)
\OUCTocFrame[Contents]

\section{Introduction}
\begin{frame}
    \frametitle{Introduction}
    Your content here.
\end{frame}

\OUCClosingFrame
\end{document}
```

---

## Compile

Always use **XeLaTeX** (required for the bundled TTF fonts and CJK support):

```bash
# Recommended — automatic multi-pass compilation
latexmk -xelatex my-presentation.tex

# Or manually (run twice to resolve cross-references)
xelatex my-presentation.tex
xelatex my-presentation.tex
```

> **Do not use `pdflatex` or `lualatex`** — the template will fall back to a plain font stack and lose all custom typography.

Compile the built-in guide:

```bash
latexmk -xelatex template-manual.tex   # → template-manual.pdf (40 pages)
latexmk -xelatex example.tex           # → example.pdf (4 pages)
```

---

## Font Notes for Windows & Linux

The template loads fonts in two ways:

| Font | How loaded | Action needed on Windows/Linux |
|---|---|---|
| `RobotoSerif` (main English serif) | From `fonts/` directory — **bundled** | None ✓ |
| `national-2-condensed-bold` (display titles) | From `fonts/` directory — **bundled** | None ✓ |
| `DFKaiSho-SB` (楷体 for `\textkai{}`) | From `fonts/` directory — **bundled** | None ✓ |
| `Menlo` (monospace) | macOS system font | Replace with `Consolas` (Win) / `Liberation Mono` (Linux) |
| `Songti SC` (宋体 CJK) | macOS system font | Replace with `Noto Serif CJK SC` or `SimSun` |

Only the **last two rows** need changing. The edit is 4 lines in `oucsmartbeamer.sty`.

---

## Customisation Reference

All configuration goes **in the preamble** of your `.tex` file:

```latex
% ── Metadata (drives cover and footer) ──────────────────────────────
\title{Your Title}
\subtitle{Your Subtitle}
\author{Author A \and Author B}
\institute{Your Institute}
\date{Your Date or Topic}

% ── Template settings ───────────────────────────────────────────────
\OUCBeamerSetup{
    marker          = MY TALK,            % text in top-right corner of cover
    left logo       = badge/ouc.png,      % path to left badge image
    right logo      = badge/ouc.png,      % path to right badge image
    footer title    = My Presentation,    % bold text in footer
    footer subtitle = Section Name,       % small text in footer
    closing title   = Thank You!,         % closing slide heading
    closing subtitle= My Presentation,    % closing slide sub-heading
    closing note    = Questions welcome   % small closing note
}

% ── Font sizes ─────────────────────────────────────────────────────
\OUCSetTitleFontSize{30}{34}    % cover title: {font-pt}{line-skip-pt}
\OUCSetBodyFontSize{\normalsize}% body text size switch
\OUCSetHeaderFontSize{\large}   % frametitle size switch
\OUCSetFooterFontSize{\small}   % footer text size switch

% ── Colour palette (0–23) ───────────────────────────────────────────
\OUCSetPalette{7}

% ── Code listing line-count warning threshold (default 20) ──────────
\OUCSetLstMaxLines{25}
```

---

## Palette Overview

There are 24 palettes (indices `0..23`), imported wholesale from the
[Thomas-Tufte-Style-Book-Template](https://github.com/Hatsuyuki017/Thomas-Tufte-Style-Book-Template)
so that a deck and its companion book can be set in exactly the same colours.
Each palette exposes six swatches ordered light → dark. The full six-swatch
reference and the long-form palette appendix are reproduced below in both
languages, so readers no longer need to switch languages just to inspect the
full palette catalogue.

Select one anywhere in the preamble:

```latex
\OUCSetPalette{7}   % N in 0..23
```

The style file exposes:

- `oucpal1` … `oucpal6` — palette swatches, light to dark
- `primary` — `pal5`; frametitle, footer accent, theorem and block titles
- `secondary` — `pal4`; example / remark / intro title backgrounds
- `accent` — `pal3`; itemize subitems, decorative strips
- `softblue` — `pal2`; example / remark / intro body backgrounds
- `paleblue` — `pal1`; `lstlisting` background
- `oucpal6` — deepest swatch; `lstlisting` border and accent, free for ad-hoc use
- `spotcolor` — theme spot colour; defaults to `accent`, and becomes Kyoto's vermilion `rgb(170,50,36)` under palette 22

`\OUCPaletteName` expands to the active palette's name, which is handy on a
colophon slide.

| N | Name | Primary (pal5) | Deepest (pal6) | Character |
|---|---|---|---|---|
| 0 | OUC Default | `rgb(30,58,138)` | `rgb(30,41,59)` | Classic academic blue |
| 1 | Brunneophobia | `rgb(86,67,53)` | `rgb(42,23,14)` | Warm earth, fired brown, weighty |
| 2 | Van Dyke | `rgb(68,60,94)` | `rgb(61,43,39)` | Grey-violet, restrained, old canvas |
| 3 | Back in Black | `rgb(74,63,75)` | `rgb(22,19,21)` | Near-monochrome, smoky pink, charcoal |
| 4 | Belle of the Ball | `rgb(118,118,44)` | `rgb(53,77,4)` | Olive, coral, vintage ballroom |
| 5 | Pine Tree | `rgb(167,88,26)` | `rgb(43,47,34)` | Autumn gold, pine shadow, ochre |
| 6 | Provence Blue | `rgb(82,92,121)` | `rgb(53,66,94)` | Provence mist blue |
| 7 | Fresco Blue | `rgb(4,75,102)` | `rgb(2,31,46)` | Fresco blue, cool sea-green |
| 8 | Monet | `rgb(16,86,102)` | `rgb(10,51,35)` | Impressionist pastel and deep teal |
| 9 | Narcissus | `rgb(190,108,26)` | `rgb(110,60,31)` | Sand, warm gold, rust orange |
| 10 | Roman Empire | `rgb(120,20,40)` | `rgb(88,28,90)` | Rome, legion red, murex purple |
| 11 | Greece | `rgb(48,105,175)` | `rgb(90,42,92)` | Greece, democratic blue, pottery red |
| 12 | Kanagawa | `rgb(13,38,76)` | `rgb(29,25,35)` | Edo, wave blue, ink line |
| 13 | Starry Night | `rgb(22,50,30)` | `rgb(20,36,88)` | Night sky, moon yellow, cypress shadow |
| 14 | A Thousand Li | `rgb(48,105,76)` | `rgb(35,78,112)` | Blue-and-green landscape, aged silk |
| 15 | And Quiet Flows the Don | `rgb(52,70,90)` | `rgb(88,26,24)` | The Don, turbid blue, dark blood |
| 16 | Cyberpunk Edgerunners | `rgb(15,32,98)` | `rgb(14,8,28)` | Night City, neon, cyber overload |
| 17 | The Grand Budapest Hotel | `rgb(128,88,148)` | `rgb(143,52,65)` | Faded aristocracy, pink-violet, cream |
| 18 | Renaissance Florence | `rgb(46,70,118)` | `rgb(85,54,34)` | Renaissance, lapis, terracotta |
| 19 | Soviet Avant-Garde | `rgb(196,28,28)` | `rgb(24,20,18)` | Constructivism, red and black, industrial |
| 20 | Constantinople | `rgb(102,32,65)` | `rgb(30,52,88)` | Byzantium, gilt, imperial sea |
| 21 | France | `rgb(180,32,40)` | `rgb(44,74,138)` | France, tricolour reinterpreted |
| 22 | Kyoto | `rgb(80,94,68)` | `rgb(34,40,66)` | Kyoto, zen stillness, yūgen |
| 23 | Siamese Dream | `rgb(188,105,40)` | `rgb(42,68,48)` | Distorted rock, adolescence, conjoined dream |


---

## Complete Palette Quick Reference

The complete six-swatch strips for all 24 palettes are listed below. Each
palette runs from `pal1` to `pal6`, light → dark. Kyoto additionally exposes
`spotcolor = rgb(170,50,36)`.

### 0. OUC Default

```text
OUC Default A   rgb(239, 246, 255)
OUC Default B   rgb(219, 234, 254)
OUC Default C   rgb( 96, 165, 250)
OUC Default D   rgb( 37,  99, 235)
OUC Default E   rgb( 30,  58, 138)
OUC Default F   rgb( 30,  41,  59)
```

### 1. Brunneophobia

```text
Brunneophobia A rgb(238, 211, 180)
Brunneophobia B rgb(213, 148,  79)
Brunneophobia C rgb(213, 148,  79)
Brunneophobia D rgb(180,  69,  15)
Brunneophobia E rgb( 86,  67,  53)
Brunneophobia F rgb( 42,  23,  14)
```

### 2. Van Dyke

```text
Van Dyke A       rgb(236, 194, 188)
Van Dyke B       rgb(169, 159, 191)
Van Dyke C       rgb(169, 159, 191)
Van Dyke D       rgb(191, 113, 133)
Van Dyke E       rgb( 68,  60,  94)
Van Dyke F       rgb( 61,  43,  39)
```

### 3. Back in Black

```text
Back in Black A  rgb(240, 217, 228)
Back in Black B  rgb(193, 160, 172)
Back in Black C  rgb(193, 160, 172)
Back in Black D  rgb(128, 108, 121)
Back in Black E  rgb( 74,  63,  75)
Back in Black F  rgb( 22,  19,  21)
```

### 4. Belle of the Ball

```text
Belle A          rgb(226, 203, 192)
Belle B          rgb(206, 171, 150)
Belle C          rgb(210, 135, 106)
Belle D          rgb(229,  74,  57)
Belle E          rgb(118, 118,  44)
Belle F          rgb( 53,  77,   4)
```

### 5. Pine Tree

```text
Pine Tree A      rgb(238, 200, 111)
Pine Tree B      rgb(222, 166,  32)
Pine Tree C      rgb(222, 166,  32)
Pine Tree D      rgb(177, 120, 133)
Pine Tree E      rgb(167,  88,  26)
Pine Tree F      rgb( 43,  47,  34)
```

### 6. Provence Blue

```text
Provence A       rgb(170, 188, 175)
Provence B       rgb(137, 156, 154)
Provence C       rgb(137, 156, 154)
Provence D       rgb(110, 124, 139)
Provence E       rgb( 82,  92, 121)
Provence F       rgb( 53,  66,  94)
```

### 7. Fresco Blue

```text
Fresco A         rgb(166, 224, 244)
Fresco B         rgb( 71, 169, 207)
Fresco C         rgb( 71, 169, 207)
Fresco D         rgb(  9, 121, 158)
Fresco E         rgb(  4,  75, 102)
Fresco F         rgb(  2,  31,  46)
```

### 8. Monet

```text
Monet A          rgb(247, 244, 213)
Monet B          rgb(211, 150, 140)
Monet C          rgb(211, 150, 140)
Monet D          rgb(131, 153,  88)
Monet E          rgb( 16,  86, 102)
Monet F          rgb( 10,  51,  35)
```

### 9. Narcissus

```text
Narcissus A      rgb(221, 213, 200)
Narcissus B      rgb(185, 149, 144)
Narcissus C      rgb(185, 149, 144)
Narcissus D      rgb(199, 149,  72)
Narcissus E      rgb(190, 108,  26)
Narcissus F      rgb(110,  60,  31)
```

### 10. Roman Empire

```text
Carrara Marble   rgb(236, 232, 225)
Gloria Aurum     rgb(212, 175,  55)
Laurel Viridis   rgb( 74, 110,  65)
Legion Crimson   rgb(180,  30,  30)
Senate Bordeaux  rgb(120,  20,  40)
Tyrian Purple    rgb( 88,  28,  90)
```

### 11. Greece

```text
Parian Marble      rgb(245, 240, 228)
Gloria Aurum       rgb(212, 175,  55)
Athena's Olive     rgb( 98, 128,  48)
Attic Terracotta   rgb(188,  82,  38)
Agora Kyanos       rgb( 48, 105, 175)
Dionysian Grape    rgb( 90,  42,  92)
```

### 12. Kanagawa

```text
Nami-shiro       rgb(237, 233, 222)
Boten            rgb(208, 224, 238)
Fuji-gasumi      rgb(150, 186, 210)
Bero-ai          rgb( 26,  78, 132)
Shinkai          rgb( 13,  38,  76)
Sumi             rgb( 29,  25,  35)
```

### 13. Starry Night

```text
Lumière Lunaire     rgb(240, 208,  68)
Lueurs du Village   rgb(198, 140,  52)
Aube Glacée         rgb(105, 155, 200)
Tourbillon Outremer rgb( 48,  96, 165)
Cyprès Nocturne     rgb( 22,  50,  30)
Minuit Cobalt       rgb( 20,  36,  88)
```

### 14. A Thousand Li

```text
Song Silk        rgb(218, 203, 170)
Sky Azurite      rgb(110, 165, 195)
Ochre-Gold       rgb(183, 118,  45)
Pale Malachite   rgb( 96, 148, 110)
Malachite True   rgb( 48, 105,  76)
Azurite Deep     rgb( 35,  78, 112)
```

### 15. And Quiet Flows the Don

```text
Полынь            rgb(142, 120,  70)
Степной Пепел     rgb(110, 108, 104)
Донская Земля     rgb(118,  86,  52)
Ржавое Железо     rgb(122,  66,  36)
Мутный Дон        rgb( 52,  70,  90)
Запёкшаяся Кровь  rgb( 88,  26,  24)
```

### 16. Cyberpunk Edgerunners

```text
Psycho Yellow    rgb(225, 255,   8)
Flatline Green   rgb( 10, 238, 100)
Neon Magenta     rgb(238,  18, 120)
Edgerunner Red   rgb(205,  20,  35)
Luna Blue        rgb( 15,  32,  98)
Night City Void  rgb( 14,   8,  28)
```

### 17. The Grand Budapest Hotel

```text
Crème Vanille      rgb(247, 235, 215)
Brume Alpine       rgb(168, 178, 196)
Rose Méndl         rgb(237, 148, 158)
Doré Antique       rgb(176, 136,  60)
Violet Concierge   rgb(128,  88, 148)
Bordeaux Vintage   rgb(143,  52,  65)
```

### 18. Renaissance Florence

```text
Avorio Fiorentino            rgb(238, 228, 208)
Oro dell'Altare              rgb(190, 148,  52)
Cotto Brunellesco            rgb(172,  84,  50)
Verde Cipresso               rgb( 54,  80,  60)
Oltremare di Lapislazzuli    rgb( 46,  70, 118)
Noce Toscano                 rgb( 85,  54,  34)
```

### 19. Soviet Avant-Garde

```text
ГАЗЕТА   rgb(225, 218, 205)
ПЛАКАТ   rgb(200, 150,  32)
БЕТОН    rgb(118, 114, 108)
ЧЕРТЁЖ   rgb( 50,  80, 138)
КРАСНЫЙ  rgb(196,  28,  28)
ЧЁРНЫЙ   rgb( 24,  20,  18)
```

### 20. Constantinople

```text
Λευκός · Fildişi   rgb(236, 225, 207)
Χρυσός · Altın     rgb(195, 150,  42)
Ώχρα · Toprak      rgb(170, 112,  50)
Κυπαρίσσι · Selvi  rgb( 50,  76,  58)
Πορφύρα · Mor      rgb(102,  32,  65)
Βόσπορος · Boğaz   rgb( 30,  52,  88)
```

### 21. France

```text
Ivoire Champagne    rgb(232, 222, 205)
Olive Dorée         rgb(142, 133,  58)
Zinc Parisien       rgb(122, 126, 132)
Lavande Provençale  rgb(143, 108, 148)
Rouge Marianne      rgb(180,  32,  40)
Bleu République     rgb( 44,  74, 138)
```

### 22. Kyoto

```text
Kinushiro      rgb(234, 226, 212)
Sakura-nezumi  rgb(204, 184, 178)
Aotake-nezumi  rgb(116, 126, 120)
Karacha        rgb(110,  84,  64)
Koke-iro       rgb( 80,  94,  68)
Kon            rgb( 34,  40,  66)
Shu-hi         rgb(170,  50,  36)   % spotcolor
```

### 23. Siamese Dream

```text
Luna           rgb(238, 226, 208)
Disarm         rgb(182, 180, 193)
Today          rgb(198, 158,  65)
Hummer         rgb(150, 145, 135)
Mayonaise      rgb(188, 105,  40)
Soma           rgb( 42,  68,  48)
```

---

## Appendix: Full Palette Descriptions

The appendix below is the full English counterpart to the long-form Chinese
catalogue. Each palette is presented with the same four-part structure: a short
color philosophy, a six-color set, the full swatch strip, and a brief design
logic note explaining how the palette is meant to behave on the page.

### Palette 0 — OUC Default

#### Color Philosophy

This is a deep academic blue system organized around scholarship, the sea, and
structural order. It is not a display palette built for bravura; it is a
palette built to hold information in place. Pale blue opens breathing room,
bright blue handles guidance, navy carries authority, and the near-black harbor
blue closes the system.

#### Six-Color Set

| Color | RGB | Note |
|---|---|---|
| Mist Blue | `rgb(239,246,255)` | Almost-white blue for backgrounds and breathing room |
| Soft Sky | `rgb(219,234,254)` | Secondary pale layer for light information blocks |
| Signal Blue | `rgb(96,165,250)` | Guidance blue for prompts and light emphasis |
| Structural Blue | `rgb(37,99,235)` | Mid-tone structural blue, crisp and modern |
| Academic Navy | `rgb(30,58,138)` | Primary color, stable, rational, and academic |
| Deep Harbor | `rgb(30,41,59)` | Deep anchor for the strongest contrast |

#### Full Palette

```text
Mist Blue        rgb(239, 246, 255)
Soft Sky         rgb(219, 234, 254)
Signal Blue      rgb( 96, 165, 250)
Structural Blue  rgb( 37,  99, 235)
Academic Navy    rgb( 30,  58, 138)
Deep Harbor      rgb( 30,  41,  59)
```

Design logic: the chain runs from nearly invisible pale blue to harbor-deep
navy, giving the page a very explicit hierarchy. It is the most natural fit
for academic prose, contents pages, chapter titles, and table heads.

### Palette 1 — Brunneophobia

#### Color Philosophy

Brunneophobia is built from fired earth, old wood, leather, and the residual
heat of a kiln. These are not cheerful browns but smoked browns, the colors of
ceramic skins, worn tabletops, and cracked spines. It suits books that want
weight without claustrophobia.

#### Six-Color Set

| Color | RGB | Note |
|---|---|---|
| Clay Mist | `rgb(238,211,180)` | Pale clay foundation |
| Ochre Sand | `rgb(213,148,79)` | Warm ochre-brown middle layer |
| Ochre Sand | `rgb(213,148,79)` | Repeated slot for the five-color legacy mapping |
| Kiln Orange | `rgb(180,69,15)` | Fired ochre-orange |
| Walnut Brown | `rgb(86,67,53)` | Primary color, steady walnut brown |
| Charred Earth | `rgb(42,23,14)` | Deep charred-soil anchor |

#### Full Palette

```text
Clay Mist     rgb(238, 211, 180)
Ochre Sand    rgb(213, 148,  79)
Ochre Sand    rgb(213, 148,  79)
Kiln Orange   rgb(180,  69,  15)
Walnut Brown  rgb( 86,  67,  53)
Charred Earth rgb( 42,  23,  14)
```

Design logic: pale clay and charred earth stretch the two extremes apart,
while burnt ochre compresses the middle. The result is warm, steady, and
restrained, especially suitable for literature, history, and old-object
subjects.

### Palette 2 — Van Dyke

#### Color Philosophy

Van Dyke moves between old canvas, dusty rose, and faded indigo. It avoids
display contrast and instead leans on a powdery, low-voiced elegance. It works
well when the page needs soft drama rather than overt force.

#### Six-Color Set

| Color | RGB | Note |
|---|---|---|
| Dust Rose | `rgb(236,194,188)` | Pale grey-rose ground |
| Faded Indigo | `rgb(169,159,191)` | Misty indigo-violet |
| Faded Indigo | `rgb(169,159,191)` | Repeated slot |
| Old Wine | `rgb(191,113,133)` | Faded wine-red middle tone |
| Muted Indigo | `rgb(68,60,94)` | Primary color, low-saturation indigo |
| Burnt Umber | `rgb(61,43,39)` | Dark brown-grey anchor |

#### Full Palette

```text
Dust Rose      rgb(236, 194, 188)
Faded Indigo   rgb(169, 159, 191)
Faded Indigo   rgb(169, 159, 191)
Old Wine       rgb(191, 113, 133)
Muted Indigo   rgb( 68,  60,  94)
Burnt Umber    rgb( 61,  43,  39)
```

Design logic: rose, violet, wine, and brown-grey form an old-oil-painting
continuum. The emotional register is quiet and literary, more grounded than a
typical purple-based palette.

### Palette 3 — Back in Black

#### Color Philosophy

This is not black and white, but a near-monochrome system with the residual
warmth of dusty mauve. It feels like backstage velvet, mirrored dressing-room
light, and the last warmth left inside dark fabric. The palette stays tightly
controlled without becoming inhuman.

#### Six-Color Set

| Color | RGB | Note |
|---|---|---|
| Powder Haze | `rgb(240,217,228)` | Pale smoky pink |
| Mauve Dust | `rgb(193,160,172)` | Dusty mauve middle layer |
| Mauve Dust | `rgb(193,160,172)` | Repeated slot |
| Velvet Gray | `rgb(128,108,121)` | Mauve-grey transition |
| Charcoal Mauve | `rgb(74,63,75)` | Primary color, smoky charcoal violet |
| Stage Black | `rgb(22,19,21)` | Deepest near-black |

#### Full Palette

```text
Powder Haze    rgb(240, 217, 228)
Mauve Dust     rgb(193, 160, 172)
Mauve Dust     rgb(193, 160, 172)
Velvet Gray    rgb(128, 108, 121)
Charcoal Mauve rgb( 74,  63,  75)
Stage Black    rgb( 22,  19,  21)
```

Design logic: the near-monochrome logic keeps the page from competing with
the layout, while the dusty pink base stops it from feeling sterile. It works
for quiet, refined, exhibition-like pages.

### Palette 4 — Belle of the Ball

#### Color Philosophy

Belle of the Ball feels like a vintage ballroom where porcelain blush, coral
light, and late olive-green meet under chandeliers. The palette carries a hint
of theatrics, but its center of gravity stays in olive, which keeps the whole
thing controlled rather than sugary.

#### Six-Color Set

| Color | RGB | Note |
|---|---|---|
| Porcelain Blush | `rgb(226,203,192)` | Soft pink-beige ground |
| Antique Peach | `rgb(206,171,150)` | Old peach middle tone |
| Coral Clay | `rgb(210,135,106)` | Coral-clay bridge tone |
| Ballroom Coral | `rgb(229,74,57)` | Bright coral accent |
| Olive Court | `rgb(118,118,44)` | Primary color, courtly olive |
| Moss Shadow | `rgb(53,77,4)` | Deep mossy anchor |

#### Full Palette

```text
Porcelain Blush rgb(226, 203, 192)
Antique Peach   rgb(206, 171, 150)
Coral Clay      rgb(210, 135, 106)
Ballroom Coral  rgb(229,  74,  57)
Olive Court     rgb(118, 118,  44)
Moss Shadow     rgb( 53,  77,   4)
```

Design logic: warm pale tones establish old-world light, coral delivers the
momentary sparkle, and olive plus moss push the palette back into a controlled
retro register.

### Palette 5 — Pine Tree

#### Color Philosophy

Pine Tree is a distinctly autumnal palette. Gold, ochre-orange, pine shadow,
and a muted berry transition turn the page into late woodland space: warm hues
carry the remaining light; deep hues keep the hush of dried leaves and dark
tree lines.

#### Six-Color Set

| Color | RGB | Note |
|---|---|---|
| Autumn Gold | `rgb(238,200,111)` | Autumn gold foundation |
| Harvest Ochre | `rgb(222,166,32)` | Harvest ochre |
| Harvest Ochre | `rgb(222,166,32)` | Repeated slot |
| Faded Berry | `rgb(177,120,133)` | Muted berry transition |
| Burnt Orange | `rgb(167,88,26)` | Primary color, deep burnt orange |
| Pine Shadow | `rgb(43,47,34)` | Dark pine-shadow anchor |

#### Full Palette

```text
Autumn Gold   rgb(238, 200, 111)
Harvest Ochre rgb(222, 166,  32)
Harvest Ochre rgb(222, 166,  32)
Faded Berry   rgb(177, 120, 133)
Burnt Orange  rgb(167,  88,  26)
Pine Shadow   rgb( 43,  47,  34)
```

Design logic: this is a classic palette of warm advance and dark-green
closure. It works well for pages that want land, season, and a controlled
narrative mood.

### Palette 6 — Provence Blue

#### Color Philosophy

The beauty of Provence Blue lies in its refusal of postcard brightness. It is
closer to mist over stone walls, herb pots on a sill, or evening over lavender
fields than to a touristic Mediterranean blue. It is cool, muted, and easy to
live with across many pages.

#### Six-Color Set

| Color | RGB | Note |
|---|---|---|
| Herb Mist | `rgb(170,188,175)` | Herbal grey-green light layer |
| Stone Green | `rgb(137,156,154)` | Stone-wall blue-green |
| Stone Green | `rgb(137,156,154)` | Repeated slot |
| Slate Air | `rgb(110,124,139)` | Slate-blue air tone |
| Provence Slate | `rgb(82,92,121)` | Primary color, muted Provence blue |
| Evening Indigo | `rgb(53,66,94)` | Deep evening indigo |

#### Full Palette

```text
Herb Mist      rgb(170, 188, 175)
Stone Green    rgb(137, 156, 154)
Stone Green    rgb(137, 156, 154)
Slate Air      rgb(110, 124, 139)
Provence Slate rgb( 82,  92, 121)
Evening Indigo rgb( 53,  66,  94)
```

Design logic: the palette stays cool without becoming hard. Because it has
so much grey built into it, it performs well for body pages and contents pages
that need endurance rather than spectacle.

### Palette 7 — Fresco Blue

#### Color Philosophy

Fresco Blue borrows from weathered murals and sea air etched into mineral
surfaces. Its highlights look thinned with lime and plaster; its darks feel as
if pigment has seeped into the wall itself. The result is clean, historical,
and beautifully legible.

#### Six-Color Set

| Color | RGB | Note |
|---|---|---|
| Wash Blue | `rgb(166,224,244)` | Washed mural blue |
| Fresh Cyan | `rgb(71,169,207)` | Sea-cyan middle layer |
| Fresh Cyan | `rgb(71,169,207)` | Repeated slot |
| Mineral Teal | `rgb(9,121,158)` | Mineral teal |
| Fresco Teal | `rgb(4,75,102)` | Primary color, deep fresco teal |
| Abyss Ink | `rgb(2,31,46)` | Deep marine ink anchor |

#### Full Palette

```text
Wash Blue    rgb(166, 224, 244)
Fresh Cyan   rgb( 71, 169, 207)
Fresh Cyan   rgb( 71, 169, 207)
Mineral Teal rgb(  9, 121, 158)
Fresco Teal  rgb(  4,  75, 102)
Abyss Ink    rgb(  2,  31,  46)
```

Design logic: one of the strongest modern-leaning base palettes in the set.
Its depth ladder is extremely clear, and it feels crisper and more designed
than the default OUC blue.

### Palette 8 — Monet

#### Color Philosophy

Monet brings ivory, dusty coral, moss-green, and dark teal into the same
atmosphere. It feels less like flowers and more like air inside an Impressionist
painting: soft without being weak, open in the highlights, but still held up by
real structure in the deep tones.

#### Six-Color Set

| Color | RGB | Note |
|---|---|---|
| Ivory Light | `rgb(247,244,213)` | Pale ivory ground |
| Dusty Coral | `rgb(211,150,140)` | Dust-softened coral |
| Dusty Coral | `rgb(211,150,140)` | Repeated slot |
| Field Green | `rgb(131,153,88)` | Field green |
| Dark Teal | `rgb(16,86,102)` | Primary color, deep teal |
| Forest Teal | `rgb(10,51,35)` | Forest-dark teal anchor |

#### Full Palette

```text
Ivory Light  rgb(247, 244, 213)
Dusty Coral  rgb(211, 150, 140)
Dusty Coral  rgb(211, 150, 140)
Field Green  rgb(131, 153,  88)
Dark Teal    rgb( 16,  86, 102)
Forest Teal  rgb( 10,  51,  35)
```

Design logic: the ivory and coral layers give the page immediate warmth,
while dark teal and forest teal keep the hierarchy firm. It is especially good
for narrative and art-adjacent documents.

### Palette 9 — Narcissus

#### Color Philosophy

Narcissus is dry, warm, and particulate. Its pale tones feel like sand and old
cloth; the middle moves through weathered ochre; the dark end compresses into
rust and scorched cedar. It is especially convincing for historical, archival,
or landscape-centered material.

#### Six-Color Set

| Color | RGB | Note |
|---|---|---|
| Sand Veil | `rgb(221,213,200)` | Pale sand ground |
| Dust Rose | `rgb(185,149,144)` | Dusty rose |
| Dust Rose | `rgb(185,149,144)` | Repeated slot |
| Dry Ochre | `rgb(199,149,72)` | Dry ochre middle tone |
| Rust Amber | `rgb(190,108,26)` | Primary color, rusty amber |
| Burnt Cedar | `rgb(110,60,31)` | Deep scorched-wood anchor |

#### Full Palette

```text
Sand Veil   rgb(221, 213, 200)
Dust Rose   rgb(185, 149, 144)
Dust Rose   rgb(185, 149, 144)
Dry Ochre   rgb(199, 149,  72)
Rust Amber  rgb(190, 108,  26)
Burnt Cedar rgb(110,  60,  31)
```

Design logic: the palette has pronounced soil and rust in it, which makes
it warm without sweetness and old without turning inert.

### Palette 10 — Roman Empire

#### Color Philosophy

The Roman Empire palette has to hold stone, blood, power, ritual, and triumph
at the same time. Carrara marble provides the architectural ground; legion red
and senate wine-red divide military force from patrician authority; laurel
green and ceremonial gold stabilize the scene; Tyrian purple, the final deep
note, seals the whole palette with imperial distance.

#### Six-Color Set

| Name | RGB | Note |
|---|---|---|
| Carrara Marble | `rgb(236,232,225)` | Cool marble white with a hint of warmth |
| Gloria Aurum | `rgb(212,175,55)` | Triumphal gold, balanced between coin and icon |
| Laurel Viridis | `rgb(74,110,65)` | Matte laurel green, steady rather than bright |
| Legion Crimson | `rgb(180,30,30)` | Martial crimson, direct and saturated |
| Senate Bordeaux | `rgb(120,20,40)` | Deep wine-red with patrician gravity |
| Tyrian Purple | `rgb(88,28,90)` | The costly imperial purple of sovereignty |

#### Full Palette

```text
Carrara Marble   rgb(236, 232, 225)
Legion Crimson   rgb(180,  30,  30)
Senate Bordeaux  rgb(120,  20,  40)
Laurel Viridis   rgb( 74, 110,  65)
Gloria Aurum     rgb(212, 175,  55)
Tyrian Purple    rgb( 88,  28,  90)
```

Design logic: stone gives the civilization its base plane, the two reds split
state power into two registers, green and gold establish triumphal order, and
purple functions as the final sacred-dark anchor.

### Palette 11 — Greece

#### Color Philosophy

The Greece palette begins with temple marble and lets civic blue lead the eye.
Gold serves as a highlight, while terracotta, olive, and grape-purple restore
the human, agricultural, and theatrical complexity of Greek civilization. This
keeps it from collapsing into a mere tourist-blue-and-white cliché.

#### Six-Color Set

| Name | RGB | Note |
|---|---|---|
| Parian Marble | `rgb(245,240,228)` | Warm ivory marble for temples and sculpture |
| Gloria Aurum | `rgb(212,175,55)` | Shared ceremonial gold |
| Athena's Olive | `rgb(98,128,48)` | Olive-green of Athena's tree |
| Attic Terracotta | `rgb(188,82,38)` | Red-clay ceramic narrative tone |
| Agora Kyanos | `rgb(48,105,175)` | Aegean-civic blue |
| Dionysian Grape | `rgb(90,42,92)` | Deep dramatic purple |

#### Full Palette

```text
Parian Marble      rgb(245, 240, 228)
Agora Kyanos       rgb( 48, 105, 175)
Gloria Aurum       rgb(212, 175,  55)
Attic Terracotta   rgb(188,  82,  38)
Dionysian Grape    rgb( 90,  42,  92)
Athena's Olive     rgb( 98, 128,  48)
```

Design logic: marble holds the base, civic blue leads the composition, gold
acts as a controlled flare, terracotta and olive mediate warm and cool, and the
grape-purple sits at the deepest dramatic point.

### Palette 12 — Kanagawa

#### Color Philosophy

Kanagawa takes its logic from Hokusai's revolution in blue. Prussian blue is
the spine; washi warmth and foam-white are the air around it; sumi ink closes
the composition. It is a palette of blue structure, white breath, and dark
outline.

#### Six-Color Set

| Name | RGB | Note |
|---|---|---|
| Nami-shiro | `rgb(237,233,222)` | Foam-white, warm like paper rather than pure white |
| Boten | `rgb(208,224,238)` | Pale horizon sky |
| Fuji-gasumi | `rgb(150,186,210)` | Distant Fuji haze |
| Bero-ai | `rgb(26,78,132)` | Main Prussian-wave blue |
| Shinkai | `rgb(13,38,76)` | Deep-sea blue, nearly black |
| Sumi | `rgb(29,25,35)` | Printmaking ink-line anchor |

#### Full Palette

```text
Bero-ai      rgb( 26,  78, 132)
Shinkai      rgb( 13,  38,  76)
Fuji-gasumi  rgb(150, 186, 210)
Boten        rgb(208, 224, 238)
Nami-shiro   rgb(237, 233, 222)
Sumi         rgb( 29,  25,  35)
```

Design logic: the palette forms a continuous rise from ink-dark sea depth to
foam-white spray. That single-hue modulation is exactly what gives it its Edo
woodblock authority.

### Palette 13 — Starry Night

#### Color Philosophy

Starry Night is organized by three tiers of blue and the violent intrusion of
yellow light. The cypress is the dark vegetal flame that pulls the cosmic swirl
back toward the earth, while the village amber is the only remnant of human
warmth in the scene.

#### Six-Color Set

| Name | RGB | Note |
|---|---|---|
| Lumière Lunaire | `rgb(240,208,68)` | Moon and starburst yellow |
| Lueurs du Village | `rgb(198,140,52)` | Village-window amber |
| Aube Glacée | `rgb(105,155,200)` | Pale blue transition |
| Tourbillon Outremer | `rgb(48,96,165)` | Ultramarine vortex blue |
| Cyprès Nocturne | `rgb(22,50,30)` | Cypress-dark green |
| Minuit Cobalt | `rgb(20,36,88)` | Deep midnight cobalt |

#### Full Palette

```text
Minuit Cobalt       rgb( 20,  36,  88)
Tourbillon Outremer rgb( 48,  96, 165)
Aube Glacée         rgb(105, 155, 200)
Lumière Lunaire     rgb(240, 208,  68)
Cyprès Nocturne     rgb( 22,  50,  30)
Lueurs du Village   rgb(198, 140,  52)
```

Design logic: the three blues establish emotional depth, moon-yellow and
village amber serve as the only two warm notes, and the cypress keeps the whole
sky from floating away into pure spectacle.

### Palette 14 — A Thousand Li

#### Color Philosophy

This palette draws from the mineral layering of traditional blue-green Chinese
landscape painting. Azurite and malachite are not blunt blocks here; they are
sedimented into silk. Ochre-gold acts as a temperature regulator, while the old
silk ground gives the entire system historical thickness.

#### Six-Color Set

| Name | RGB | Note |
|---|---|---|
| Song Silk | `rgb(218,203,170)` | Warm aged-silk foundation |
| Sky Azurite | `rgb(110,165,195)` | Pale azurite for water and distance |
| Ochre-Gold | `rgb(183,118,45)` | Warm human and architectural note |
| Pale Malachite | `rgb(96,148,110)` | Transitional green mist |
| Malachite True | `rgb(48,105,76)` | Full malachite mountain green |
| Azurite Deep | `rgb(35,78,112)` | Deep azurite structural blue |

#### Full Palette

```text
Azurite Deep    rgb( 35,  78, 112)
Malachite True  rgb( 48, 105,  76)
Sky Azurite     rgb(110, 165, 195)
Pale Malachite  rgb( 96, 148, 110)
Ochre-Gold      rgb(183, 118,  45)
Song Silk       rgb(218, 203, 170)
```

Design logic: deep azurite and malachite provide the primary blue-green axis,
lighter azurite and malachite create graded atmospheric depth, ochre-gold adds
temperature, and aged silk keeps the whole palette grounded in time.

### Palette 15 — And Quiet Flows the Don

#### Color Philosophy

This palette rejects brightness altogether. Its blue is muddy, its red is dried
blood, its yellow is dead reed, and its grey is not abstract neutrality but
frozen dust and exhausted steppe air. It is designed to hold historical weight
without melodrama.

#### Six-Color Set

| Name | RGB | Note |
|---|---|---|
| Полынь | `rgb(142,120,70)` | Wormwood-yellow reed tone |
| Степной Пепел | `rgb(110,108,104)` | Lead-grey of winter steppe |
| Донская Земля | `rgb(118,86,52)` | Don-soil brown |
| Ржавое Железо | `rgb(122,66,36)` | Rusted-iron ochre-red |
| Мутный Дон | `rgb(52,70,90)` | Muddy river blue |
| Запёкшаяся Кровь | `rgb(88,26,24)` | Dried-blood dark red |

#### Full Palette

```text
Мутный Дон        rgb( 52,  70,  90)
Степной Пепел     rgb(110, 108, 104)
Донская Земля     rgb(118,  86,  52)
Полынь            rgb(142, 120,  70)
Ржавое Железо     rgb(122,  66,  36)
Запёкшаяся Кровь  rgb( 88,  26,  24)
```

Design logic: cold grey presses from above, earth-brown bears the weight,
dark blood anchors the bottom, and rust ties time into the whole system. There
is no hope color here, only gradations of attrition.

### Palette 16 — Cyberpunk Edgerunners

#### Color Philosophy

Cyberpunk Edgerunners is built on overload. There is no middle cushioning layer
between the void-dark base and the fluorescent highs. Lucy's blue is the only
credible line of escape; yellow and green signal machinery, illness, and loss
of control; red is the price paid by the body.

#### Six-Color Set

| Name | RGB | Note |
|---|---|---|
| Psycho Yellow | `rgb(225,255,8)` | Critical-overload yellow |
| Flatline Green | `rgb(10,238,100)` | Hacking and machinery green |
| Neon Magenta | `rgb(238,18,120)` | Signboard and pleasure-district magenta |
| Edgerunner Red | `rgb(205,20,35)` | Blood-cost red |
| Luna Blue | `rgb(15,32,98)` | Lucy, moon, and escape blue |
| Night City Void | `rgb(14,8,28)` | The deep violet-black substrate |

#### Full Palette

```text
Night City Void   rgb( 14,   8,  28)
Luna Blue         rgb( 15,  32,  98)
Edgerunner Red    rgb(205,  20,  35)
Neon Magenta      rgb(238,  18, 120)
Flatline Green    rgb( 10, 238, 100)
Psycho Yellow     rgb(225, 255,   8)
```

Design logic: void-dark sets the container, blue supplies the dream line,
red marks the bodily toll, and the fluorescent top end supplies the overclocked
surface noise that makes Night City feel terminally awake.

### Palette 17 — The Grand Budapest Hotel

#### Color Philosophy

This palette is wrapped in old-European fairy-tale light. Its pink is not
girlish pink but aged rose; its purple is etiquette, personality, and rank.
Vanilla cream, dim gold, and mist-blue keep the whole system bright without
turning saccharine.

#### Six-Color Set

| Name | RGB | Note |
|---|---|---|
| Crème Vanille | `rgb(247,235,215)` | Warm vanilla-cream ground |
| Brume Alpine | `rgb(168,178,196)` | Cool mist-blue regulator |
| Rose Méndl | `rgb(237,148,158)` | Signature old-rose facade tone |
| Doré Antique | `rgb(176,136,60)` | Antique dim gold |
| Violet Concierge | `rgb(128,88,148)` | Formal concierge purple |
| Bordeaux Vintage | `rgb(143,52,65)` | Vintage burgundy shadow |

#### Full Palette

```text
Rose Méndl        rgb(237, 148, 158)
Violet Concierge  rgb(128,  88, 148)
Crème Vanille     rgb(247, 235, 215)
Doré Antique      rgb(176, 136,  60)
Brume Alpine      rgb(168, 178, 196)
Bordeaux Vintage  rgb(143,  52,  65)
```

Design logic: rose and purple carry the central fairy-tale image, cream
provides the atmosphere, gold adds aristocratic weight, mist-blue cools the
page down, and burgundy stops the palette from collapsing into pastry-box
sweetness.

### Palette 18 — Renaissance Florence

#### Color Philosophy

Florentine color is not invented so much as extracted from materials: lapis,
gold leaf, baked clay, walnut, cypress, ivory gesso. The palette therefore
feels naturally ordered rather than merely styled, balancing sacred blue and
gold with earthly terracotta and wood.

#### Six-Color Set

| Name | RGB | Note |
|---|---|---|
| Avorio Fiorentino | `rgb(238,228,208)` | Florentine ivory ground |
| Oro dell'Altare | `rgb(190,148,52)` | Old altar gold |
| Cotto Brunellesco | `rgb(172,84,50)` | Brunelleschi terracotta |
| Verde Cipresso | `rgb(54,80,60)` | Deep cypress green |
| Oltremare di Lapislazzuli | `rgb(46,70,118)` | Lapis ultramarine blue |
| Noce Toscano | `rgb(85,54,34)` | Tuscan walnut brown |

#### Full Palette

```text
Avorio Fiorentino        rgb(238, 228, 208)
Oro dell'Altare          rgb(190, 148,  52)
Cotto Brunellesco        rgb(172,  84,  50)
Oltremare di Lapislazzuli rgb( 46,  70, 118)
Verde Cipresso           rgb( 54,  80,  60)
Noce Toscano             rgb( 85,  54,  34)
```

Design logic: lapis and altar gold establish the sacred register, ivory and
terracotta soften it into lived human craft, while cypress and walnut pull the
palette back toward earth and handwork.

### Palette 19 — Soviet Avant-Garde

#### Color Philosophy

Soviet Avant-Garde rejects harmony, gradient, and ornament. Each color behaves
like a hard-edged declaration: red acts, black negates, grey bears industrial
weight, blue thinks in diagrams, ochre promises the future in propaganda tones,
and newsprint white keeps the whole thing rough and public.

#### Six-Color Set

| Name | RGB | Note |
|---|---|---|
| ГАЗЕТА | `rgb(225,218,205)` | Newsprint white, rough and democratic |
| ПЛАКАТ | `rgb(200,150,32)` | Poster-ochre promise |
| БЕТОН | `rgb(118,114,108)` | Concrete industrial grey |
| ЧЕРТЁЖ | `rgb(50,80,138)` | Blueprint-mechanical blue |
| КРАСНЫЙ | `rgb(196,28,28)` | Constructivist revolutionary red |
| ЧЁРНЫЙ | `rgb(24,20,18)` | Absolute iron-black |

#### Full Palette

```text
КРАСНЫЙ  rgb(196,  28,  28)
ЧЁРНЫЙ   rgb( 24,  20,  18)
БЕТОН    rgb(118, 114, 108)
ЧЕРТЁЖ   rgb( 50,  80, 138)
ГАЗЕТА   rgb(225, 218, 205)
ПЛАКАТ   rgb(200, 150,  32)
```

Design logic: the red-black collision is the core grammar, industrial grey
forms the spine, blueprint blue adds cold reason, newsprint white recalls mass
circulation, and ochre lowers utopian promise into the rust of history.

### Palette 20 — Constantinople

#### Color Philosophy

Constantinople has to belong to Greece and Rome, Byzantium, Islam, Christianity,
and the Ottoman city at once. Gold, blue, purple, ochre, ivory, and cypress
green are therefore not decorative extras but the material afterimage of a city
where multiple civilizations keep pressing through the same stone.

#### Six-Color Set

| Name | RGB | Note |
|---|---|---|
| Λευκός · Fildişi | `rgb(236,225,207)` | Warm ivory marble base |
| Χρυσός · Altın | `rgb(195,150,42)` | Old Hagia-Sophia gold |
| Ώχρα · Toprak | `rgb(170,112,50)` | City-wall ochre earth |
| Κυπαρίσσι · Selvi | `rgb(50,76,58)` | Cypress-dark green |
| Πορφύρα · Mor | `rgb(102,32,65)` | Imperial porphyry purple |
| Βόσπορος · Boğaz | `rgb(30,52,88)` | Evening Bosphorus blue |

#### Full Palette

```text
Χρυσός · Altın       rgb(195, 150,  42)
Βόσπορος · Boğaz     rgb( 30,  52,  88)
Πορφύρα · Mor        rgb(102,  32,  65)
Ώχρα · Toprak        rgb(170, 112,  50)
Λευκός · Fildişi     rgb(236, 225, 207)
Κυπαρίσσι · Selvi    rgb( 50,  76,  58)
```

Design logic: deep blue and ochre create the east-west temperature axis,
gold-purple-ivory form the sacred triangle, and cypress green supplies the long
historical shadow that keeps the palette from becoming merely luxurious.

### Palette 21 — France

#### Color Philosophy

France should not read as literal flag colors. Its red needs the weight of wine
and blood, its white is really champagne ivory, and its blue has to carry the
gravity of Enlightenment reason. Lavender, olive-gold, and Parisian zinc bring
in the fractures between republic, province, aristocratic memory, and modern
city.

#### Six-Color Set

| Name | RGB | Note |
|---|---|---|
| Ivoire Champagne | `rgb(232,222,205)` | Champagne ivory rather than pure white |
| Olive Dorée | `rgb(142,133,58)` | Versailles olive-gold |
| Zinc Parisien | `rgb(122,126,132)` | Paris rooftop zinc grey |
| Lavande Provençale | `rgb(143,108,148)` | Southern lavender purple |
| Rouge Marianne | `rgb(180,32,40)` | Republic red with tannic depth |
| Bleu République | `rgb(44,74,138)` | Republic blue of reason and state |

#### Full Palette

```text
Rouge Marianne      rgb(180,  32,  40)
Bleu République     rgb( 44,  74, 138)
Ivoire Champagne    rgb(232, 222, 205)
Lavande Provençale  rgb(143, 108, 148)
Olive Dorée         rgb(142, 133,  58)
Zinc Parisien       rgb(122, 126, 132)
```

Design logic: the tricolor is reinterpreted as cultural matter instead of a
flat political emblem; lavender and zinc open a north-south fracture, while
olive-gold and deep blue quietly stage the old tension between monarchy and
republic.

### Palette 22 — Kyoto

#### Color Philosophy

Kyoto never announces itself. Warm silk-white, sakura-grey, bamboo-grey,
weathered tea-brown, moss green, and dark indigo form the six-color base of a
city built on restraint, mist, and aftertone. Vermilion is allowed to appear,
but only in miniature, like the only warm living thing in an otherwise hushed
tea room.

#### Six-Color Set

| Name | RGB | Note |
|---|---|---|
| Kinushiro | `rgb(234,226,212)` | Silk-paper warm white |
| Sakura-nezumi | `rgb(204,184,178)` | Fallen-blossom grey pink |
| Aotake-nezumi | `rgb(116,126,120)` | Misty bamboo grey |
| Karacha | `rgb(110,84,64)` | Weathered tea-brown wood tone |
| Koke-iro | `rgb(80,94,68)` | Moss-dark green |
| Kon | `rgb(34,40,66)` | Noh-night indigo |

#### Spot Color

| Name | RGB | Note |
|---|---|---|
| Shu-hi | `rgb(170,50,36)` | Vermilion used only as a small decisive accent |

#### Full Palette

```text
Kinushiro      rgb(234, 226, 212)
Karacha        rgb(110,  84,  64)
Sakura-nezumi  rgb(204, 184, 178)
Aotake-nezumi  rgb(116, 126, 120)
Koke-iro       rgb( 80,  94,  68)
Kon            rgb( 34,  40,  66)
-------------------------------------------
Shu-hi         rgb(170,  50,  36)  spotcolor
```

Design logic: silence and negative space are the skeleton, bamboo-grey and
tea-brown hold the temperature in balance, all six base tones refuse brightness,
and the vermilion only works because it is not allowed to become a field color.

### Palette 23 — Siamese Dream

#### Color Philosophy

Siamese Dream is a study in adolescent contradiction: overexposed light, soft
focus, low-temperature orange, and organic dark green. Its most beautiful tones
are also the least trustworthy. The palette never erupts; it seeps, like a wall
of distorted guitars carrying feelings that were never allowed to speak plainly.

#### Six-Color Set

| Name | RGB | Note |
|---|---|---|
| Luna | `rgb(238,226,208)` | Overexposed warm white afterglow |
| Disarm | `rgb(182,180,193)` | Vulnerable grey-violet |
| Today | `rgb(198,158,65)` | Beautiful but suspect faded gold |
| Hummer | `rgb(150,145,135)` | Floating shoegaze smoke-grey |
| Mayonaise | `rgb(188,105,40)` | Low-temperature emotional orange |
| Soma | `rgb(42,68,48)` | Organic black-substitute dark green |

#### Full Palette

```text
Luna       rgb(238, 226, 208)
Disarm     rgb(182, 180, 193)
Today      rgb(198, 158,  65)
Hummer     rgb(150, 145, 135)
Mayonaise  rgb(188, 105,  40)
Soma       rgb( 42,  68,  48)
```

Design logic: Luna and Hummer create the overexposed haze layer, Today and
Disarm supply the emotional contradiction, Mayonaise acts as a slow-burn core
rather than a flame, and Soma stands in for black while remaining stubbornly
alive.

---

## Available Environments

### Content boxes

```latex
\begin{infobox}   ... \end{infobox}    % blue-tinted background
\begin{warnbox}   ... \end{warnbox}    % amber-tinted background
\begin{resultbox} ... \end{resultbox}  % palette secondary background
\begin{goalbox}   ... \end{goalbox}    % solid palette primary background
```

### Theorem-like environments

```latex
\begin{De}{Title}{label}  ... \end{De}   % Definition
\begin{The}{Title}{label} ... \end{The}  % Theorem
\begin{Pro}{Title}{label} ... \end{Pro}  % Proposition
\begin{Le}{Title}{label}  ... \end{Le}   % Lemma
\begin{Co}{Title}{label}  ... \end{Co}   % Corollary
\begin{Exa}{Title}{label} ... \end{Exa}  % Example
\begin{Rmk}{Title}{label} ... \end{Rmk}  % Remark
```

### Proof and container

```latex
\begin{Proof}  ... \end{Proof}   % proof with QED mark
\begin{Boxed}  ... \end{Boxed}   % rounded grey container
```

### Chapter-introduction panels

```latex
\begin{Intro}{Header}{Body text}      \end{Intro}       % title top-left
\begin{RightIntro}{Header}{Body text} \end{RightIntro}  % title top-right
```

### Inline helpers

```latex
\UnderlineBox{text}              % double-ruled underlined block
\Quote{quotation}{attribution}   % formatted pull-quote
\Minipage{w1}{left}{w2}{right}   % side-by-side two minipages
\Eq{expression}                  % centred unlabelled equation
\EqL{expression}{label}          % centred labelled equation
\EvOdd{lines}{width}{content}    % right-margin wrapfigure
\textkai{中文楷体}                 % render text in bundled Kai font
```

### Table of contents and page-progress ring (v1.1+)

```latex
\section{Overview}        % use standard \section{...} to mark groups
\section{Methods}
\section{Results}

\OUCTocFrame              % renders a TOC frame titled "Contents"
\OUCTocFrame[目录]         % custom frame title
```

Section entries are rendered as numbered pill badges (palette `primary`)
followed by the section title; the section that is *currently* active when
the TOC frame is drawn is highlighted in palette `accent`.

A small circular progress ring is drawn next to the page number in the
footer on every regular content frame. It is filled clockwise in palette
`primary` proportionally to `\insertframenumber / \inserttotalframenumber`,
so the reader can see at a glance how far through the deck you are. The
ring requires no user action — it is enabled automatically by the style.

### Code listings

Frames that contain a `lstlisting` environment must be declared `[fragile]`.  
For listings longer than the threshold (default 20 lines), add `[allowframebreaks]` to auto-paginate:

```latex
\begin{frame}[fragile,allowframebreaks]
    \frametitle{My Code}
    \begin{lstlisting}[language=Matlab]
    % your code here
    \end{lstlisting}
\end{frame}
```

Supported language keys include `Matlab`, `Python`, `bash`, `[LaTeX]TeX`, `C`, `C++`, `Java`, and any language supported by the `listings` package.

---

## Version History

| Version | Date    | Highlights |
|---------|---------|------------|
| **v1.2** | 2026-09 | Palette catalogue expanded from 10 to **24** (`\OUCSetPalette{0..23}`), imported wholesale from the [Thomas-Tufte-Style-Book-Template](https://github.com/Hatsuyuki017/Thomas-Tufte-Style-Book-Template) so a deck and its companion book share one colour system; new palettes 10–23 (Roman Empire, Greece, Kanagawa, Starry Night, A Thousand Li, And Quiet Flows the Don, Cyberpunk Edgerunners, The Grand Budapest Hotel, Renaissance Florence, Soviet Avant-Garde, Constantinople, France, Kyoto, Siamese Dream); added the `spotcolor` theme spot colour (follows `accent`, switches to Kyoto's vermilion under palette 22); README colour chapter replaced with the book template's full quick reference and palette appendix. Also completed and repaired v1.1, which the shipped `.sty` never actually contained: implemented the documented `\OUCTocFrame` contents frame and the circular page-progress ring in the footer, and fixed the footer progress bar overflowing a TeX dimen on the first pass (`\inserttotalframenumber` is only a placeholder until the `.aux` exists), which aborted a from-scratch `latexmk` run. The 24 palette swatch pages now form a **Palette Gallery** section at the end of the manual, just before Acknowledgements; manual grew 40 → 55 pages. |
| **v1.1** | 2026-05 | Added `\OUCTocFrame[Title]` styled table-of-contents (numbered pill badges, current section auto-highlighted in `accent`); added a circular page-progress ring drawn next to the page number in the footer (track in `linegray`, arc in `primary`, fills clockwise from 12 o'clock); manual extended from 36 → 40 pages with TikZ tutorial frames and a TOC demo page. |
| **v1.0** | 2026-05 | Initial release: 10 palettes, theorem-like environments (`The`, `De`, `Exa`, `Rmk`, `Pro`, `Le`, `Co`, `Proof`, `Boxed`), content boxes (`infobox` / `warnbox` / `resultbox` / `goalbox`), `\OUCTitleFrame` / `\OUCClosingFrame`, multi-language `lstlisting` styles, bottom linear progress bar, palette-aware brand colours, palette-controlled TikZ pre-loaded libraries. |

> **Upgrade note (v1.1 → v1.2):** no breaking changes. Palettes 0–9 keep byte-identical RGB values, so existing decks compile to the same colours; indices 10–23 and the `spotcolor` name are purely additive.
>
> **Upgrade note (v1.0 → v1.1):** no breaking changes. Existing decks compile unchanged; the new progress ring activates automatically. To opt into the new TOC frame, add `\section{...}` markers around your content and call `\OUCTocFrame[Contents]` once after `\OUCTitleFrame`.

---

## Licence

The style file and example documents are released under the **MIT Licence** — use freely in academic, personal, and commercial projects.  
Bundled fonts are subject to their own licences (see each font file for details).  
The OUC badge images (`badge/ouc.png`, `badge/AUlightbadge.png`) are copyright of their respective institutions; please replace them when using this template for non-OUC presentations.


---

# OUC Smart Beamer 模板

[English](#ouc-smart-beamer-template) | **中文**

一款精致的 XeLaTeX Beamer 学术演示模板。  
内置 24 套配色方案、定理类环境、代码高亮风格、干净的封面与收尾页、带编号徽标的目录帧，以及紧贴页码的圆环进度条——所有逻辑封装在单一 `.sty` 文件中。

> **当前版本：** v1.2 — 详见[版本历史](#版本历史)。
>
> **效果预览** — 以配色方案 0（OUC Default）编译：
>
> ![OUC Smart Beamer 模板预览](OUC_Smart_Beamer_Template.png)
>
> *详见 `template-manual.pdf`，共 55 页完整使用手册。*

---

## 目录

1. [文件夹结构](#文件夹结构)
2. [使用前提](#使用前提)
   - [macOS](#macos-1)
   - [Windows](#windows-1)
   - [Linux](#linux-1)
3. [快速开始](#快速开始)
4. [编译方式](#编译方式)
5. [Windows 与 Linux 字体说明](#windows-与-linux-字体说明)
6. [自定义参考](#自定义参考)
7. [配色总览](#配色总览)
   - [完整色版速查](#完整色版速查)
   - [附录：全部配色方案详述](#附录全部配色方案详述)
8. [可用环境](#可用环境)
9. [版本历史](#版本历史)
10. [许可证](#许可证)

---

## 文件夹结构

```
beamertemplate/
├── oucsmartbeamer.sty        ← 主样式文件，所有模板逻辑均在此
├── template-manual.tex       ← 完整用户手册（编译得到 55 页 PDF）
├── example.tex               ← 最小示例幻灯片，复制后直接修改即可
├── fonts/                    ← 内置字体（自动加载，无需手动操作）
│   ├── RobotoSerif-Regular.ttf
│   ├── RobotoSerif-Italic.ttf
│   ├── national-2-condensed-bold.ttf
│   ├── DFKaiSho-SB.ttf       ← 楷体，用于 \textkai{...}
│   └── NISC18030.ttf
└── badge/                    ← 内置徽标图片
    ├── ouc.png
    └── AUlightbadge.png
```

> **只需编辑 `example.tex`（或你自己的 `.tex` 文件）即可创建演示文稿。  
> 除非需要为你的操作系统更改字体，否则不要修改 `oucsmartbeamer.sty`。**

---

## 使用前提

### macOS

| 需求 | 获取方式 |
|---|---|
| **MacTeX**（含 XeLaTeX 与所有宏包） | [tug.org/mactex](https://tug.org/mactex/) — 安装完整版（约 5 GB） |
| **Latexmk** | 随 MacTeX 一起安装，无需单独处理 |
| 系统字体 **Songti SC** 与 **Menlo** | macOS 内置，无需任何操作 |

MacTeX 会自动安装所有所需宏包。安装完成后，克隆本仓库即可直接编译，macOS 上无需任何额外配置。

```bash
# 使用 Homebrew 安装 MacTeX（可选方式）
brew install --cask mactex
```

---

### Windows

#### 第一步 — 安装 TeX 发行版

二选一：

| 发行版 | 下载地址 | 说明 |
|---|---|---|
| **TeX Live**（推荐） | [tug.org/texlive](https://tug.org/texlive/) | 完整安装（约 7 GB），含所有宏包 |
| **MiKTeX** | [miktex.org](https://miktex.org/) | 体积较小，缺少的宏包按需自动下载 |

> **注意：** 安装 TeX Live 时请选择 *Full Scheme*（完整安装）。  
> 使用 MiKTeX 时请开启"自动安装缺失宏包"选项。

#### 第二步 — 安装中文字体

本模板默认使用 **Songti SC**（宋体），这是 macOS 专属字体。  
Windows 用户需要替换为一个兼容的 CJK 字体。

**方案 A — 使用免费的 Noto Serif CJK（推荐）：**

1. 从 [Google Fonts / Noto](https://www.google.com/get/noto/) 或 [GitHub releases](https://github.com/notofonts/noto-cjk/releases) 下载 *Noto Serif CJK SC*。
2. 双击 `.ttf` 或 `.otf` 文件安装。

**方案 B — 使用 Windows 内置宋体（SimSun） — 每台 Windows 电脑均自带，无需下载。**

#### 第三步 — 修改 `oucsmartbeamer.sty` 适配 Windows 字体

打开 `oucsmartbeamer.sty`，修改**第 25–28 行**：

```latex
% ──────── 修改前（macOS 默认） ────────
\setmonofont{Menlo}
\setCJKmainfont{Songti SC}
\setCJKsansfont{Songti SC}
\setCJKmonofont{Songti SC}

% ──────── 修改后 — 方案 A：Noto Serif CJK ────────
\setmonofont{Consolas}
\setCJKmainfont{Noto Serif CJK SC}
\setCJKsansfont{Noto Serif CJK SC}
\setCJKmonofont{Noto Serif CJK SC}

% ──────── 修改后 — 方案 B：SimSun ────────
\setmonofont{Consolas}
\setCJKmainfont{SimSun}
\setCJKsansfont{SimSun}
\setCJKmonofont{SimSun}
```

> `Consolas` 在所有 Windows 系统上均已预装。  
> 只需改动以上四行，`.sty` 中的其余内容与操作系统无关，不需要修改。

---

### Linux

1. 通过包管理器安装 **TeX Live**：
   ```bash
   # Debian / Ubuntu
   sudo apt install texlive-full latexmk
   # Arch
   sudo pacman -S texlive-most texlive-lang latexmk
   # Fedora
   sudo dnf install texlive-scheme-full latexmk
   ```
2. 安装中文字体，例如：
   ```bash
   # Debian / Ubuntu — 安装 Noto CJK
   sudo apt install fonts-noto-cjk
   ```
3. 与 Windows 相同，修改 `oucsmartbeamer.sty` 第 25–28 行（使用 `Noto Serif CJK SC` 和 `Liberation Mono`）：
   ```latex
   \setmonofont{Liberation Mono}
   \setCJKmainfont{Noto Serif CJK SC}
   \setCJKsansfont{Noto Serif CJK SC}
   \setCJKmonofont{Noto Serif CJK SC}
   ```

---

## 快速开始

1. **复制** `example.tex` 并重命名，例如 `my-presentation.tex`。
2. **填写**标题、作者、单位和日期。
3. **选择配色方案**（可选，默认为方案 0）：
   ```latex
   \OUCSetPalette{7}   % 0–23，参见配色总览章节
   ```
4. **添加帧**，使用 `\begin{frame}...\end{frame}`。
5. **编译**（见下一节）。

最小示例：

```latex
\documentclass[aspectratio=169,10pt]{beamer}
\usepackage{oucsmartbeamer}

\title{我的演示}
\subtitle{副标题}
\author{你的名字}
\institute{你的单位}
\date{2026}

\OUCBeamerSetup{
    marker=MY TALK,
    footer title=我的演示,
    footer subtitle=你的名字,
    closing title=谢谢,
    closing note=欢迎提问
}

\begin{document}
\OUCTitleFrame

%% 可选：带编号徽标的目录帧
\OUCTocFrame[目录]

\section{引言}
\begin{frame}
    \frametitle{引言}
    你的内容。
\end{frame}

\OUCClosingFrame
\end{document}
```

---

## 编译方式

必须使用 **XeLaTeX**（内置 TTF 字体与 CJK 支持均依赖 XeLaTeX）：

```bash
# 推荐 — 自动多遍编译
latexmk -xelatex my-presentation.tex

# 或手动执行（运行两遍以解析交叉引用）
xelatex my-presentation.tex
xelatex my-presentation.tex
```

> **不要使用 `pdflatex` 或 `lualatex`** — 模板将回退到基础字体，丢失所有自定义排版。

编译内置手册：

```bash
latexmk -xelatex template-manual.tex   # → template-manual.pdf（55 页）
latexmk -xelatex example.tex           # → example.pdf（4 页）
```

---

## Windows 与 Linux 字体说明

模板以两种方式加载字体：

| 字体 | 加载方式 | Windows/Linux 操作 |
|---|---|---|
| `RobotoSerif`（英文正文衬线体） | 从 `fonts/` 目录加载 — **已内置** | 无需操作 ✓ |
| `national-2-condensed-bold`（展示标题） | 从 `fonts/` 目录加载 — **已内置** | 无需操作 ✓ |
| `DFKaiSho-SB`（楷体，用于 `\textkai{}`） | 从 `fonts/` 目录加载 — **已内置** | 无需操作 ✓ |
| `Menlo`（等宽字体） | macOS 系统字体 | 替换为 `Consolas`（Win）/ `Liberation Mono`（Linux） |
| `Songti SC`（宋体 CJK） | macOS 系统字体 | 替换为 `Noto Serif CJK SC` 或 `SimSun` |

只有**最后两行**需要修改，改动仅涉及 `oucsmartbeamer.sty` 的 4 行代码。

---

## 自定义参考

所有配置均写在你的 `.tex` 文件**导言区**：

```latex
% ── 元数据（驱动封面与页脚内容） ─────────────────────────────────────
\title{你的标题}
\subtitle{副标题}
\author{作者甲 \and 作者乙}
\institute{你的单位}
\date{日期或主题}

% ── 模板设置 ──────────────────────────────────────────────────────────
\OUCBeamerSetup{
    marker          = MY TALK,            % 封面右上角标识文字
    left logo       = badge/ouc.png,      % 左侧徽标路径
    right logo      = badge/ouc.png,      % 右侧徽标路径
    footer title    = 我的演示,            % 页脚主标题（加粗）
    footer subtitle = 章节名称,            % 页脚副标题
    closing title   = 谢谢！,              % 收尾页主标题
    closing subtitle= 我的演示,            % 收尾页副标题
    closing note    = 欢迎提问             % 收尾页说明文字
}

% ── 字号设置 ──────────────────────────────────────────────────────────
\OUCSetTitleFontSize{30}{34}    % 封面主标题：{字号pt}{行距pt}
\OUCSetBodyFontSize{\normalsize}% 正文字号开关
\OUCSetHeaderFontSize{\large}   % 页眉 frametitle 字号开关
\OUCSetFooterFontSize{\small}   % 页脚字号开关

% ── 配色方案（0–23） ───────────────────────────────────────────────────
\OUCSetPalette{7}

% ── 代码块行数警告阈值（默认 20）────────────────────────────────────────
\OUCSetLstMaxLines{25}
```

---

## 配色总览

全部 24 套配色（编号 `0..23`）整体取自
[Thomas-Tufte-Style-Book-Template](https://github.com/Hatsuyuki017/Thomas-Tufte-Style-Book-Template)，
使幻灯片与配套书籍可以使用完全一致的色彩体系。每套配色暴露六个色板，由浅至深排列。

在导言区任意位置选择一套：

```latex
\OUCSetPalette{7}   % N 取 0..23
```

样式文件暴露以下颜色名：

- `oucpal1` 到 `oucpal6`：按由浅到深排列
- `primary`：`pal5`；页眉标题、页脚强调、定理与 block 标题
- `secondary`：`pal4`；例题 / 备注 / 引言面板的标题背景
- `accent`：`pal3`；itemize 次级条目、装饰色条
- `softblue`：`pal2`；例题 / 备注 / 引言面板的正文背景
- `paleblue`：`pal1`；`lstlisting` 代码块背景
- `oucpal6`：最深色；`lstlisting` 描边与强调色，也可自由取用
- `spotcolor`：主题点睛色；默认等于 `accent`，在 Kyoto（22 号）下切换为朱绯 `rgb(170,50,36)`

`\OUCPaletteName` 会展开为当前配色的名称，适合放在版权页上。

下表列出全部 24 套配色的编号、名称、主色与气质概要。

| N | 名称 | Primary (pal5) | 最深色 (pal6) | 风格关键词 |
|---|---|---|---|---|
| 0 | OUC Default | `rgb(30,58,138)` | `rgb(30,41,59)` | 经典学术蓝 |
| 1 | Brunneophobia | `rgb(86,67,53)` | `rgb(42,23,14)` | 暖土、烧褐、厚重 |
| 2 | Van Dyke | `rgb(68,60,94)` | `rgb(61,43,39)` | 灰紫、内敛、旧画布 |
| 3 | Back in Black | `rgb(74,63,75)` | `rgb(22,19,21)` | 近单色、烟粉、炭黑 |
| 4 | Belle of the Ball | `rgb(118,118,44)` | `rgb(53,77,4)` | 橄榄、珊瑚、复古舞会 |
| 5 | Pine Tree | `rgb(167,88,26)` | `rgb(43,47,34)` | 秋金、松影、赭褐 |
| 6 | Provence Blue | `rgb(82,92,121)` | `rgb(53,66,94)` | 普罗旺斯雾蓝 |
| 7 | Fresco Blue | `rgb(4,75,102)` | `rgb(2,31,46)` | 壁画蓝、清冷海青 |
| 8 | Monet | `rgb(16,86,102)` | `rgb(10,51,35)` | 印象派粉彩与深青 |
| 9 | Narcissus | `rgb(190,108,26)` | `rgb(110,60,31)` | 沙土、暖金、铁锈橘 |
| 10 | Roman Empire | `rgb(120,20,40)` | `rgb(88,28,90)` | 罗马、军团红、骨螺紫 |
| 11 | Greece | `rgb(48,105,175)` | `rgb(90,42,92)` | 希腊、民主蓝、陶器赤 |
| 12 | Kanagawa | `rgb(13,38,76)` | `rgb(29,25,35)` | 江户、浪蓝、墨线 |
| 13 | Starry Night | `rgb(22,50,30)` | `rgb(20,36,88)` | 夜空、月黄、柏影 |
| 14 | A Thousand Li | `rgb(48,105,76)` | `rgb(35,78,112)` | 千里江山、青绿、古绢 |
| 15 | And Quiet Flows the Don | `rgb(52,70,90)` | `rgb(88,26,24)` | 顿河、浊蓝、暗血 |
| 16 | Cyberpunk Edgerunners | `rgb(15,32,98)` | `rgb(14,8,28)` | 夜都、荧光、赛博过载 |
| 17 | The Grand Budapest Hotel | `rgb(128,88,148)` | `rgb(143,52,65)` | 旧贵族、粉紫、奶油底 |
| 18 | Renaissance Florence | `rgb(46,70,118)` | `rgb(85,54,34)` | 文艺复兴、青金、陶红 |
| 19 | Soviet Avant-Garde | `rgb(196,28,28)` | `rgb(24,20,18)` | 构成主义、红黑、工业 |
| 20 | Constantinople | `rgb(102,32,65)` | `rgb(30,52,88)` | 拜占庭、金辉、海都 |
| 21 | France | `rgb(180,32,40)` | `rgb(44,74,138)` | 法兰西、红白蓝再解读 |
| 22 | Kyoto | `rgb(80,94,68)` | `rgb(34,40,66)` | 京都、禅寂、幽玄 |
| 23 | Siamese Dream | `rgb(188,105,40)` | `rgb(42,68,48)` | 失真摇滚、青春期、连体梦境 |


---

## 完整色版速查

正文部分保留每套 palette 的“完整色版”，便于直接浏览与选择。六色均按 `pal1 -> pal6` 由浅到深排列。Kyoto 另有 `spotcolor = rgb(170,50,36)`。

### 0. OUC Default

```text
OUC Default A   rgb(239, 246, 255)
OUC Default B   rgb(219, 234, 254)
OUC Default C   rgb( 96, 165, 250)
OUC Default D   rgb( 37,  99, 235)
OUC Default E   rgb( 30,  58, 138)
OUC Default F   rgb( 30,  41,  59)
```

### 1. Brunneophobia

```text
Brunneophobia A rgb(238, 211, 180)
Brunneophobia B rgb(213, 148,  79)
Brunneophobia C rgb(213, 148,  79)
Brunneophobia D rgb(180,  69,  15)
Brunneophobia E rgb( 86,  67,  53)
Brunneophobia F rgb( 42,  23,  14)
```

### 2. Van Dyke

```text
Van Dyke A       rgb(236, 194, 188)
Van Dyke B       rgb(169, 159, 191)
Van Dyke C       rgb(169, 159, 191)
Van Dyke D       rgb(191, 113, 133)
Van Dyke E       rgb( 68,  60,  94)
Van Dyke F       rgb( 61,  43,  39)
```

### 3. Back in Black

```text
Back in Black A  rgb(240, 217, 228)
Back in Black B  rgb(193, 160, 172)
Back in Black C  rgb(193, 160, 172)
Back in Black D  rgb(128, 108, 121)
Back in Black E  rgb( 74,  63,  75)
Back in Black F  rgb( 22,  19,  21)
```

### 4. Belle of the Ball

```text
Belle A          rgb(226, 203, 192)
Belle B          rgb(206, 171, 150)
Belle C          rgb(210, 135, 106)
Belle D          rgb(229,  74,  57)
Belle E          rgb(118, 118,  44)
Belle F          rgb( 53,  77,   4)
```

### 5. Pine Tree

```text
Pine Tree A      rgb(238, 200, 111)
Pine Tree B      rgb(222, 166,  32)
Pine Tree C      rgb(222, 166,  32)
Pine Tree D      rgb(177, 120, 133)
Pine Tree E      rgb(167,  88,  26)
Pine Tree F      rgb( 43,  47,  34)
```

### 6. Provence Blue

```text
Provence A       rgb(170, 188, 175)
Provence B       rgb(137, 156, 154)
Provence C       rgb(137, 156, 154)
Provence D       rgb(110, 124, 139)
Provence E       rgb( 82,  92, 121)
Provence F       rgb( 53,  66,  94)
```

### 7. Fresco Blue

```text
Fresco A         rgb(166, 224, 244)
Fresco B         rgb( 71, 169, 207)
Fresco C         rgb( 71, 169, 207)
Fresco D         rgb(  9, 121, 158)
Fresco E         rgb(  4,  75, 102)
Fresco F         rgb(  2,  31,  46)
```

### 8. Monet

```text
Monet A          rgb(247, 244, 213)
Monet B          rgb(211, 150, 140)
Monet C          rgb(211, 150, 140)
Monet D          rgb(131, 153,  88)
Monet E          rgb( 16,  86, 102)
Monet F          rgb( 10,  51,  35)
```

### 9. Narcissus

```text
Narcissus A      rgb(221, 213, 200)
Narcissus B      rgb(185, 149, 144)
Narcissus C      rgb(185, 149, 144)
Narcissus D      rgb(199, 149,  72)
Narcissus E      rgb(190, 108,  26)
Narcissus F      rgb(110,  60,  31)
```

### 10. Roman Empire

```text
Carrara Marble   rgb(236, 232, 225)
Gloria Aurum     rgb(212, 175,  55)
Laurel Viridis   rgb( 74, 110,  65)
Legion Crimson   rgb(180,  30,  30)
Senate Bordeaux  rgb(120,  20,  40)
Tyrian Purple    rgb( 88,  28,  90)
```

### 11. Greece

```text
Parian Marble      rgb(245, 240, 228)
Gloria Aurum       rgb(212, 175,  55)
Athena's Olive     rgb( 98, 128,  48)
Attic Terracotta   rgb(188,  82,  38)
Agora Kyanos       rgb( 48, 105, 175)
Dionysian Grape    rgb( 90,  42,  92)
```

### 12. Kanagawa

```text
Nami-shiro       rgb(237, 233, 222)
Boten            rgb(208, 224, 238)
Fuji-gasumi      rgb(150, 186, 210)
Bero-ai          rgb( 26,  78, 132)
Shinkai          rgb( 13,  38,  76)
Sumi             rgb( 29,  25,  35)
```

### 13. Starry Night

```text
Lumière Lunaire    rgb(240, 208,  68)
Lueurs du Village  rgb(198, 140,  52)
Aube Glacée        rgb(105, 155, 200)
Tourbillon Outremer rgb( 48,  96, 165)
Cyprès Nocturne    rgb( 22,  50,  30)
Minuit Cobalt      rgb( 20,  36,  88)
```

### 14. A Thousand Li

```text
Song Silk        rgb(218, 203, 170)
Sky Azurite      rgb(110, 165, 195)
Ochre-Gold       rgb(183, 118,  45)
Pale Malachite   rgb( 96, 148, 110)
Malachite True   rgb( 48, 105,  76)
Azurite Deep     rgb( 35,  78, 112)
```

### 15. And Quiet Flows the Don

```text
Полынь            rgb(142, 120,  70)
Степной Пепел     rgb(110, 108, 104)
Донская Земля     rgb(118,  86,  52)
Ржавое Железо     rgb(122,  66,  36)
Мутный Дон        rgb( 52,  70,  90)
Запёкшаяся Кровь  rgb( 88,  26,  24)
```

### 16. Cyberpunk Edgerunners

```text
Psycho Yellow    rgb(225, 255,   8)
Flatline Green   rgb( 10, 238, 100)
Neon Magenta     rgb(238,  18, 120)
Edgerunner Red   rgb(205,  20,  35)
Luna Blue        rgb( 15,  32,  98)
Night City Void  rgb( 14,   8,  28)
```

### 17. The Grand Budapest Hotel

```text
Crème Vanille      rgb(247, 235, 215)
Brume Alpine       rgb(168, 178, 196)
Rose Méndl         rgb(237, 148, 158)
Doré Antique       rgb(176, 136,  60)
Violet Concierge   rgb(128,  88, 148)
Bordeaux Vintage   rgb(143,  52,  65)
```

### 18. Renaissance Florence

```text
Avorio Fiorentino            rgb(238, 228, 208)
Oro dell'Altare              rgb(190, 148,  52)
Cotto Brunellesco            rgb(172,  84,  50)
Verde Cipresso               rgb( 54,  80,  60)
Oltremare di Lapislazzuli    rgb( 46,  70, 118)
Noce Toscano                 rgb( 85,  54,  34)
```

### 19. Soviet Avant-Garde

```text
ГАЗЕТА   rgb(225, 218, 205)
ПЛАКАТ   rgb(200, 150,  32)
БЕТОН    rgb(118, 114, 108)
ЧЕРТЁЖ   rgb( 50,  80, 138)
КРАСНЫЙ  rgb(196,  28,  28)
ЧЁРНЫЙ   rgb( 24,  20,  18)
```

### 20. Constantinople

```text
Λευκός · Fildişi   rgb(236, 225, 207)
Χρυσός · Altın     rgb(195, 150,  42)
Ώχρα · Toprak      rgb(170, 112,  50)
Κυπαρίσσι · Selvi  rgb( 50,  76,  58)
Πορφύρα · Mor      rgb(102,  32,  65)
Βόσπορος · Boğaz   rgb( 30,  52,  88)
```

### 21. France

```text
Ivoire Champagne    rgb(232, 222, 205)
Olive Dorée         rgb(142, 133,  58)
Zinc Parisien       rgb(122, 126, 132)
Lavande Provençale  rgb(143, 108, 148)
Rouge Marianne      rgb(180,  32,  40)
Bleu République     rgb( 44,  74, 138)
```

### 22. Kyoto

```text
Kinushiro      rgb(234, 226, 212)
Sakura-nezumi  rgb(204, 184, 178)
Aotake-nezumi  rgb(116, 126, 120)
Karacha        rgb(110,  84,  64)
Koke-iro       rgb( 80,  94,  68)
Kon            rgb( 34,  40,  66)
Shu-hi         rgb(170,  50,  36)   % spotcolor
```

### 23. Siamese Dream

```text
Luna           rgb(238, 226, 208)
Disarm         rgb(182, 180, 193)
Today          rgb(198, 158,  65)
Hummer         rgb(150, 145, 135)
Mayonaise      rgb(188, 105,  40)
Soma           rgb( 42,  68,  48)
```

---

## 附录：全部配色方案详述

以下附录中，原有 10 套基础 palette 与扩展的 14 套主题 palette 采用统一体例：

- 色彩哲学
- 六色配色组表格
- 完整色板
- 结构性说明文本

### Palette 0 — OUC Default

#### 色彩哲学

这是一套以学院、海洋与结构秩序为核心的深蓝配色。它的逻辑不是“炫技”，而是为信息排布建立稳定骨架：浅蓝负责留白，亮蓝负责导视，海军蓝负责权威，近黑蓝负责收束。

#### 六色配色组

| 颜色 | RGB | 说明 |
|---|---|---|
| Mist Blue | `rgb(239,246,255)` | 近白浅蓝，用于背景与呼吸空间 |
| Soft Sky | `rgb(219,234,254)` | 次浅层，适合轻量信息区 |
| Signal Blue | `rgb(96,165,250)` | 导视蓝，用于提示与弱强调 |
| Structural Blue | `rgb(37,99,235)` | 中层结构色，清晰且现代 |
| Academic Navy | `rgb(30,58,138)` | 主色，稳定、理性、带学院权威 |
| Deep Harbor | `rgb(30,41,59)` | 最深锚点，用于最强对比与收边 |

#### 完整色板

```text
Mist Blue        rgb(239, 246, 255)
Soft Sky         rgb(219, 234, 254)
Signal Blue      rgb( 96, 165, 250)
Structural Blue  rgb( 37,  99, 235)
Academic Navy    rgb( 30,  58, 138)
Deep Harbor      rgb( 30,  41,  59)
```

结构说明：这组色从几乎不可见的浅蓝一路收束到深港湾蓝，形成非常清晰的层级链。它适合学术正文、目录、章节标题与表格表头，也最接近模板的默认气质。

### Palette 1 — Brunneophobia

#### 色彩哲学

Brunneophobia 以烧土、木器、皮革和窑火残温为基调。它不是明亮的棕，而是被岁月熏过的褐；它给人的感受更像是陶器表面、旧木桌面和书脊革面，适合厚重但不压迫的书籍视觉。

#### 六色配色组

| 颜色 | RGB | 说明 |
|---|---|---|
| Clay Mist | `rgb(238,211,180)` | 浅陶土底色 |
| Ochre Sand | `rgb(213,148,79)` | 暖黄褐中层 |
| Ochre Sand | `rgb(213,148,79)` | 重复槽位，用于 5 色 palette 映射 |
| Kiln Orange | `rgb(180,69,15)` | 窑火赭橙 |
| Walnut Brown | `rgb(86,67,53)` | 主色，稳重木褐 |
| Charred Earth | `rgb(42,23,14)` | 最深焦土色 |

#### 完整色板

```text
Clay Mist     rgb(238, 211, 180)
Ochre Sand    rgb(213, 148,  79)
Ochre Sand    rgb(213, 148,  79)
Kiln Orange   rgb(180,  69,  15)
Walnut Brown  rgb( 86,  67,  53)
Charred Earth rgb( 42,  23,  14)
```

结构说明：浅陶土与焦土黑拉开两端，中间用烧赭色压缩空间，因此整组色温暖、稳定、克制，适合文学、历史或旧物气质明显的内容。

### Palette 2 — Van Dyke

#### 色彩哲学

Van Dyke 像旧画布、玫瑰灰与褪色靛紫之间的低语。它不靠高对比夺目，而靠一种近乎粉尘感的暗雅来维持存在，适合需要柔和戏剧性的页面。

#### 六色配色组

| 颜色 | RGB | 说明 |
|---|---|---|
| Dust Rose | `rgb(236,194,188)` | 浅灰粉底 |
| Faded Indigo | `rgb(169,159,191)` | 雾靛紫 |
| Faded Indigo | `rgb(169,159,191)` | 重复槽位 |
| Old Wine | `rgb(191,113,133)` | 旧酒红中层 |
| Muted Indigo | `rgb(68,60,94)` | 主色，低饱和靛紫 |
| Burnt Umber | `rgb(61,43,39)` | 深棕灰锚点 |

#### 完整色板

```text
Dust Rose      rgb(236, 194, 188)
Faded Indigo   rgb(169, 159, 191)
Faded Indigo   rgb(169, 159, 191)
Old Wine       rgb(191, 113, 133)
Muted Indigo   rgb( 68,  60,  94)
Burnt Umber    rgb( 61,  43,  39)
```

结构说明：粉、紫、酒红和棕灰共同形成一条旧油画式的综合色链，视觉情绪偏安静、偏文学，也比普通紫系更沉着。

### Palette 3 — Back in Black

#### 色彩哲学

这套 palette 不是纯黑白，而是带烟粉残温的近单色体系。它像舞台幕后、天鹅绒暗影与化妆镜边缘残留的暖灰粉，在单色控制中保留了一丝人味。

#### 六色配色组

| 颜色 | RGB | 说明 |
|---|---|---|
| Powder Haze | `rgb(240,217,228)` | 浅烟粉 |
| Mauve Dust | `rgb(193,160,172)` | 雾粉紫 |
| Mauve Dust | `rgb(193,160,172)` | 重复槽位 |
| Velvet Gray | `rgb(128,108,121)` | 灰紫中层 |
| Charcoal Mauve | `rgb(74,63,75)` | 主色，炭灰紫 |
| Stage Black | `rgb(22,19,21)` | 最深近黑 |

#### 完整色板

```text
Powder Haze    rgb(240, 217, 228)
Mauve Dust     rgb(193, 160, 172)
Mauve Dust     rgb(193, 160, 172)
Velvet Gray    rgb(128, 108, 121)
Charcoal Mauve rgb( 74,  63,  75)
Stage Black    rgb( 22,  19,  21)
```

结构说明：近单色体系意味着它不会干扰排版结构，但烟粉底让它不至于冷硬到失去质感，适合沉静、精致、偏展览式的页面。

### Palette 4 — Belle of the Ball

#### 色彩哲学

这套 palette 像复古舞会：瓷粉底、珊瑚红光与末段橄榄深绿在同一舞厅里相遇。它有轻微戏剧性，但主色落在橄榄上，因此最终仍是受控制的复古感。

#### 六色配色组

| 颜色 | RGB | 说明 |
|---|---|---|
| Porcelain Blush | `rgb(226,203,192)` | 浅粉米色 |
| Antique Peach | `rgb(206,171,150)` | 旧桃色 |
| Coral Clay | `rgb(210,135,106)` | 珊瑚土色 |
| Ballroom Coral | `rgb(229,74,57)` | 亮珊瑚强调 |
| Olive Court | `rgb(118,118,44)` | 主色，橄榄宫廷绿 |
| Moss Shadow | `rgb(53,77,4)` | 最深苔影绿 |

#### 完整色板

```text
Porcelain Blush rgb(226, 203, 192)
Antique Peach   rgb(206, 171, 150)
Coral Clay      rgb(210, 135, 106)
Ballroom Coral  rgb(229,  74,  57)
Olive Court     rgb(118, 118,  44)
Moss Shadow     rgb( 53,  77,   4)
```

结构说明：浅暖底负责旧贵族柔光，珊瑚负责舞会的瞬时亮度，橄榄和苔影把整体重新压回复古而非甜腻的方向。

### Palette 5 — Pine Tree

#### 色彩哲学

Pine Tree 是一套秋意极强的 palette。金黄、赭橙、松影绿和深炭灰共同构成暮秋林地的空间：暖色负责光，深色负责树影与风干之后的静默。

#### 六色配色组

| 颜色 | RGB | 说明 |
|---|---|---|
| Autumn Gold | `rgb(238,200,111)` | 秋金底色 |
| Harvest Ochre | `rgb(222,166,32)` | 丰收黄赭 |
| Harvest Ochre | `rgb(222,166,32)` | 重复槽位 |
| Faded Berry | `rgb(177,120,133)` | 微灰莓色过渡 |
| Burnt Orange | `rgb(167,88,26)` | 主色，深赭橙 |
| Pine Shadow | `rgb(43,47,34)` | 最深松林影 |

#### 完整色板

```text
Autumn Gold   rgb(238, 200, 111)
Harvest Ochre rgb(222, 166,  32)
Harvest Ochre rgb(222, 166,  32)
Faded Berry   rgb(177, 120, 133)
Burnt Orange  rgb(167,  88,  26)
Pine Shadow   rgb( 43,  47,  34)
```

结构说明：这是一组典型“暖色推进、深绿收尾”的 palette，适合想要土地感、季节感和轻微叙事情绪的页面。

### Palette 6 — Provence Blue

#### 色彩哲学

Provence Blue 的美感在于其去鲜亮化的冷静。它不像海边明信片那样耀眼，而更像窗台陶盆、雾里石墙和暮色薰衣草田上方的压低天空。

#### 六色配色组

| 颜色 | RGB | 说明 |
|---|---|---|
| Herb Mist | `rgb(170,188,175)` | 灰草本浅层 |
| Stone Green | `rgb(137,156,154)` | 石墙青灰 |
| Stone Green | `rgb(137,156,154)` | 重复槽位 |
| Slate Air | `rgb(110,124,139)` | 板岩空气蓝 |
| Provence Slate | `rgb(82,92,121)` | 主色，普罗旺斯板岩蓝 |
| Evening Indigo | `rgb(53,66,94)` | 最深夜幕蓝 |

#### 完整色板

```text
Herb Mist      rgb(170, 188, 175)
Stone Green    rgb(137, 156, 154)
Stone Green    rgb(137, 156, 154)
Slate Air      rgb(110, 124, 139)
Provence Slate rgb( 82,  92, 121)
Evening Indigo rgb( 53,  66,  94)
```

结构说明：整体色温冷而不硬，灰度充足，因此适合正文页面与目录等需要长期观看的内容，而不会造成刺眼疲劳。

### Palette 7 — Fresco Blue

#### 色彩哲学

Fresco Blue 参考湿壁画和海风吹蚀后的青蓝表面。它的亮部像被石灰稀释过，深部则像颜料渗入墙体深层，是一套非常干净而有历史肌理的蓝绿体系。

#### 六色配色组

| 颜色 | RGB | 说明 |
|---|---|---|
| Wash Blue | `rgb(166,224,244)` | 壁画洗淡浅蓝 |
| Fresh Cyan | `rgb(71,169,207)` | 海青中层 |
| Fresh Cyan | `rgb(71,169,207)` | 重复槽位 |
| Mineral Teal | `rgb(9,121,158)` | 矿物青 |
| Fresco Teal | `rgb(4,75,102)` | 主色，壁画深青 |
| Abyss Ink | `rgb(2,31,46)` | 最深墨海色 |

#### 完整色板

```text
Wash Blue    rgb(166, 224, 244)
Fresh Cyan   rgb( 71, 169, 207)
Fresh Cyan   rgb( 71, 169, 207)
Mineral Teal rgb(  9, 121, 158)
Fresco Teal  rgb(  4,  75, 102)
Abyss Ink    rgb(  2,  31,  46)
```

结构说明：这是一套最适合现代、科技、理工与清爽视觉的基础 palette 之一，深浅分层非常清楚，且整体比 OUC Default 更具设计感。

### Palette 8 — Monet

#### 色彩哲学

Monet 将象牙、灰粉、苔绿和深青压进同一画面，它更像印象派的空气，而不是印象派的花。轻柔但不弱，浅层留白很多，深层却仍有足够的结构支撑。

#### 六色配色组

| 颜色 | RGB | 说明 |
|---|---|---|
| Ivory Light | `rgb(247,244,213)` | 浅象牙底 |
| Dusty Coral | `rgb(211,150,140)` | 灰珊瑚 |
| Dusty Coral | `rgb(211,150,140)` | 重复槽位 |
| Field Green | `rgb(131,153,88)` | 野地绿 |
| Dark Teal | `rgb(16,86,102)` | 主色，深青 |
| Forest Teal | `rgb(10,51,35)` | 最深林影青 |

#### 完整色板

```text
Ivory Light  rgb(247, 244, 213)
Dusty Coral  rgb(211, 150, 140)
Dusty Coral  rgb(211, 150, 140)
Field Green  rgb(131, 153,  88)
Dark Teal    rgb( 16,  86, 102)
Forest Teal  rgb( 10,  51,  35)
```

结构说明：柔和象牙与灰珊瑚让它有很强的页面亲和力，而深青与森林绿则保证了阅读层级，尤其适合叙事型、艺术型文档。

### Palette 9 — Narcissus

#### 色彩哲学

Narcissus 是一组干燥、温暖且带泥土颗粒感的 palette。浅层是砂土与旧布，中段是枯黄赭橙，深段则压到铁锈与木炭棕上，整体非常适合历史、考古与地景主题。

#### 六色配色组

| 颜色 | RGB | 说明 |
|---|---|---|
| Sand Veil | `rgb(221,213,200)` | 浅砂底 |
| Dust Rose | `rgb(185,149,144)` | 尘土玫瑰 |
| Dust Rose | `rgb(185,149,144)` | 重复槽位 |
| Dry Ochre | `rgb(199,149,72)` | 干赭黄 |
| Rust Amber | `rgb(190,108,26)` | 主色，铁锈橘 |
| Burnt Cedar | `rgb(110,60,31)` | 最深焦木棕 |

#### 完整色板

```text
Sand Veil   rgb(221, 213, 200)
Dust Rose   rgb(185, 149, 144)
Dust Rose   rgb(185, 149, 144)
Dry Ochre   rgb(199, 149,  72)
Rust Amber  rgb(190, 108,  26)
Burnt Cedar rgb(110,  60,  31)
```

结构说明：这组色有很强的土气与锈感，适合需要温暖但不甜、古朴但不沉死的页面气氛。

### Palette 10 — Roman Empire

#### 色彩哲学

罗马帝国的颜色必须同时承载石、血、权力、荣誉与凯旋。卡拉拉大理石的冷白是建筑与神庙的基底；军团红与元老院酒红构成权力内部的双重红色结构；月桂绿与荣耀金提供战胜后的秩序与典仪；骨螺紫则作为皇权的终极象征压住全局。

#### 六色配色组

| 名称 | 英文 | RGB | 说明 |
|---|---|---|---|
| 大理石 | Carrara Marble | `rgb(236,232,225)` | 卡拉拉大理石的冷白底色，略带暖灰，呈现神庙与雕像的质感 |
| 荣耀金 | Gloria Aurum | `rgb(212,175,55)` | 凯旋式黄金的中性金，介于铸币与神像镀金之间，不过暖也不过冷 |
| 桂冠 | Laurel Viridis | `rgb(74,110,65)` | 月桂冠叶片的哑光深绿，非翠绿，取干燥叶片的沉稳色调 |
| 罗马军团 | Legion Crimson | `rgb(180,30,30)` | 军团战袍的鲜烈战红，饱和而有力，象征铁与血 |
| 元老院 | Senate Bordeaux | `rgb(120,20,40)` | 元老院托加袍缘的深沉酒红，比军团红更内敛、更权贵 |
| 奥古斯都紫 | Tyrian Purple | `rgb(88,28,90)` | 骨螺紫染料的历史色，价比黄金，专属皇权，深邃而神秘 |

#### 完整色板

```text
Carrara Marble   rgb(236, 232, 225)
Legion Crimson   rgb(180,  30,  30)
Senate Bordeaux  rgb(120,  20,  40)
Laurel Viridis   rgb( 74, 110,  65)
Gloria Aurum     rgb(212, 175,  55)
Tyrian Purple    rgb( 88,  28,  90)
```

设计思路：石白提供文明底盘，双重红色负责军政权力的层次分工，绿色与金色构成凯旋秩序，而骨螺紫作为最高暗部锚点，使整组配色具备帝国神圣性而不流于舞台化。

### Palette 11 — Greece

#### 色彩哲学

希腊主题配色以神庙大理石为底，以民主蓝统领视觉，以荣耀金做高光点缀。陶器赤、橄榄银绿与葡萄紫从文化层面补足人间性、智慧与戏剧性，使其不止停留在“蓝白金”的旅游符号，而具有古典文明的复杂呼吸。

#### 六色配色组

| 名称 | 英文 | RGB | 说明 |
|---|---|---|---|
| 帕罗斯大理石 | Parian Marble | `rgb(245,240,228)` | 暖白而偏象牙，是神庙与雕像的物质底色 |
| 荣耀金 | Gloria Aurum | `rgb(212,175,55)` | 沿用罗马组的中性荣耀金 |
| 橄榄银绿 | Athena's Olive | `rgb(98,128,48)` | 雅典娜所赠橄榄树的沉稳绿调 |
| 陶器赤 | Attic Terracotta | `rgb(188,82,38)` | 红绘陶器底色，是神话与英雄叙事的媒介色 |
| 民主蓝 | Agora Kyanos | `rgb(48,105,175)` | 爱琴海与 Agora 上空的中性蔚蓝 |
| 狄俄尼索斯葡萄紫 | Dionysian Grape | `rgb(90,42,92)` | 象征酒神、戏剧与狂欢节的深紫 |

#### 完整色板

```text
Parian Marble      rgb(245, 240, 228)  ░░  底色·神庙·纯粹
Agora Kyanos       rgb( 48, 105, 175)  ██  主色·民主·爱琴海
Gloria Aurum       rgb(212, 175,  55)  ██  点缀·荣耀·神明
Attic Terracotta   rgb(188,  82,  38)  ██  辅色·叙事·人间
Dionysian Grape    rgb( 90,  42,  92)  ██  暗调·神秘·戏剧
Athena's Olive     rgb( 98, 128,  48)  ██  中调·智慧·生命
```

配色逻辑：以大理石白为底，民主蓝统领视觉重心，金色做高光点缀；陶器赤与橄榄绿构成一对冷暖平衡的中间调，葡萄紫作为最深的暗部锚点，整体在地中海阳光下呈现出既庄重又充满生命力的古典张力。

### Palette 12 — Kanagawa

#### 色彩哲学

《神奈川冲浪里》的革命性在于葛饰北斎将普鲁士蓝引入浮世绘，以单一色系的深浅变奏构建戏剧张力，再以墨线和和纸留白完成空间收束。这是一组以蓝为骨、以白为气、以墨为锚的江户时代色板。

#### 六色配色组

| 名称 | 英文 | RGB | 说明 |
|---|---|---|---|
| 波白·沫雪 | Nami-shiro | `rgb(237,233,222)` | 浪尖破碎的泡沫，非纯白，带有和纸的微暖底色 |
| 暮天·天际 | Boten | `rgb(208,224,238)` | 海平线处的天空渐变色，苍茫而留白 |
| 富士霞·远岚 | Fuji-gasumi | `rgb(150,186,210)` | 远景富士山的淡蓝轮廓，虚化而沉静 |
| ベロ藍·浪蓝 | Bero-ai | `rgb(26,78,132)` | 画面主体，普鲁士蓝浪身 |
| 深海·暗涌 | Shinkai | `rgb(13,38,76)` | 浪底最深处的墨蓝，近乎黑而仍保有蓝的冷意 |
| 墨·轮廓 | Sumi | `rgb(29,25,35)` | 木版印刷的墨线，统摄全图骨架 |

#### 完整色板

```text
ベロ藍  Bero-ai      rgb( 26,  78, 132)  ██  主色·浪·生命力
深海    Shinkai      rgb( 13,  38,  76)  ██  暗调·深渊·压迫感
富士霞  Fuji-gasumi  rgb(150, 186, 210)  ██  中调·远景·永恒
暮天    Boten        rgb(208, 224, 238)  ░░  浅调·天空·呼吸感
波白    Nami-shiro   rgb(237, 233, 222)  ░░  高光·泡沫·和纸质感
墨      Sumi         rgb( 29,  25,  35)  ██  锚点·轮廓·版画骨骼
```

配色逻辑：整组色彩以普鲁士蓝家族为核心，从墨黑→深海蓝→浪蓝→富士霞→暮天→波白构成一条完整的明度递进链，如同浪从深处涌起、在浪尖碎裂成雪沫的瞬间。这种“单色系深浅变奏”正是江户浮世绘木版印刷美学的精髓。

### Palette 13 — Starry Night

#### 色彩哲学

梵高的《星月夜》并非印象派而是后印象派的极点：夜空以钴蓝与群青为骨，铬黄月光在蓝色重压下迸裂，柏树如黑色火焰直刺苍穹，村庄的暖黄则是唯一的人间余温。整组色板以三层蓝构成情绪纵深，用冷暖对抗驱动画面生命力。

#### 六色配色组

| 名称 | 英文 | RGB | 说明 |
|---|---|---|---|
| 月华铬黄 | Lumière Lunaire | `rgb(240,208,68)` | 月亮与星芒的爆裂光晕 |
| 村灯琥珀 | Lueurs du Village | `rgb(198,140,52)` | 村庄窗口透出的暖黄 |
| 晨曦苍蓝 | Aube Glacée | `rgb(105,155,200)` | 漩涡边缘的淡蓝过渡 |
| 星涡群青 | Tourbillon Outremer | `rgb(48,96,165)` | 漩涡主体的群青蓝 |
| 柏影墨绿 | Cyprès Nocturne | `rgb(22,50,30)` | 前景柏树的深邃暗绿 |
| 深夜钴蓝 | Minuit Cobalt | `rgb(20,36,88)` | 夜空最深处的底色 |

#### 完整色板

```text
Minuit Cobalt       rgb( 20,  36,  88)  ██  深锚·情绪底色·夜的重量
Tourbillon Outremer rgb( 48,  96, 165)  ██  主旋·漩涡·后印象笔触
Aube Glacée         rgb(105, 155, 200)  ██  过渡·呼吸·边界之光
Lumière Lunaire     rgb(240, 208,  68)  ██  爆点·月华·生命燃烧
Cyprès Nocturne     rgb( 22,  50,  30)  ██  沉默·柏树·拒绝被照亮
Lueurs du Village   rgb(198, 140,  52)  ██  余温·人间·唯一的暖
```

配色逻辑：三层蓝色构成由深至浅的情绪纵深轴。月华铬黄与村灯琥珀是画面仅有的两个暖色，一个属于宇宙、一个属于人间；柏影墨绿作为视觉锚点，以最暗的植物色把整组色的运动重新拉回大地。

### Palette 14 — A Thousand Li

#### 色彩哲学

《千里江山图》的颜色来自矿物颜料的层层积染：石青与石绿不一次着色，而是沉入绢底，形成“薄中见厚”的通透矿物感。整组色板围绕青绿主调、层次渐变、金赭点缀、空灵雅致与古绢质感展开。

#### 六色配色组

| 名称 | 英文 | RGB | 说明 |
|---|---|---|---|
| 古绢底 | Song Silk | `rgb(218,203,170)` | 千年绢素氧化后的暖米底色 |
| 天青·浅 | Sky Azurite | `rgb(110,165,195)` | 远山与江面折光的浅石青 |
| 赭金 | Ochre-Gold | `rgb(183,118,45)` | 礁石、屋舍与金线的温度色 |
| 苍绿·浅 | Pale Malachite | `rgb(96,148,110)` | 中景与云雾之间的过渡绿 |
| 石绿·正 | Malachite True | `rgb(48,105,76)` | 山体受光面的正孔雀石绿 |
| 石青·深 | Azurite Deep | `rgb(35,78,112)` | 山体阴面与水深处的矿蓝骨架 |

#### 完整色板

```text
霁山青  Azurite Deep    rgb( 35,  78, 112)  ██  骨·深邃·山之阴面
苍岭绿  Malachite True  rgb( 48, 105,  76)  ██  肉·华贵·山之受光
烟渚色  Sky Azurite     rgb(110, 165, 195)  ██  气·空灵·远山与水
岚霭绿  Pale Malachite  rgb( 96, 148, 110)  ██  韵·渐变·云雾中景
砂岩赭  Ochre-Gold      rgb(183, 118,  45)  ██  点·温度·金赭人迹
宋绢暖  Song Silk       rgb(218, 203, 170)  ░░  底·时间·千年绢素
```

五大特征的色彩映射：青绿主调由霁山青与苍岭绿共同锚定；层次渐变通过深青到浅青、正绿到浅绿的双链条完成；金赭点缀由砂岩赭承担温度调节；空灵雅致来自烟渚色与岚霭绿打开的呼吸感；古绢质感则由宋绢暖托起整组颜色的时间厚度。

### Palette 15 — And Quiet Flows the Don

#### 色彩哲学

这组配色拒绝一切鲜亮，只保留时间磨损之后的残余：不是蓝，是浊蓝；不是红，是暗血；不是黄，是枯苇；不是灰，是冻土与铅尘。它试图用“冷灰 + 土褐 + 暗血 + 浊蓝”压住史诗的沉重与苦难。

#### 六色配色组

| 名称 | 英文 | RGB | 说明 |
|---|---|---|---|
| 枯苇秋黄 | Полынь | `rgb(142,120,70)` | 被霜打过的苇草与苦艾的颜色 |
| 草原铅灰 | Степной Пепел | `rgb(110,108,104)` | 冬日荒原天地混为一色的灰 |
| 黄土大地 | Донская Земля | `rgb(118,86,52)` | 顿河流域栗钙土的褐色 |
| 铁锈赭红 | Ржавое Железо | `rgb(122,66,36)` | 军刀与枪托上的锈色 |
| 顿河浊蓝 | Мутный Дон | `rgb(52,70,90)` | 裹挟泥沙与血色的浊蓝河水 |
| 暗血战痕 | Запёкшаяся Кровь | `rgb(88,26,24)` | 凝固渗入军衣的深褐红 |

#### 完整色板

```text
Мутный Дон        顿河浊蓝  rgb( 52,  70,  90)  ██  冷·流动·命运底色
Степной Пепел     草原铅灰  rgb(110, 108, 104)  ██  重·静止·时间灰烬
Донская Земля     黄土大地  rgb(118,  86,  52)  ██  钝·厚重·苦难根基
Полынь            枯苇秋黄  rgb(142, 120,  70)  ██  涩·残存·短暂温柔
Ржавое Железо     铁锈赭红  rgb(122,  66,  36)  ██  锈·腐蚀·荣光衰败
Запёкшаяся Кровь  暗血战痕  rgb( 88,  26,  24)  ██  沉·凝固·史诗之重
```

色彩结构的悲剧逻辑：冷灰压顶，土褐承重，暗血锚底，铁锈贯穿时间感。整组色没有任何“希望色”，只有不同层级的磨损与沉郁。

### Palette 16 — Cyberpunk Edgerunners

#### 色彩哲学

《边缘行者》的视觉语言是一种过载美学：极暗底色与极亮荧光之间没有缓冲层。夜之城的霓虹不是繁荣而是麻醉，Lucy 的蓝是唯一的逃逸路径，黄色与绿色则是失控和运转的赛博症状。

#### 六色配色组

| 名称 | 英文 | RGB | 说明 |
|---|---|---|---|
| 迷幻荧黄 | Psycho Yellow | `rgb(225,255,8)` | 过载与赛博精神病的临界黄 |
| 电路荧绿 | Flatline Green | `rgb(10,238,100)` | 骇入代码流与改造体的运转色 |
| 霓虹品红 | Neon Magenta | `rgb(238,18,120)` | 酒吧、广告牌与欢场的霓虹色 |
| 鲜血赤红 | Edgerunner Red | `rgb(205,20,35)` | 边缘行者的代价之红 |
| 露娜深蓝 | Luna Blue | `rgb(15,32,98)` | Lucy、月球与梦的颜色 |
| 夜都虚空 | Night City Void | `rgb(14,8,28)` | 承载全部霓虹的深紫黑底 |

#### 完整色板

```text
Night City Void   夜都虚空  rgb( 14,   8,  28)  ██  底·深渊·过载的容器
Luna Blue         露娜深蓝  rgb( 15,  32,  98)  ██  沉·梦境·唯一的出口
Edgerunner Red    鲜血赤红  rgb(205,  20,  35)  ██  烈·代价·无处回避
Neon Magenta      霓虹品红  rgb(238,  18, 120)  ██  燥·谎言·城市的麻醉
Flatline Green    电路荧绿  rgb( 10, 238, 100)  ██  冷·运转·改造的代码
Psycho Yellow     迷幻荧黄  rgb(225, 255,   8)  ██  爆·失控·过载的临界
```

色彩结构的叙事逻辑：虚空压底，冷暖裂变，荧光过载，红色终章。没有黑暗，霓虹只是颜料；没有月球梦，夜之城就只剩噪声。

### Palette 17 — The Grand Budapest Hotel

#### 色彩哲学

这组配色像裹着柔光滤镜的旧欧洲童话：粉不是少女粉，而是旧玫瑰；紫不是妖艳紫，而是礼仪与人格；奶油底、复古暗金与雾蓝共同保证其明亮却不甜腻、优雅却不失时间感。

#### 六色配色组

| 名称 | 英文 | RGB | 说明 |
|---|---|---|---|
| 香草奶油 | Crème Vanille | `rgb(247,235,215)` | 饭店内壁与蛋糕胚的暖底色 |
| 阿尔卑斯雾蓝 | Brume Alpine | `rgb(168,178,196)` | 低饱和冷调，负责降温与透气 |
| 美酒蔷薇 | Rose Méndl | `rgb(237,148,158)` | 饭店外墙与甜品盒的标志旧玫瑰 |
| 古铜暗金 | Doré Antique | `rgb(176,136,60)` | 镜框、门把与制服肩章的旧贵族金 |
| 执行者紫 | Violet Concierge | `rgb(128,88,148)` | 古斯塔夫先生制服的权威紫 |
| 复古酒绛 | Bordeaux Vintage | `rgb(143,52,65)` | 图书馆、密谋与危险的暗影锚点 |

#### 完整色板

```text
Rose Méndl        美酒蔷薇     rgb(237, 148, 158)  ░░  主角·童话·旧玫瑰尘埃
Violet Concierge  执行者紫     rgb(128,  88, 148)  ██  人格·权威·荒诞尊严
Crème Vanille     香草奶油     rgb(247, 235, 215)  ░░  底气·呼吸·世界的空气
Doré Antique      古铜暗金     rgb(176, 136,  60)  ██  岁月·贵族·不肯褪去的光
Brume Alpine      阿尔卑斯雾蓝 rgb(168, 178, 196)  ░░  冷静·降温·现实的边缘
Bordeaux Vintage  复古酒绛     rgb(143,  52,  65)  ██  暗影·危险·令甜不腻的苦
```

五重美学法则的色彩映射：马卡龙柔色由蔷薇粉与执行者紫承担；奶油暖底由香草奶油统摄负空间；复古暗金负责贵族重量；雾蓝作为冷调调节器；酒绛则以一粒暗色防止整体沦为甜品陈列。

### Palette 18 — Renaissance Florence

#### 色彩哲学

佛罗伦萨的颜色不是被设计出来的，而是从矿石、金箔、陶土、木板和宗教空间中生长出来的。它们共同构成一种天然矿物色 + 暖金 + 陶土红 + 深褐墨绿 + 象牙白的古典秩序。

#### 六色配色组

| 名称 | 英文 | RGB | 说明 |
|---|---|---|---|
| 翡冷翠象牙 | Avorio Fiorentino | `rgb(238,228,208)` | 大理石与坦培拉底板的暖象牙 |
| 祭坛暖金 | Oro dell'Altare | `rgb(190,148,52)` | 背光金箔与旧贵族金饰的旧金 |
| 穹顶陶红 | Cotto Brunellesco | `rgb(172,84,50)` | 穹顶砖瓦与佛罗伦萨屋檐的陶土红 |
| 柏影墨绿 | Verde Cipresso | `rgb(54,80,60)` | 托斯卡纳柏树与铜绿的深绿 |
| 青金矿蓝 | Oltremare di Lapislazzuli | `rgb(46,70,118)` | 圣母袍服式的青金石蓝 |
| 胡桃深褐 | Noce Toscano | `rgb(85,54,34)` | 核桃木画板与阴影底釉的深褐 |

#### 完整色板

```text
Avorio Fiorentino     翡冷翠象牙  rgb(238, 228, 208)  ░░  底·呼吸·大理石与铅白
Oro dell'Altare       祭坛暖金    rgb(190, 148,  52)  ██  光·神圣·五百年旧金
Cotto Brunellesco     穹顶陶红    rgb(172,  84,  50)  ██  暖·人间·窑火与砖瓦
Oltremare             青金矿蓝    rgb( 46,  70, 118)  ██  重·肃穆·圣母的袍色
Verde Cipresso        柏影墨绿    rgb( 54,  80,  60)  ██  沉·自然·托斯卡纳丘陵
Noce Toscano          胡桃深褐    rgb( 85,  54,  34)  ██  根·人文·木质与大地
```

四重气质的色彩映射：青金矿蓝与祭坛暖金构成神圣庄重；象牙与陶红实现温润华贵；六色统一去现代化，形成古典醇厚；深绿与胡桃褐则把神圣重新拉回人的手艺与土地。

### Palette 19 — Soviet Avant-Garde

#### 色彩哲学

苏联先锋主义拒绝调和、拒绝渐变、拒绝装饰。每一种颜色都是硬边宣言：红色是行动，黑色是绝对，灰色是承重，蓝色是机械理性，赭黄是宣传中的未来，粗纸白则是大众传播的廉价载体。

#### 六色配色组

| 名称 | 英文 | RGB | 说明 |
|---|---|---|---|
| 粗纸白 | ГАЗЕТА | `rgb(225,218,205)` | 新闻纸白，粗粝、民主、反精英 |
| 宣传赭黄 | ПЛАКАТ | `rgb(200,150,32)` | 丰收海报里的赭黄承诺 |
| 混凝土灰 | БЕТОН | `rgb(118,114,108)` | 工业化进程的中性见证者 |
| 机械蓝 | ЧЕРТЁЖ | `rgb(50,80,138)` | 蓝图与纪律的冷蓝 |
| 列宁红 | КРАСНЫЙ | `rgb(196,28,28)` | 革命旗帜式的沉重红 |
| 铸铁黑 | ЧЁРНЫЙ | `rgb(24,20,18)` | 黑色方块般的绝对黑 |

#### 完整色板

```text
КРАСНЫЙ  列宁红    rgb(196,  28,  28)  ██  宣言·行动·革命的硬边
ЧЁРНЫЙ   铸铁黑    rgb( 24,  20,  18)  ██  绝对·虚无·零度的确定
БЕТОН    混凝土灰  rgb(118, 114, 108)  ██  工业·中性·进程的见证
ЧЕРТЁЖ   机械蓝    rgb( 50,  80, 138)  ██  精确·蓝图·冰冷的理想
ГАЗЕТА   粗纸白    rgb(225, 218, 205)  ░░  载体·大众·反精英的底色
ПЛАКАТ   宣传赭黄  rgb(200, 150,  32)  ██  丰收·乌托邦·未竟的承诺
```

六重美学法则的色彩映射：红黑强撞是结构核心；工业灰承担脊柱；机械蓝提供理性纪律；粗纸白强调大众传播属性；赭黄则把未来许诺压低到历史锈感之中。

### Palette 20 — Constantinople

#### 色彩哲学

君士坦丁堡的颜色必须同时属于希腊-罗马、波斯-伊斯兰、基督教与奥斯曼。金、蓝、紫、赭、象牙与暗绿在这里不是装饰，而是多文明叠压后的物质回声：穹顶金光、海峡深蓝、骨螺帝王紫、城墙赭土、大理石象牙和柏树深绿共同构成一座海都的神圣与世俗。

#### 六色配色组

| 名称 | 英文 | RGB | 说明 |
|---|---|---|---|
| 普罗科尼索象牙 | Λευκός · Fildişi | `rgb(236,225,207)` | 大理石地面的暖象牙底色 |
| 圣索菲亚金 | Χρυσός · Altın | `rgb(195,150,42)` | 烛烟熏染后的旧金 |
| 狄奥多西赭 | Ώχρα · Toprak | `rgb(170,112,50)` | 城墙与安纳托利亚土地的赭土色 |
| 柏树暗绿 | Κυπαρίσσι · Selvi | `rgb(50,76,58)` | 墓地、庭园与铜绿柱础的深绿 |
| 帝王骨螺紫 | Πορφύρα · Mor | `rgb(102,32,65)` | 权力与宗教之间的深红紫 |
| 博斯普鲁斯蓝 | Βόσπορος · Boğaz | `rgb(30,52,88)` | 海峡在傍晚收拢光线后的深沉蓝 |

#### 完整色板

```text
Χρυσός · Altın       圣索菲亚金      rgb(195, 150,  42)  ██  神圣·永恒·烛火之光
Βόσπορος · Boğaz     博斯普鲁斯蓝    rgb( 30,  52,  88)  ██  深渊·海都·文明交汇
Πορφύρα · Mor        帝王骨螺紫      rgb(102,  32,  65)  ██  权力·奢华·无价之色
Ώχρα · Toprak        狄奥多西赭      rgb(170, 112,  50)  ██  大地·坚守·城墙记忆
Λευκός · Fildişi     普罗科尼索象牙  rgb(236, 225, 207)  ░░  底色·理性·大理石呼吸
Κυπαρίσσι · Selvi    柏树暗绿        rgb( 50,  76,  58)  ██  永恒·死亡·两种信仰的凝视
```

文明交汇的色彩结构：东西冷暖轴由深蓝与赭土构成；神圣三角由金、紫、象牙构成；柏树暗绿则承担最长的历史纵深，使整组配色在华贵之外仍保有时间的阴影。

### Palette 21 — France

#### 色彩哲学

法兰西的颜色不是简单的红白蓝，而是一种“被文化重新训练过的红白蓝”。共和红需要有血与单宁的重量；白不是纯白，而是香槟象牙；蓝则带启蒙理性的深度。再辅以薰衣草、橄榄金与锌灰，整组色才能同时拥有浪漫、理性、贵族、土地与现代城市气质。

#### 六色配色组

| 名称 | 英文 | RGB | 说明 |
|---|---|---|---|
| 香槟象牙 | Ivoire Champagne | `rgb(232,222,205)` | 含时间杂质的“白” |
| 凡尔赛橄榄金 | Olive Dorée | `rgb(142,133,58)` | 法式园林式的古典金绿 |
| 巴黎锌灰 | Zinc Parisien | `rgb(122,126,132)` | 奥斯曼巴黎屋顶的冷灰 |
| 普罗旺斯薰衣草 | Lavande Provençale | `rgb(143,108,148)` | 南法暖紫 |
| 共和红 | Rouge Marianne | `rgb(180,32,40)` | 沉而有力的革命红 |
| 共和深蓝 | Bleu République | `rgb(44,74,138)` | 启蒙理性与国家权威之蓝 |

#### 完整色板

```text
Rouge Marianne      共和红         rgb(180,  32,  40)  ██  激情·革命·波尔多深处
Bleu République     共和深蓝       rgb( 44,  74, 138)  ██  理性·权威·启蒙的颜色
Ivoire Champagne    香槟象牙       rgb(232, 222, 205)  ░░  底气·时间·含杂质的纯粹
Lavande Provençale  普罗旺斯薰衣草 rgb(143, 108, 148)  ██  浪漫·土地·南北之间的裂缝
Olive Dorée         凡尔赛橄榄金   rgb(142, 133,  58)  ██  秩序·贵族·驯化的自然
Zinc Parisien       巴黎锌灰       rgb(122, 126, 132)  ██  克制·现代·奥斯曼的天际
```

法兰西精神的色彩结构：三色旗被重新解释为文化色而非政治符号；南法暖紫与巴黎锌灰构成南北气质裂缝；橄榄金与深蓝之间则潜伏着王权与共和的深层对立。

### Palette 22 — Kyoto

#### 色彩哲学

京都的颜色从不主动开口。绢白、樱灰粉、青竹灰、枯茶褐、苔绿与暗绀构成“六色底”，共同营造幽玄、柔雾、低饱和、留白克制的古都精神；而朱红只允许以极小面积出现，像茶室里唯一一枝有温度的花。

#### 六色配色组

| 名称 | 英文 | RGB | 说明 |
|---|---|---|---|
| 绢白 | Kinushiro | `rgb(234,226,212)` | 和纸与绢布的暖白留白 |
| 樱灰粉 | Sakura-nezumi | `rgb(204,184,178)` | 落樱覆石后的灰粉 |
| 青竹灰 | Aotake-nezumi | `rgb(116,126,120)` | 晨雾中竹节的冷暖平衡色 |
| 枯茶褐 | Karacha | `rgb(110,84,64)` | 百年杉木的侘び之褐 |
| 苔色 | Koke-iro | `rgb(80,94,68)` | 禅院石组底部的哑深绿 |
| 暗绀 | Kon | `rgb(34,40,66)` | 能剧与夜色的深靛蓝 |

#### 点睛色

| 名称 | 英文 | RGB | 说明 |
|---|---|---|---|
| 朱鸟居 | Shu-hi | `rgb(170,50,36)` | 极小面积使用的朱红点睛色 |

#### 完整色板

```text
絹白  Kinushiro    rgb(234, 226, 212)  ░░  底·呼吸·留白的物质
枯茶  Karacha      rgb(110,  84,  64)  ██  暖·侘び·百年杉木
桜鼠  Sakura-nez   rgb(204, 184, 178)  ░░  柔·物哀·落樱之灰
青竹鼠 Aotake-nez  rgb(116, 126, 120)  ██  冷·平衡·晨雾竹节
苔色  Koke-iro     rgb( 80,  94,  68)  ██  沉·时间·枯山水苔
紺    Kon          rgb( 34,  40,  66)  ██  深·冥想·能剧暗夜
─────────────────────────────────────────
朱緋  Shu-hi ·点睛 rgb(170,  50,  36)  ██  燃·鸟居·冷寂里的热
```

京都精神的色彩结构：留白为骨，冷暖天平靠青竹灰与枯茶褐维持，幽玄来自全部颜色去鲜亮后的柔雾感，而朱红作为唯一破局者，只能在最关键的点上出现。炸裂的红是装饰，克制的朱红才是京都。

### Palette 23 — Siamese Dream

#### 色彩哲学

《Siamese Dream》的封面本身就是一张配色宣言——两个女孩在柔焦的暖白光晕里相依，背景的深绿若隐若现，橙黄的光线像记忆里某个下午，美好得不真实。这不是摇滚专辑封面惯用的高对比冲击美学，而是一种刻意制造的梦境质感：过曝、柔化、带着胶片颗粒的温柔失真——如同 Corgan 把最原始的情感录进了最失真的吉他音墙里。

#### 六色配色组

| 名称 | 英文 | RGB | 说明 |
|---|---|---|---|
| 终章暖白 | Luna | `rgb(238,226,208)` | 封面光晕、专辑收束的余韵：胶片过曝后仍残留的人间温度 |
| 裸露灰紫 | Disarm | `rgb(182,180,193)` | Disarm 卸下所有失真时的颜色：玻璃碎裂前的透明与脆 |
| 可疑旧金 | Today | `rgb(198,158,65)` | Today 表层明媚旋律下的褪色金：美丽而不可信任 |
| 悬浮烟灰 | Hummer | `rgb(150,145,135)` | shoegaze 音墙堆叠出的失重悬浮：梦游者眼中的物质形态 |
| 低温烧橙 | Mayonaise | `rgb(188,105,40)` | 封面光源色、情感核心：积压已久的情绪在低温中缓慢焦化 |
| 深渊暗绿 | Soma | `rgb(42,68,48)` | 封面背景的深绿、九分钟史诗的坍塌：苔藓与腐叶共生的有机黑暗 |

#### 完整色板

```text
Luna       rgb(238, 226, 208)  ░░  终·暖白·胶片过曝后的人间温度
Disarm     rgb(182, 180, 193)  ░░  裸·灰紫·玻璃碎裂前的脆
Today      rgb(198, 158,  65)  ██  悖·旧金·美丽而不可信任
Hummer     rgb(150, 145, 135)  ██  漂·烟灰·梦游者的悬浮
Mayonaise  rgb(188, 105,  40)  ██  核·烧橙·低温焦化的情感
Soma       rgb( 42,  68,  48)  ██  深·暗绿·苔藓与腐叶的有机黑暗
```

Siamese Dream 的色彩结构是青春期情感的悖论：Luna 的暖白与 Hummer 的烟灰构成失焦层，把所有痛苦先过曝、再柔化；Today 的旧金与 Disarm 的灰紫是悖论的两极，用最美的容器装最重的内容；Mayonaise 的烧橙作为 primary 不是燃烧的红，而是已经燃烧过、被时间慢烤的橙；Soma 的暗绿作为最深色 `pal6`，是六色中唯一的“黑色替身”——不是纯黑，而是仍在生长的有机黑暗。整组配色全部退避鲜亮，因为这张专辑的情绪从不爆炸——它渗透。

---

## 可用环境

### 内容盒子

```latex
\begin{infobox}   ... \end{infobox}    % 蓝色调背景
\begin{warnbox}   ... \end{warnbox}    % 琥珀色调背景
\begin{resultbox} ... \end{resultbox}  % 配色 secondary 背景
\begin{goalbox}   ... \end{goalbox}    % 纯配色 primary 背景
```

### 定理类环境

```latex
\begin{De}{标题}{标签}  ... \end{De}   % 定义
\begin{The}{标题}{标签} ... \end{The}  % 定理
\begin{Pro}{标题}{标签} ... \end{Pro}  % 命题
\begin{Le}{标题}{标签}  ... \end{Le}   % 引理
\begin{Co}{标题}{标签}  ... \end{Co}   % 推论
\begin{Exa}{标题}{标签} ... \end{Exa}  % 例题
\begin{Rmk}{标题}{标签} ... \end{Rmk}  % 备注
```

### 证明与容器

```latex
\begin{Proof}  ... \end{Proof}   % 含 QED 符号的证明
\begin{Boxed}  ... \end{Boxed}   % 圆角灰色容器
```

### 章节引言面板

```latex
\begin{Intro}{标题}{正文}      \end{Intro}       % 标题在左上角
\begin{RightIntro}{标题}{正文} \end{RightIntro}  % 标题在右上角
```

### 行内辅助命令

```latex
\UnderlineBox{文字}              % 双线下划线块
\Quote{引文}{来源}               % 格式化引用
\Minipage{w1}{左列}{w2}{右列}    % 并排两列
\Eq{表达式}                      % 居中无编号公式
\EqL{表达式}{标签}               % 居中有编号公式
\EvOdd{行数}{宽度}{内容}          % 右侧绕排图
\textkai{中文楷体}                % 以内置楷体渲染文字
```

### 目录与页码进度环（v1.1+）

```latex
\section{Overview}        % 用标准的 \section{...} 划分章节
\section{Methods}
\section{Results}

\OUCTocFrame              % 渲染默认标题为 "Contents" 的目录帧
\OUCTocFrame[目录]         % 自定义帧标题
```

Section 条目以编号药丸徽标（配色 `primary`）+ 章节标题渲染；调用目录帧
时所在的当前 section 会自动高亮为 `accent` 色。

每个普通内容帧的页码右侧自动绘制一个小圆环进度条，灰色为轨道、`primary`
色弧线表示已完成进度，以 `\insertframenumber / \inserttotalframenumber`
为比例顺时针填充，方便听众实时感知讲解进度。该功能由样式自动开启，无需用户操作。

### 代码列表

含 `lstlisting` 的帧必须声明 `[fragile]`。  
若代码超过阈值行数（默认 20 行），加 `[allowframebreaks]` 可自动分页：

```latex
\begin{frame}[fragile,allowframebreaks]
    \frametitle{我的代码}
    \begin{lstlisting}[language=Matlab]
    % 代码写在这里
    \end{lstlisting}
\end{frame}
```

支持的语言关键字包括 `Matlab`、`Python`、`bash`、`[LaTeX]TeX`、`C`、`C++`、`Java` 以及 `listings` 宏包支持的所有语言。

---

## 版本历史

| 版本 | 日期 | 主要更新 |
|------|------|---------|
| **v1.2** | 2026-09 | 配色方案由 10 套扩充至 **24** 套（`\OUCSetPalette{0..23}`），整体取自 [Thomas-Tufte-Style-Book-Template](https://github.com/Hatsuyuki017/Thomas-Tufte-Style-Book-Template)，使幻灯片与配套书籍共用同一套色彩体系；新增 10–23 号配色（Roman Empire、Greece、Kanagawa、Starry Night、A Thousand Li、And Quiet Flows the Don、Cyberpunk Edgerunners、The Grand Budapest Hotel、Renaissance Florence、Soviet Avant-Garde、Constantinople、France、Kyoto、Siamese Dream）；新增主题点睛色 `spotcolor`（默认跟随 `accent`，22 号 Kyoto 下切换为朱绯）；README 配色章节整体替换为书籍模板的完整色版速查与配色详述附录。同时补齐并修复了 v1.1——发布的 `.sty` 实际上从未包含这些功能：实现了文档中已声明的 `\OUCTocFrame` 目录帧与页脚圆环进度条，并修复页脚线性进度条在首遍编译时超出 TeX dimen 上限的问题（`.aux` 生成前 `\inserttotalframenumber` 只是占位值），该问题会让从零开始的 `latexmk` 直接失败。24 页配色色板现独立为手册末尾的 **Palette Gallery** 一节，位于致谢之前；手册由 40 页增至 55 页。 |
| **v1.1** | 2026-05 | 新增 `\OUCTocFrame[标题]` 目录帧（编号药丸徽标、当前 section 自动以 `accent` 色高亮）；新增页码右侧圆环形进度条（`linegray` 轨道 + `primary` 色弧，从 12 点方向顺时针填充）；手册由 36 页扩展到 40 页，加入 TikZ 教程与目录演示页。 |
| **v1.0** | 2026-05 | 首次发布：10 套配色、定理类环境（`The`、`De`、`Exa`、`Rmk`、`Pro`、`Le`、`Co`、`Proof`、`Boxed`）、内容盒子（`infobox` / `warnbox` / `resultbox` / `goalbox`）、`\OUCTitleFrame` / `\OUCClosingFrame`、多语言 `lstlisting` 样式、底部线性进度条、调色板感知品牌色、调色板控制下的 TikZ 预载库。 |

> **升级说明（v1.1 → v1.2）：** 无破坏性变更。0–9 号配色的 RGB 值逐字节保持不变，原有幻灯片重编后颜色完全一致；10–23 号索引与 `spotcolor` 颜色名均为纯增量新增。
>
> **升级说明（v1.0 → v1.1）：** 无破坏性变更。原有幻灯片直接重编即可，圆环进度条会自动出现；若想启用新的目录帧，在内容中加入 `\section{...}` 标记并在 `\OUCTitleFrame` 之后调用一次 `\OUCTocFrame[目录]` 即可。

---

## 许可证

样式文件与示例文档以 **MIT 许可证**发布 — 可自由用于学术、个人和商业项目。  
内置字体遵从各自的许可证（详见字体文件）。  
OUC 徽标图片（`badge/ouc.png`、`badge/AUlightbadge.png`）归各自机构所有；在非 OUC 场景中使用本模板时，请替换为你自己的徽标。

---

## 致谢

本模板展开自开源 LaTeX 社区的贡献：

- **A Tufte-Style Book Template** 作者 **Kevin Godby** *等* — Overleaf 地址：  
  <https://www.overleaf.com/latex/templates/a-tufte-style-book-with-vdqi-title-and-contents-page/xqkjxvmrhmmp>  
  本模板中的定理类环境（`The`、`De`、`Exa`、`Rmk` …）、公式辅助命令（`\Eq`、`\EqL`）以及数学宏包组合均受该模板启发。

感谢 Kevin Godby 对 LaTeX 社区的开源贡献。

---

## 致谢

本模板展开自开源 LaTeX 社区的贡献：

- **A Tufte-Style Book Template** 作者 **Kevin Godby** *等* — Overleaf 地址：  
  <https://www.overleaf.com/latex/templates/a-tufte-style-book-with-vdqi-title-and-contents-page/xqkjxvmrhmmp>  
  本模板中的定理类环境（`The`、`De`、`Exa`、`Rmk` …）、公式辅助命令（`\Eq`、`\EqL`）以及数学宏包组合均受该模板启发。

感谢 Kevin Godby 对 LaTeX 社区的开源贡献。

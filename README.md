# OUC Smart Beamer Template

**English** | [中文](#ouc-smart-beamer-模板)

A polished XeLaTeX Beamer template for academic presentations.  
Features 10 built-in colour palettes, theorem-like environments, code listing styles, and a clean title/closing page — all encapsulated in a single `.sty` file.

> **Render preview** — compiled with palette 7 (Fresco Blue):
>
> *See `template-manual.pdf` for a full 27-page visual guide.*

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
7. [Colour Palettes](#colour-palettes)
8. [Available Environments](#available-environments)
9. [Licence](#licence)

---

## Folder Structure

```
beamertemplate/
├── oucsmartbeamer.sty        ← single style file; all template logic lives here
├── template-manual.tex       ← full user guide (compiles to 27-page PDF)
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
   \OUCSetPalette{7}   % 0–9, see Colour Palettes section
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
latexmk -xelatex template-manual.tex   # → template-manual.pdf (27 pages)
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

% ── Colour palette (0–9) ────────────────────────────────────────────
\OUCSetPalette{7}

% ── Code listing line-count warning threshold (default 20) ──────────
\OUCSetLstMaxLines{25}
```

---

## Colour Palettes

Call `\OUCSetPalette{N}` with N from 0 to 9.  
Each palette exposes six colours `oucpal1`…`oucpal6` (light → dark).

| N | Name | Primary (pal5) | Character |
|---|---|---|---|
| 0 | OUC Default | Navy blue (30, 58, 138) | Classic academic blue |
| 1 | Brunneophobia | Dark brown (86, 67, 53) | Warm earthy |
| 2 | Van Dyke | Indigo (68, 60, 94) | Muted purple |
| 3 | Back in Black | Charcoal (74, 63, 75) | Near-monochrome |
| 4 | Belle of the Ball | Olive (118, 118, 44) | Red-green contrast |
| 5 | Pine Tree | Burnt orange (167, 88, 26) | Warm autumn |
| 6 | Provence Blue | Slate blue (82, 92, 121) | Cool muted |
| 7 | Fresco Blue | Deep teal (4, 75, 102) | Clean blue-green |
| 8 | Monet | Dark teal (16, 86, 102) | Impressionist pastel |
| 9 | Narcissus | Rust (190, 108, 26) | Warm golden |

Slot semantics: `pal1` = code-block background · `pal2` = example/remark body · `pal4` = example/remark title · `pal5` = primary emphasis (frametitle, footer, theorem titles) · `pal6` = darkest accent (ad-hoc use).

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

## Licence

The style file and example documents are released under the **MIT Licence** — use freely in academic, personal, and commercial projects.  
Bundled fonts are subject to their own licences (see each font file for details).  
The OUC badge images (`badge/ouc.png`, `badge/AUlightbadge.png`) are copyright of their respective institutions; please replace them when using this template for non-OUC presentations.


---

# OUC Smart Beamer 模板

[English](#ouc-smart-beamer-template) | **中文**

一款精致的 XeLaTeX Beamer 学术演示模板。  
内置 10 套配色方案、定理类环境、代码高亮风格，以及干净的封面与收尾页——所有逻辑封装在单一 `.sty` 文件中。

> **效果预览** — 以配色方案 7（Fresco Blue）编译：
>
> *详见 `template-manual.pdf`，共 27 页完整使用手册。*

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
7. [配色方案](#配色方案)
8. [可用环境](#可用环境)
9. [许可证](#许可证)

---

## 文件夹结构

```
beamertemplate/
├── oucsmartbeamer.sty        ← 主样式文件，所有模板逻辑均在此
├── template-manual.tex       ← 完整用户手册（编译得到 27 页 PDF）
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
   \OUCSetPalette{7}   % 0–9，参见配色方案章节
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
latexmk -xelatex template-manual.tex   # → template-manual.pdf（27 页）
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

% ── 配色方案（0–9） ────────────────────────────────────────────────────
\OUCSetPalette{7}

% ── 代码块行数警告阈值（默认 20）────────────────────────────────────────
\OUCSetLstMaxLines{25}
```

---

## 配色方案

使用 `\OUCSetPalette{N}`，N 取 0 到 9。  
每套配色暴露六个颜色 `oucpal1`…`oucpal6`（由浅至深）。

| N | 名称 | 主色（pal5） | 风格 |
|---|---|---|---|
| 0 | OUC Default | 深蓝 (30, 58, 138) | 经典学术蓝 |
| 1 | Brunneophobia | 深褐 (86, 67, 53) | 暖土系 |
| 2 | Van Dyke | 靛蓝 (68, 60, 94) | 沉静紫 |
| 3 | Back in Black | 深灰 (74, 63, 75) | 近单色 |
| 4 | Belle of the Ball | 橄榄绿 (118, 118, 44) | 红绿对比 |
| 5 | Pine Tree | 赭褐 (167, 88, 26) | 暖秋色 |
| 6 | Provence Blue | 板岩蓝 (82, 92, 121) | 冷静沉稳 |
| 7 | Fresco Blue | 深青 (4, 75, 102) | 干净蓝绿 |
| 8 | Monet | 深青 (16, 86, 102) | 印象派柔色 |
| 9 | Narcissus | 铁锈橘 (190, 108, 26) | 暖金系 |

颜色槽语义：`pal1` = 代码块背景 · `pal2` = 例题/备注正文背景 · `pal4` = 例题/备注标题背景 · `pal5` = 主强调色（页眉、页脚、定理标题） · `pal6` = 最深色（自由使用）。

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

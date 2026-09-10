# Alice 系列（magic-doll-vibe）

一个以 **AliceBlue** 家族为底，**90% 为 Vibe coding 生成**的终端/编辑器配色系列，覆盖 9 个平台，各平台保持同一套调色板与视觉语言。

仅自用，不喜勿喷！

| 主题 | 底色 | 基调 |
|---|---|---|
| **Alice Sunny** | `#f0f8ff`（AliceBlue） | 浅色 · 明亮 · 柔和 |
| **Alice Rainy** | `#1f252a` | 深色 · 冷灰蓝 · 低饱和（阴雨感） |
| **Alice Nightly** | `#090e12` | 深色 · 近纯黑 · 高对比（深夜感） |

三个主题共享同一组**强调色**：`acc1 = #56a0d1`、`acc2 = #5b7f92` 逐字节一致；`acc3` 浅色版为 `#8868ae`，深色版统一提亮到 `#a280cb`（只做文字色、不影响色块）。

## 设计思路

- **亮度锚点**：浅色版以 `bg1`（L≈0.975）和 `acc1`（L≈0.678）为基准；深色版整体反转——bg 落在 L 0.13–0.26、文字档 L 0.70–0.75、彩底用浅字（`txt2`）。代码前景色对 bg1 对比度 Rainy ≥4.7、Nightly ≥4.5。
- **同色系压深**：所有颜色只调整明度/饱和度、不动色相——蓝（240°）、紫（304°）、绿（169°）、金（78°）、玫瑰（353°）五大色相家族贯穿全部主题与平台。
- **墨字/浅字铺彩底**：浅色版彩色块用深墨字 `#1f2f3a`；深色版反过来用浅字 `txt2`（acc2 底 + 白字 4.29）。
- **light-\* 两套约定**：浅色主题里 ANSI bright 靠"更饱和"强调（更浅会隐形）；深色主题回归常规"更亮"。
- **彩虹括号**：六层嵌套按 蓝→紫→绿→金→玫瑰→注释 循环（全平台统一）。

## 调色板

### 基础

| token | hex | OKLCH | 用途 |
|---|---|---|---|
| `bg1` | `#f0f8ff` | 0.975 0.013 244° | 编辑器背景（AliceBlue） |
| `bg2` | `#dae2e9` | 0.909 0.013 244° | 面板 / 光标行 / 弹窗 |
| `txt1` | `#3b3b3b` | 0.352 0.000 90° | 正文 |
| `txt2` | `#1f2f3a` | 0.296 0.029 239° | 彩色块上的墨字 |

### 强调色

| token | hex | OKLCH | 用途 | 对 bg1 对比度 |
|---|---|---|---|---|
| `acc1` | `#56a0d1` | 0.678 0.104 240° | 类型 / 光标 / 当前行号 / 主强调 | 2.67 |
| `acc2` | `#5b7f92` | 0.577 0.050 232° | 变量 / 函数 / 选区 / hint | 4.00 |
| `acc3` | `#8868ae` | 0.577 0.110 304° | 关键字 / 常量 / 标签 | 4.22 |
| `str` | `#4f7a6a` | 0.543 0.054 169° | 字符串 / info | 4.53 |
| `num` | `#a57a2e` | 0.608 0.106 78° | 数字 | 3.61 |
| `comm` | `#787878` | 0.573 0.000 90° | 注释 / 行号 | 4.12 |
| `warn` | `#b58532` | 0.649 0.114 78° | 警告（比 num 略暖亮） | 3.08 |
| `err` | `#a56a83` | 0.595 0.082 353° | 错误 / diff.minus | 3.92 |

### 终端 16 色（基色 + vivid bright）

| 色 | base | bright (`light-*`) |
|---|---|---|
| black | `#1f2f3a` | `#2E4250` |
| red | `#C998AE` | `#DC8AB1` |
| green | `#7FAD9C` | `#59B698` |
| yellow | `#CFB886` | `#D8B260` |
| blue | `#56A0D1` | `#2EA2E5` |
| magenta | `#CBA0E3` | `#CC97F3` |
| cyan | `#789eb1` | `#56A3C4` |
| gray/white | `#a8b4c0` | `#BAC6D1` |

bright 与基色**同明度、高饱和**；WezTerm/Zed 的 dim 档为 OKLCH L−0.06 的衍生色。

## 目录结构

按平台分目录，主题文件统一命名 `alice-sunny` / `alice-rainy` / `alice-nightly`：

```
magic-doll-vibe/
├── helix/
│   ├── alice-sunny.toml
│   ├── alice-rainy.toml
│   ├── alice-nightly.toml
│   └── legacy/alice-sunny-v1.toml     # 初版留档（旧调色板，勿用）
├── wezterm/
│   ├── alice-sunny.toml
│   ├── alice-rainy.toml
│   └── alice-nightly.toml
├── zellij/
│   ├── alice-sunny.kdl
│   ├── alice-rainy.kdl
│   └── alice-nightly.kdl
├── zed/
│   ├── alice-sunny.json
│   ├── alice-rainy.json
│   └── alice-nightly.json
├── vscode/
│   ├── alice-sunny/                   # VS Code 扩展（可直接安装）
│   ├── alice-rainy/
│   └── alice-nightly/
├── opencode/
│   ├── alice-sunny.json
│   ├── alice-rainy.json
│   └── alice-nightly.json
├── claude/
│   ├── alice-sunny.json
│   ├── alice-rainy.json
│   └── alice-nightly.json
├── jetbrains/
│   ├── alice-sunny.icls
│   ├── alice-rainy.icls
│   └── alice-nightly.icls
└── vim/                               # Vim 与 Neovim 通用
    ├── colors/alice-{sunny,rainy,nightly}.vim
    └── lua/lualine/themes/alice-{sunny,rainy,nightly}.lua
```

## 深色主题

Alice Rainy 与 Alice Nightly 共享深色设计，仅明度/饱和度不同：

| | Rainy（冷灰蓝 · 柔和） | Nightly（深蓝黑 · 高对比） |
|---|---|---|
| bg1 / bg2 | `#1f252a` / `#30363c` | `#090e12` / `#161b20` |
| txt1 / txt2 | `#ccd2d7` / `#eef2f6` | `#e0e5ea` / `#f6f9fb` |
| str | `#65b095` | `#50bf9b` |
| num | `#bfa065` | `#d2a652` |
| comm | `#8f9396` | `#8f9396` |
| warn | `#c49a55` | `#d7a03d` |
| err | `#ba829a` | `#cf84a5` |
| acc1 / acc2 / acc3 | `#56a0d1` / `#5b7f92` / `#a280cb` | 同左 |

深色下选区/光标/状态栏走"彩底 + 浅字"；ANSI bright 采用常规"更亮"约定。Rainy 偏低饱和阴天观感，Nightly 偏深黑高对比。

---

## 安装

下文每个平台都给出 **macOS / Linux** 与 **Windows (PowerShell)** 两种方式。`<repo>` 指本仓库克隆/解压后的根目录。

```bash
git clone https://github.com/reiAkwa/magic-doll-vibe.git
```

### Helix

主题名 = 文件名（去 `.toml`），即 `alice-sunny` / `alice-rainy` / `alice-nightly`。

```bash
# macOS / Linux
mkdir -p ~/.config/helix/themes
cp <repo>/helix/*.toml ~/.config/helix/themes/
```
```powershell
# Windows
New-Item -ItemType Directory -Force "$env:APPDATA\helix\themes" | Out-Null
Copy-Item <repo>\helix\*.toml "$env:APPDATA\helix\themes\"
```

`~/.config/helix/config.toml`（Windows 为 `%APPDATA%\helix\config.toml`）：

```toml
theme = "alice-sunny"      # 或 alice-rainy / alice-nightly

[editor]
cursorline = true          # 可选：光标行底色
rainbow-brackets = true    # 可选：彩虹括号
```

### WezTerm

把 `wezterm/` 目录直接加进搜索路径（无需复制）：

```lua
-- ~/.config/wezterm/wezterm.lua  (Windows: %USERPROFILE%\.config\wezterm\wezterm.lua)
local wezterm = require 'wezterm'
local config = {}

config.color_scheme_dirs = { '<repo>/wezterm' }   -- Windows 用正斜杠，如 'C:/path/to/magic-doll-vibe/wezterm'
config.color_scheme = 'alice-sunny'               -- 或 alice-rainy / alice-nightly

return config
```

或复制进全局配色目录：

```bash
mkdir -p ~/.config/wezterm/colors && cp <repo>/wezterm/*.toml ~/.config/wezterm/colors/
```
```powershell
New-Item -ItemType Directory -Force "$env:USERPROFILE\.config\wezterm\colors" | Out-Null
Copy-Item <repo>\wezterm\*.toml "$env:USERPROFILE\.config\wezterm\colors\"
```

### Zellij

主题名 = 文件名（去 `.kdl`），即 `alice-sunny` / `alice-rainy` / `alice-nightly`。

```bash
# macOS / Linux
mkdir -p ~/.config/zellij/themes
cp <repo>/zellij/*.kdl ~/.config/zellij/themes/
```
```powershell
# Windows
New-Item -ItemType Directory -Force "$env:USERPROFILE\.config\zellij\themes" | Out-Null
Copy-Item <repo>\zellij\*.kdl "$env:USERPROFILE\.config\zellij\themes\"
```

`~/.config/zellij/config.kdl`（Windows 为 `%USERPROFILE%\.config\zellij\config.kdl`）：

```kdl
theme "alice-sunny"      // 或 alice-rainy / alice-nightly
```

Zellij 会自动读取 themes 目录下的 `.kdl`；也可直接把 `themes { ... }` 内容并入 `config.kdl`。

### Zed

```bash
mkdir -p ~/.config/zed/themes && cp <repo>/zed/*.json ~/.config/zed/themes/
```
```powershell
New-Item -ItemType Directory -Force "$env:USERPROFILE\.config\zed\themes" | Out-Null
Copy-Item <repo>\zed\*.json "$env:USERPROFILE\.config\zed\themes\"
```

然后 `Ctrl+Shift+P` → `theme selector` → **Alice Sunny / Alice Rainy / Alice Nightly**（主题名来自 JSON 内部 `name`，与文件名无关）。

### VS Code

`vscode/` 下是三个可直接安装的扩展。任选一种：

```bash
# 方式 A：本地安装（推荐，跨平台）
code --install-extension <repo>/vscode/alice-sunny          # 也可指向 alice-rainy / alice-nightly
# 或在 VS Code 里 Ctrl+Shift+P → "Developer: Install Extension from Location..." 选择对应文件夹
```
```powershell
code --install-extension <repo>\vscode\alice-sunny
```

```bash
# 方式 B：打包成 VSIX
cd <repo>/vscode/alice-sunny
npx @vscode/vsce package
code --install-extension alice-sunny-1.0.0.vsix
```

安装后 `Ctrl+K Ctrl+T` → **Alice Sunny / Rainy / Nightly**。

### OpenCode

主题名 = 文件名（去 `.json`）。

```bash
mkdir -p ~/.config/opencode/themes && cp <repo>/opencode/*.json ~/.config/opencode/themes/
```
```powershell
New-Item -ItemType Directory -Force "$env:USERPROFILE\.config\opencode\themes" | Out-Null
Copy-Item <repo>\opencode\*.json "$env:USERPROFILE\.config\opencode\themes\"
```

TUI 里 `/theme` 选择，或在 `opencode.json` / `tui.json` 写 `"theme": "alice-sunny"`。

### Claude Code

需要 v2.1.118+。文件名（去 `.json`）= 主题 slug。

```bash
mkdir -p ~/.claude/themes && cp <repo>/claude/*.json ~/.claude/themes/
```
```powershell
New-Item -ItemType Directory -Force "$env:USERPROFILE\.claude\themes" | Out-Null
Copy-Item <repo>\claude\*.json "$env:USERPROFILE\.claude\themes\"
```

`/theme` → **Alice Sunny / Rainy / Nightly**（文件热重载）。注意 Claude Code 不绘制终端背景，建议搭配 WezTerm 版一起用才是完整观感。Sunny 的 `base` 为 `light`，Rainy/Nightly 为 `dark`。

### JetBrains

Settings → Editor → Color Scheme → ⚙ → **Import Scheme** → 选择 `<repo>/jetbrains/alice-sunny.icls`（或 `alice-rainy.icls` / `alice-nightly.icls`）。

`.icls` 继承 IDE 默认方案（Sunny 继承 `Default`，深色继承 `Darcula`），只覆盖编辑器、控制台 ANSI、诊断波浪线、括号匹配等，UI 框架保持系统默认。

### Vim / Neovim

Vimscript 经典 colorscheme，Vim 与 Neovim 通用，真彩 + 自动 256 色回退。colorscheme 名 = 文件名（去 `.vim`）。

```bash
# Vim — macOS / Linux
mkdir -p ~/.vim/colors ~/.vim/lua/lualine/themes
cp <repo>/vim/colors/*.vim ~/.vim/colors/
cp <repo>/vim/lua/lualine/themes/*.lua ~/.vim/lua/lualine/themes/

# Neovim — macOS / Linux
mkdir -p ~/.config/nvim/colors ~/.config/nvim/lua/lualine/themes
cp <repo>/vim/colors/*.vim ~/.config/nvim/colors/
cp <repo>/vim/lua/lualine/themes/*.lua ~/.config/nvim/lua/lualine/themes/
```
```powershell
# Vim — Windows
New-Item -ItemType Directory -Force "$env:USERPROFILE\.vim\colors" | Out-Null
Copy-Item <repo>\vim\colors\*.vim "$env:USERPROFILE\.vim\colors\"

# Neovim — Windows
New-Item -ItemType Directory -Force "$env:LOCALAPPDATA\nvim\colors" | Out-Null
Copy-Item <repo>\vim\colors\*.vim "$env:LOCALAPPDATA\nvim\colors\"
```

启用：

```vim
colorscheme alice-sunny    " 或 alice-rainy / alice-nightly
```

自动设置 `background`（Sunny=light，Rainy/Nightly=dark）与终端 ANSI（`g:terminal_color_0..15`）；内置 Treesitter 组链接、诊断高亮、`@rainbow.level1–6` 彩虹括号（配合 rainbow-delimiters.nvim）。

**内置插件高亮**（约 300 组）：telescope、nvim-tree、neo-tree、which-key、gitsigns、indent-blankline（v2+v3）、lazy.nvim、mason、nvim-notify、trouble、dashboard/alpha、bufferline、nvim-cmp、blink.cmp（含 25 种 Kind）、dropbar.nvim（含 WinBar）、flash、hop、leap、mini.*、barbecue/navic、nvim-scrollbar 等。

**lualine**：主题文件随包附带，随 colors 一起放进 `lua/lualine/themes/` 后：

```lua
require('lualine').setup({ options = { theme = 'alice-sunny' } })  -- 或 alice-rainy / alice-nightly
```

模式色沿用 Helix 状态栏约定：normal=蓝(acc1)、insert=红、visual=紫、replace=金、command=青、terminal=绿。

## 平台间对应关系

| 角色 | Helix | WezTerm | Zellij | Zed | VS Code | OpenCode | Claude Code | JetBrains | Vim/Neovim |
|---|---|---|---|---|---|---|---|---|---|
| 背景 / 正文 | bg1 / txt1 | background / foreground | text_unselected | editor.background / editor.foreground | editor.background / editor.foreground | background / text | text（背景由终端负责） | DEFAULT_TEXT | Normal |
| 光标 | acc1 实底 | cursor_bg | — | players[0].cursor | editorCursor.foreground | primary | claude | CARET_COLOR | Cursor |
| 选区 | acc2 实底 | selection_bg | text_selected | players[0].selection | editor.selectionBackground | backgroundElement | selectionBg | SELECTION_BACKGROUND | Visual |
| 光标行 | cursorline | — | — | editor.active_line.background | editor.lineHighlightBackground | — | — | CARET_ROW_COLOR | CursorLine |
| 彩虹括号 | `rainbow` 数组 | ansi | — | editor.document_highlight.bracket_background | editorBracketHighlight.foreground1–6 | syntaxPunctuation | rainbow_* | MATCHED_BRACE_ATTRIBUTES* | @rainbow.level1–6 |
| 搜索命中 | ui.highlight（黄底） | — | — | search.match_background | editor.findMatchHighlightBackground | textHighlighted | selectionBg | SEARCH_RESULT_ATTRIBUTES | Search / IncSearch |
| 状态栏 | acc2 底 + 浅字 | — | ribbon_selected / frame_selected | statusBar.background | statusBar.background | primary | claude | — | StatusLine |
| 终端 16 色 | — | ansi / brights | — | terminal.ansi.* | terminal.ansi* | — | — | CONSOLE_*_OUTPUT | g:terminal_color_0–15 |

全平台统一约定：**光标 = acc1 实底**、**选区 = acc2 实底**、**彩虹第 6 级 = 注释色**。

\* JetBrains 彩虹括号为单色括号 + 匹配块高亮，多级彩虹依赖 IDE 内置功能。

## 备注

- 所有派生色（hover/active/border/dim/半透明底）均由 OKLCH 计算，改基色后可整组重推。
- `num` 与 `warn` 有意做了微差（暖度 + 明度），诊断色不再和数字完全撞色。
- VS Code 的运算符强制正体（规则置于 tokenColors 末位并配 semanticTokenColors），不受关键字斜体影响。
- `helix/legacy/alice-sunny-v1.toml` 为最初版本，使用旧调色板，仅供留档，请勿使用。

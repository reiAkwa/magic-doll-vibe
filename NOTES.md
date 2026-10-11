# 重写待办（复查记录）

推翻重写前的一次全仓库体检记录，供新版对照。README 里写错的地方已经修正，这里是**代码层面**仍需处理的点，按类别列出，附实测数值与文件位置。

> 校验口径：对比度 = WCAG 对比度（sRGB 相对亮度）；L / C / ΔL = OKLCH。数值均可用脚本复算。

---

## A. 配色 / 可读性（要在新调色板里解决）

1. **Rainy 的 `acc2` 对比度不足**
   `#5b7f92` 对 Rainy `bg1 #1f252a` 只有 **3.61**（< AA 4.5）。而 `acc2` 是 `variable` / `function` / `constructor` 的主力色（`helix/alice-rainy.toml:95-100`）。Nightly 为 4.52，勉强压线。
2. **选区（`acc2` 底 + `txt2`）文字对比度偏低**
   Sunny **3.21** / Rainy **3.81** / Nightly **4.06**。注意：README 曾写的“4.29”是**纯白** `#ffffff` 对 `acc2` 的值，不是实际文字色 `txt2`。
3. **OpenCode 搜索命中几乎不可见**
   `opencode/*.json` 的 `textHighlighted` = `bg2`，Sunny 对 bg1 对比度仅 **1.22**；其它平台搜索命中都是金/黄底（Helix `yellow`、VS Code `#CFB886`）。
4. **Helix 引用了未定义的调色板名 `black`**
   三份 `helix/alice-*.toml` 的 `[palette]` 都没有 `black` / `white`，但 `diagnostic.*` 用了 `fg = "black"`（sunny:78-82、rainy:79-83、nightly:79-83），Rainy/Nightly 的 `ui.highlight` 也用了。Helix 的默认 palette 会把 `black` 落到**终端 ANSI 0**，即颜色随用户终端配置变化，与文档承诺的“墨字 `#1f2f3a` / 浅字 `txt2`”都不是一回事。另外三主题诊断实际都是“黑字铺彩底”，与 README 描述的深浅两套铺彩底约定不符。
5. **浅色版高亮子本身偏淡**
   Sunny `ui.highlight` 底 `yellow #CFB886` 对 `bg1` 仅 **1.8**（文字 `txt1` 对 `yellow` 5.79，可读，但色块不显眼）。可考虑更高饱和/更高对比的搜索底色。

## B. 平台一致性（建议用统一定义重推）

6. **OpenCode 的选区不是 `acc2`**
   用的是 `backgroundElement`（Sunny `#d3dbe2`）。Helix / Zed / VS Code / Zellij / Claude Code 都是 `acc2` 实底。
7. **Zed 没有彩虹括号**
   只有单色括号匹配底色 `editor.document_highlight.bracket_background`（Sunny `#7FAD9C40`）。JetBrains 同样只有单色括号 + 匹配块高亮。真正的 6 级彩虹只有 Helix / VS Code / Claude Code / Vim·Neovim。
8. **Helix 的 select 模式状态栏是绿色**
   `ui.statusline.select = green`（sunny:42），而 lualine 的 visual 是紫（`acc3`）。跨平台模式色不统一；Helix 只有 normal/insert/select 三档。
9. **Helix `ui.selection.primary` 在 Sunny 缺 `fg`**
   `helix/alice-sunny.toml:15` 只有 `bg`；Rainy/Nightly 都有 `fg = "txt2"`。
10. **WezTerm 的 256 色表基本与本系列无关**
    `wezterm/*.toml` 的 `[colors.indexed]` 中，**索引 17–231 三个主题逐字节完全相同**（通用 xterm 256 色），只有 16 和 232–255 灰阶随主题变化。若在意 256 色模式，需要重新生成。
11. **`black` / `white` 未在 palette 定义**
    同 A-4；若依赖终端默认色，主题就不自洽。

## C. 元数据 / 结构

12. **占位符未替换**：`zed/*.json` 的 `"author": "theme-new"`、`vscode/*/package.json` 的 `"publisher": "theme-new"`；Helix 主题干脆没有 author 字段。仓库实为 `reiAkwa/magic-doll-vibe`。
13. **目录名不一致**：文档 / 仓库名是 `magic-doll-vibe`，本地检出目录是 `theme-new`。
14. **Helix 的 dim 档没做**：三份主题（含 legacy）末尾都留着 `# TODO: dim colors`。

## D. 已修正的 README 谎言（对照用）

- 亮度锚点“bg L 0.13–0.26 / 文字档 L 0.70–0.75” → 实为 bg **0.16–0.33**、文字档 **0.86–0.98**。
- “Rainy ≥4.7” → 实为 Rainy `acc2` = 3.61。
- “acc2 底 + 白字 4.29” → 实为 3.21 / 3.81 / 4.06。
- “bright 同明度” → 仅 6 个彩色档成立，`black`（ΔL +0.072）/`gray`（+0.056）会变亮。
- “dim = L−0.06（WezTerm/Zed）” → dim 只有 Zed 有，且 `dim_black` 是**提亮**（+0.063）。
- “彩虹括号全平台统一” → Zed / JetBrains 不成立。
- “选区 = acc2 实底（全局）” → OpenCode 例外。
- “模式色沿用 Helix 状态栏约定” → Helix 只有三档，select 是绿。

---

## 附：实测数值（OKLCH L）

| | bg1 | bg2 | txt1 | txt2 |
|---|---|---|---|---|
| Sunny | 0.975 | 0.909 | 0.352 | 0.296 |
| Rainy | 0.261 | 0.330 | 0.861 | 0.959 |
| Nightly | 0.160 | 0.219 | 0.920 | 0.980 |

Sunny 调色板对 bg1 `#f0f8ff` 的对比度（README 原表，已逐项复核无误）：
`acc1` 2.67 · `acc2` 4.00 · `acc3` 4.22 · `str` 4.53 · `num` 3.61 · `comm` 4.12 · `warn` 3.08 · `err` 3.92。

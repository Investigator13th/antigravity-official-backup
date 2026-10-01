---
version: 1.0.0-antigravity
name: Google-Antigravity-Design-System
description: The official visual identity and interface specification of Google Antigravity. A zero-gravity, high-precision tech-humanist design system defined by Google Sans Flex variable typography, a disciplined 13-step slate-grey monochromatic palette with Google electric accents, 36px macro-radii, 9999px pill controls, optical backdrop blurs, and magnetic floating cursor interactions. Engineered for high-signal, cross-agent consistency in AI-assisted frontend generation.

# ==============================================================================
# 01. MACHINE-READABLE DESIGN TOKENS (YAML SPECIFICATION)
# ==============================================================================
colors:
  # 品牌核心与交互墨水 (Action & Text Inks)
  primary: "#121317"                  # 纯黑炭墨 (Primary CTA 背景、核心文字与强调锚点)
  primary-hover: "#2f3034"            # 深灰悬停态 (Button Hover)
  primary-pressed: "rgba(230, 234, 240, 0.12)" # 按下反馈态
  primary-disabled: "#f8f9fc"         # 主按钮禁用底
  on-primary: "#ffffff"               # 主按钮文字色 (纯白，对比度 18.2:1)
  on-disabled: "#6a6a71"              # 禁用态文本颜色

  # 经典科技点缀色 (Google Brand Accents)
  accent-blue: "#3279f9"              # 核心聚焦与交互链接蓝 (Google Blue 600)
  accent-blue-hover: "#1557b0"        # 链接悬停深蓝
  accent-blue-container: "#e8f0fe"    # 浅通透蓝信息底 (Announcement / Tag)
  accent-blue-border: "rgba(50, 121, 249, 0.2)" # 蓝系强调细描边
  
  # 画布与多层容器表面 (Surfaces & Container Elevation)
  canvas: "#ffffff"                   # 纯白画布底色 (Light Canvas Base)
  surface: "#ffffff"                  # 默认浮层表面
  surface-container-low: "rgba(0, 0, 0, 0.02)" # 极浅底色分割 / 斑马纹
  surface-container: "#f8f9fc"        # 浅冷白灰底色 (Grey 10 · 卡片、轮播底、次级容器)
  surface-container-high: "#eff2f7"   # 中浅灰底 (Grey 20 · 悬停高亮、导航药丸底)
  surface-container-higher: "#e6eaf0" # 进阶浅灰 (Grey 50 · 下拉分割线、内嵌槽)
  surface-container-highest: "#e1e6ec"# 结构强调浅灰 (Grey 100)

  # 暗夜沉浸表面 (Inverse Surfaces · 专用于落地页底部 Download 沉浸黑卡)
  surface-inverse: "#121317"          # 极黑底板 (Grey 1200 · 空间悬浮感黑卡底)
  on-surface-inverse: "#f8f9fc"       # 黑底主要标题与文字 (Grey 10)
  on-surface-inverse-variant: "#b2bbc5" # 黑底副标题与辅助说明 (Grey 300)

  # 墨水与层级文字 (Typography Inks & Readability)
  ink: "#121317"                      # 一级文字 / 核心标题 (深邃炭黑，对纯白对比度 18.2:1)
  body: "#121317"                     # 正文阅读文字
  muted: "#45474d"                    # 二级正文 / 辅助副标题 (Grey 800，对比度 9.5:1)
  muted-soft: "#6a6a71"               # 三级微注 / 禁用与时间戳 (Grey 50-20)
  divider: "rgba(33, 34, 38, 0.06)"   # 结构分隔细线

  # 激光手术刀级描边 (Outlines & Borders)
  outline: "rgba(33, 34, 38, 0.12)"   # 标准 1px 容器描边 (12% 炭黑)
  outline-variant: "rgba(33, 34, 38, 0.06)" # 次级超轻微描边 (6% 炭黑，极简通透)
  outline-focus: "rgba(50, 121, 249, 0.4)" # 键盘与无障碍聚焦光环
  inverse-outline: "rgba(230, 234, 240, 0.12)" # 逆向深底容器描边
  inverse-outline-variant: "rgba(230, 234, 240, 0.06)" # 逆向深底极细描边

  # 毛玻璃与高斯透明通道 (Backdrop Overlays)
  overlay-nav: "rgba(255, 255, 255, 0.85)" # 导航栏透光磨砂 (85% 白 + 5px Blur)
  overlay-card: "rgba(255, 255, 255, 0.95)" # 悬浮右键菜单底 (95% 白 + 16px Blur)
  overlay-button-secondary: "rgba(183, 191, 217, 0.1)" # 次要按钮通透微冷紫灰
  overlay-button-secondary-hover: "#f0f1f5" # 次要按钮悬停态
  overlay-video-control: "rgba(0, 0, 0, 0.3)" # 视频控件半透深黑圆钮

typography:
  font-family-sans: '"Google Sans Flex", "Google Sans", -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, "PingFang SC", "Microsoft YaHei", sans-serif'
  font-family-mono: '"Google Sans Code", Consolas, Menlo, Monaco, monospace'
  font-family-icon: '"Google Symbols", sans-serif'

  # 展示层级 (Display & Hero Scales · 针对大视口建立的巨型物理张力)
  display-hero:
    fontFamily: "{typography.font-family-sans}"
    fontSize: 107px
    lineHeight: 1.0
    letterSpacing: -2.14px
    fontWeight: 450
    fontVariationSettings: '"wdth" 100, "opsz" 144'
    usage: "首屏主视觉核心 Slogan (大桌面)"
  display-9xl:
    fontFamily: "{typography.font-family-sans}"
    fontSize: 148px
    lineHeight: 0.98
    letterSpacing: -2.96px
    fontWeight: 450
    fontVariationSettings: '"wdth" 100, "opsz" 144'
  display-8xl:
    fontFamily: "{typography.font-family-sans}"
    fontSize: 124px
    lineHeight: 0.98
    letterSpacing: -2.48px
    fontWeight: 450
    fontVariationSettings: '"wdth" 100, "opsz" 124'
  display-7xl:
    fontFamily: "{typography.font-family-sans}"
    fontSize: 98px
    lineHeight: 0.84
    letterSpacing: -1.8px
    fontWeight: 450
    fontVariationSettings: '"wdth" 100, "opsz" 98'
  display-6xl:
    fontFamily: "{typography.font-family-sans}"
    fontSize: 72px
    lineHeight: 1.0
    letterSpacing: -1.44px
    fontWeight: 450
    fontVariationSettings: '"wdth" 100, "opsz" 72'
  display-5xl:
    fontFamily: "{typography.font-family-sans}"
    fontSize: 54px
    lineHeight: 1.04
    letterSpacing: -0.95px
    fontWeight: 450
    fontVariationSettings: '"wdth" 100, "opsz" 54'
    usage: "模块核心统领一级标题 (Section Heading)"

  # 结构层级 (Headings & Titles)
  heading-4xl:
    fontFamily: "{typography.font-family-sans}"
    fontSize: 42px
    lineHeight: 1.04
    letterSpacing: -0.73px
    fontWeight: 450
    fontVariationSettings: '"wdth" 100, "opsz" 42'
  heading-3xl:
    fontFamily: "{typography.font-family-sans}"
    fontSize: 32px
    lineHeight: 1.06
    letterSpacing: -0.15px
    fontWeight: 450
    fontVariationSettings: '"wdth" 100, "opsz" 32'
    usage: "卡片组主标题、功能大卡标题"
  heading-2xl:
    fontFamily: "{typography.font-family-sans}"
    fontSize: 28px
    lineHeight: 1.08
    letterSpacing: -0.1px
    fontWeight: 450
    fontVariationSettings: '"wdth" 100, "opsz" 28'
  heading-xl:
    fontFamily: "{typography.font-family-sans}"
    fontSize: 24px
    lineHeight: 1.08
    letterSpacing: -0.07px
    fontWeight: 700
    fontVariationSettings: '"wght" 700, "wdth" 100, "opsz" 24'
    usage: "小节重强调标题、深色卡片头部"
  heading-lg:
    fontFamily: "{typography.font-family-sans}"
    fontSize: 22px
    lineHeight: 1.12
    letterSpacing: -0.08px
    fontWeight: 700
    fontVariationSettings: '"wght" 700, "wdth" 100, "opsz" 22'

  # 阅读与应用层级 (Body, Micro-copy & CTA)
  body-lead:
    fontFamily: "{typography.font-family-sans}"
    fontSize: 20px
    lineHeight: 1.3
    letterSpacing: -0.05px
    fontWeight: 450
    fontVariationSettings: '"wdth" 100, "opsz" 20'
    usage: "引导摘要段落"
  body-md:
    fontFamily: "{typography.font-family-sans}"
    fontSize: 17.5px
    lineHeight: 1.45
    letterSpacing: 0.18px
    fontWeight: 400
    fontVariationSettings: '"wdth" 100, "opsz" 17.5'
    usage: "系统基准正文 (Standard Base)"
  caption-sm:
    fontFamily: "{typography.font-family-sans}"
    fontSize: 14.5px
    lineHeight: 1.45
    letterSpacing: 0.16px
    fontWeight: 400
    fontVariationSettings: '"wdth" 100, "opsz" 15'
    usage: "辅助信息、元数据、卡片副文"
  caption-xs:
    fontFamily: "{typography.font-family-sans}"
    fontSize: 12.5px
    lineHeight: 1.24
    letterSpacing: 0.11px
    fontWeight: 450
    usage: "微型徽章、浮动提示、状态指示"
  cta-primary:
    fontFamily: "{typography.font-family-sans}"
    fontSize: 17.5px
    lineHeight: 1.45
    letterSpacing: 0.18px
    fontWeight: 450
    usage: "主要行动按钮文字"
  cta-compact:
    fontFamily: "{typography.font-family-sans}"
    fontSize: 14.5px
    lineHeight: 1.45
    letterSpacing: 0.11px
    fontWeight: 450
    usage: "紧凑型导航/次级按钮文字"
  code-accent:
    fontFamily: "{typography.font-family-mono}"
    fontSize: 14.5px
    lineHeight: 1.45
    letterSpacing: 0px
    fontWeight: 400
    usage: "行内代码与技术指标"

rounded:
  none: "0px"
  xs: "4px"                          # 微型标签、行内代码、输入框
  sm: "8px"                          # 表格容器、图标小底板、卡片内部组件
  md: "16px"                         # 右键菜单浮层、标准卡片圆角
  lg: "24px"                         # 弹窗面板、移动端下拉菜单底边缘
  xl: "36px"                         # 标志性 Antigravity 视听大卡、Hero Media 弧度
  xxl: "48px"                        # 超大功能区外框
  pill: "9999px"                     # 药丸按钮、全圆标签、自定义光标 Badge
  full: "9999px"

spacing:
  none: "0px"
  xs: "4px"
  sm: "8px"
  md: "16px"
  lg: "24px"
  xl: "36px"
  xxl: "48px"
  3xl: "60px"
  4xl: "80px"
  5xl: "88px"
  6xl: "120px"
  7xl: "180px"

components:
  button-primary:
    backgroundColor: "{colors.primary}"
    textColor: "{colors.on-primary}"
    typography: "{typography.cta-primary}"
    rounded: "{rounded.pill}"
    padding: "10px 24px"
    border: "1px solid transparent"
  button-primary-hover:
    backgroundColor: "{colors.primary-hover}"
    textColor: "{colors.on-primary}"
  button-primary-inverse:
    backgroundColor: "{colors.canvas}"
    textColor: "{colors.ink}"
    typography: "{typography.cta-primary}"
    rounded: "{rounded.pill}"
    padding: "10px 24px"
  button-secondary:
    backgroundColor: "{colors.overlay-button-secondary}"
    textColor: "{colors.ink}"
    typography: "{typography.cta-primary}"
    rounded: "{rounded.pill}"
    padding: "10px 24px"
    border: "1px solid {colors.outline-variant}"
    backdropFilter: "blur(6px)"
  button-secondary-inverse:
    backgroundColor: "rgba(170, 177, 204, 0.2)"
    textColor: "{colors.on-surface-inverse}"
    typography: "{typography.cta-primary}"
    rounded: "{rounded.pill}"
    padding: "10px 24px"
    border: "1px solid {colors.inverse-outline-variant}"
    backdropFilter: "blur(8px)"
  nav-compact-button:
    backgroundColor: "rgba(183, 191, 217, 0.09)"
    textColor: "{colors.muted}"
    typography: "{typography.cta-compact}"
    rounded: "{rounded.pill}"
    padding: "8px 16px"
  custom-cursor-pill:
    backgroundColor: "{colors.canvas}"
    textColor: "{colors.ink}"
    typography: "{typography.caption-sm}"
    rounded: "{rounded.pill}"
    padding: "16px 24px 16px 16px"
    border: "1px solid {colors.outline-variant}"
    boxShadow: "0 8px 24px rgba(0, 0, 0, 0.08)"
  video-control-pill:
    backgroundColor: "{colors.overlay-video-control}"
    textColor: "{colors.canvas}"
    rounded: "{rounded.full}"
    width: "48px"
    height: "48px"
    backdropFilter: "blur(16px)"
  macro-feature-card:
    backgroundColor: "{colors.surface-container}"
    rounded: "{rounded.xl}"
    overflow: "hidden"
  immersive-download-hero:
    backgroundColor: "{colors.surface-inverse}"
    textColor: "{colors.on-surface-inverse}"
    rounded: "{rounded.xl}"
    paddingBlock: "180px"
---

# Google Antigravity 设计系统规范文档 (DESIGN-antigravity.md)

> **规范版本**: `1.0.0-antigravity`  
> **基准分析工程**: [antigravity-official-backup](file:///c:/Users/huang/Documents/Antigravity/antigravity-official-backup)  
> **官方在线形态**: `https://antigravity.google/`  
> **适用范围**: Google Antigravity 官方及衍生生态站点、AI Coding Agent 代码生成规范、高端先锋科技 UI 构建标准。

---

## 零、 核心设计哲学 (Design Philosophy & Metaphor)

Google Antigravity 是 Google 专为下一代**智能体协作与代码工程（Agent-First Engineering）**打造的平台级视觉载体。其设计语言的核心不仅是“现代审美”，更是对“反重力（Antigravity）”这一物理隐喻的技术化转译：

```
                    ┌────────────────────────────────────────┐
                    │      反重力哲学 (The Antigravity)      │
                    │   零重力悬浮 · 极致轻盈 · 空间科技克制  │
                    └───────────────────┬────────────────────┘
                                        │
        ┌───────────────────────────────┴──────────────────────────────┐
        ▼                                                              ▼
┌──────────────────────────────┐                              ┌──────────────────────────────┐
│  物理悬浮与磁吸 (Floating)   │                              │ 机械克制与纯净 (Restraint)   │
│ · 36px 宏观柔润大圆角 (XL)   │                              │ · 纯粹黑白灰微冷阶梯 (Greys) │
│ · 9999px 全胶囊悬浮交互点   │                              │ · Google Sans Flex 450 精密  │
│ · 磁吸动态光标 (Smart Cursor)│                              │ · 0.06 极淡激光级细线描边    │
│ · Canvas 零重力无序粒子流    │                              │ · 底部巨幅纯黑空间跃迁质感   │
└──────────────────────────────┘                              └──────────────────────────────┘
```

1. **零重力悬浮感 (Floating & Weightlessness)**：
   界面抛弃传统重阴影、实心卡片堆砌的做法，大范围采用 **透光毛玻璃（Backdrop Blurs: 5px~16px）**、**36px 宏观柔润大倒角（`--shape-corner-xl: 36px`）** 以及 **全胶囊药丸轮廓（`9999px`）**。界面元素如宇宙舱内的漂浮物，顺滑、无摩擦阻力。
2. **纯粹单色克制与 Google 极光对撞 (Monochrome Discipline vs. Spectral Spark)**：
   全局 95% 以上的视觉面积严格由 **13 档微冷 Slate Greys（`#121317` 至 `#ffffff`）** 统领。拒绝千篇一律的浓艳渐变，仅在核心 Logo、悬浮粒子与微型状态徽章中保留纯正 Google 经典色谱（红、黄、绿、电光蓝 `#3279f9`），制造“深空中的灵光一现”。
3. **明暗逆向二元论 (Inverse Surface Bifurcation)**：
   系统不采用全局切换的 Dark Mode，而是在页面行进节奏中注入**剧烈的明暗空间反转**——整页前 80% 为极透亮的纯白冷灰空间，到了最终沉浸式的行动召唤区（Download Section），瞬间切换为深邃的宇宙纯黑（`#121317`），并在黑底上反转注入纯白发光药丸按钮，形成不可抗拒的心理聚焦。

---

## 一、 色彩与材质系统 (Color Palette & Surface Materials)

Antigravity 的色彩系统是一套经过严密对比度（WCAG AA/AAA）核算的工业级调色板。

### 1.1 灰阶色系表 (The Slate Grey Ladder)

所有色彩建立在微冷蓝灰底色上，拒绝发黄发暖的脏灰：

| Token 名称 | 物理十六进制 / RGB | 语义角色与用途 | 对白底对比度 |
| :--- | :--- | :--- | :--- |
| `palette.grey-0` | `#ffffff` / `255, 255, 255` | 纯白画布基底、主要按钮文字、高光浮层 | 1:1 |
| `palette.grey-10` | `#f8f9fc` | 极浅冷灰底板、Surface Container、卡片背景 | 1.05:1 |
| `palette.grey-15` | `#f0f1f5` | 次要按钮 Hover 态微弱填充 | 1.12:1 |
| `palette.grey-20` | `#eff2f7` | 中浅交互底、导航悬停底（Container High） | 1.15:1 |
| `palette.grey-50` | `#e6eaf0` | 分割槽底色、滑块轨道底色 | 1.25:1 |
| `palette.grey-100` | `#e1e6ec` | 结构边界强调、不可点击背景 | 1.35:1 |
| `palette.grey-300` | `#b2bbc5` | 深色反转面板上的次级副文本 | 3.5:1 (对黑底) |
| `palette.grey-400` | `#b7bfd9` | 通透玻璃态按钮的基础色调 (微冷紫灰) | - |
| `palette.grey-800` | `#45474d` | **官方副标题与第二正文色** (`--theme-surface-on-surface-variant`) | **9.5:1 (AAA)** |
| `palette.grey-900` | `#2f3034` | 主行动按钮悬停加深色 | 12.8:1 |
| `palette.grey-1000` | `#212226` | 标题链接点击按压色、描边基底色 | 15.6:1 |
| `palette.grey-1200` | `#121317` | **全局绝对主文本色、逆向黑卡底板** (`--theme-surface-on-surface`) | **18.2:1 (AAA)** |

### 1.2 材质与光学描边 (Hairlines & Glassmorphism)

Antigravity 坚决摒弃厚重描边。系统规范要求所有边框使用**极微透明度中性灰**：

* **白天模式浅色描边**:
  * 主分割线: `border: 1px solid rgba(33, 34, 38, 0.06);`（6% 极轻微炭黑，清晰划分模块而不割裂视觉）
  * 控件描边: `border: 1px solid rgba(33, 34, 38, 0.12);`（12% 炭黑，用于输入框、次要按钮）
* **黑夜沉浸逆向描边**:
  * `border: 1px solid rgba(230, 234, 240, 0.06);`（6% 冷白透光折痕）
* **毛玻璃光效参数**:
  * 导航栏 Header: `background: #ffffffd9; backdrop-filter: blur(5px);`
  * 悬浮右键菜单 Context Menu: `background: #ffffff; backdrop-filter: blur(16px); box-shadow: 0 16px 40px rgba(0,0,0,0.12), 0 3px 10px rgba(0,0,0,0.04);`
  * 视频浮动控制钮: `background: rgba(255, 255, 255, 0.12); backdrop-filter: blur(16px);`

---

## 二、 排版与可变字体阶梯 (Typography & Font Mechanics)

系统全面拥抱 Google 现代可变字体（Variable Fonts）体系，通过 **Google Sans Flex** 的字宽（`wdth`）、字重（`wght`）以及光学字号轴（`opsz`）实现极度精密排版。

```
Google Sans Flex: opsz 8..144, slnt -10..0, wdth 25..150, wght 400..500, ROND 0..100
Google Sans Code: 0..1 (Italic / Regular)
Google Symbols: opsz 20..48, wght 100..700, FILL 0..1, GRAD -50..200, ROND 0..100
```

### 2.1 工业级 12 档排版阶梯表

| 规范级别 | 桌面字号 / 行高 | 负字距 (Tracking) | 轴参数与字重 | 推荐场景 |
| :--- | :--- | :--- | :--- | :--- |
| **`landing-main`** | **107px / 107px** | `-2.14px` | `opsz: 144, wght: 450` | 首屏主 Slogan（大屏绝对重力点） |
| **`heading-00 (9xl)`** | **148px / 145px** | `-2.96px` | `opsz: 144, wght: 450` | 巨型数据/极度张力数字 |
| **`heading-1 (7xl)`** | **98px / 82px** | `-1.80px` | `opsz: 98, wght: 450` | 首屏备选超级大标题 |
| **`heading-2 (6xl)`** | **72px / 72px** | `-1.44px` | `opsz: 72, wght: 450` | 核心模块 Section 大标题 |
| **`heading-3 (5xl)`** | **54px / 56.16px** | `-0.95px` | `opsz: 54, wght: 450` | 二级大区块主标题 |
| **`heading-4 (4xl)`** | **42px / 43.68px** | `-0.73px` | `opsz: 42, wght: 450` | 特性大卡标题、视听演示标题 |
| **`heading-5 (3xl)`** | **32px / 33.92px** | `-0.15px` | `opsz: 32, wght: 450` | Markdown 一级标题、对话标题 |
| **`heading-6 (2xl)`** | **28px / 30.24px** | `-0.10px` | `opsz: 28, wght: 450` | 弹窗 Modal 标题、卡片组头部 |
| **`heading-7 (xl)`** | **24px / 25.92px** | `-0.07px` | `opsz: 24, wght: 700` | 粗体小节标题、Markdown H2 |
| **`body-lead`** | **20px / 26px** | `-0.05px` | `opsz: 20, wght: 450` | 摘要前导句、引导正文 |
| **`body (base)`** | **17.5px / 25.38px** | `+0.18px` | `opsz: 17.5, wght: 400` | **系统基准正文 (Standard Body)** |
| **`caption (sm)`** | **14.5px / 21.02px** | `+0.16px` | `opsz: 15, wght: 400` | 辅助说明、元数据、紧凑按钮 |
| **`small (xs)`** | **12.5px / 15.5px** | `+0.11px` | `opsz: 12.5, wght: 450` | 右键状态微标、法律版权信息 |

> **关键规则（Typography Rules）**：
> 1. **避免粗笨的 700 字重轰炸**：标题普遍采用 **`font-weight: 450`**。这是 Google Sans Flex 独特的人文优雅字重，既有结构分量，又保留通透骨架。
> 2. **大字距收紧法则**：字号大于 24px 时必须强制应用负字距（`-0.07px` 到 `-2.96px`），消除字体松垮感。
> 3. **等宽代号标注**：对于代号、环境参数、指令调用，使用 `Google Sans Code`（20px / 行高 28px / `-0.08px`），颜色指定为 `#121317`。

---

## 三、 几何形态、网格与圆角体系 (Geometry, Grids & Radii)

### 3.1 标志性圆角矩阵 (Shape Corners)

Antigravity 的几何特征是由**极端的大圆角（36px）**与**极致的胶囊圆角（9999px）**共同塑造的：

```
[  4px (XS)  ]  --> 输入框微弧度、行内代码块
[  8px (SM)  ]  --> 数据表格、次级图标背板、Markdown 提示块
[ 16px (MD)  ]  --> 悬浮右键菜单、标准特性卡片
[ 24px (LG)  ]  --> 下拉抽屉底角、弹窗外框
[ 36px (XL)  ]  --> ★ 标志性视听巨卡、Hero 视频包裹框、Download 黑卡外框
[ 9999px (Full) ] --> ★ 所有按钮、自定义光标药丸、滑动控制条
```

### 3.2 布局网格与响应式断点 (Fluid Responsive Grid)

页面容器使用标准 **12 栏响应式流体网格**，通过 `calc(-1 * var(--grid-gutter) / 2)` 实现负边距内嵌平齐：

* **断点定义**:
  * `xs`: `<= 425px`（4 栏网格，间距 16px，页面内边距 16px）
  * `sm`: `<= 767px`（4 栏网格，间距 16px，页面内边距 16px）
  * `md`: `<= 1024px`（8 栏网格，间距 40px，页面内边距 40px）
  * `lg`: `<= 1440px`（12 栏网格，间距 48px，页面内边距 72px）
  * `xl / max`: `1600px`（12 栏网格，间距 64px，最大宽度限制 `1728px + 144px`）

### 3.3 垂直节奏间距 (Vertical Rhythm)

* 微间距: `xs (4px)`, `sm (8px)`, `md (16px)`, `lg (24px)`
* 模块间距: `xl (36px)`, `2xl (48px)`, `3xl (60px)`, `4xl (80px)`
* 巨型宏观节奏: `5xl (88px)`, `6xl (120px)`, `7xl (180px)`
  * 落地页各大 Section 必须保持 `padding-block: var(--space-6xl) 0 var(--space-5xl);`（120px 顶部 / 88px 底部），确保极致的呼吸感。

---

## 四、 核心 UI 组件规范与交互状态 (Component Grammar & States)

### 4.1 主行动按钮 (Button Primary)

核心主 CTA 按钮是极具标识度的纯黑全胶囊药丸：

```css
.button-primary {
  font-family: "Google Sans Flex", sans-serif;
  font-size: 17.5px;
  line-height: 25.38px;
  letter-spacing: 0.18px;
  font-weight: 450;
  padding: 10px 24px;
  border-radius: 9999px;
  background-color: #121317; /* 主墨色 */
  color: #ffffff;
  border: 1px solid transparent;
  cursor: pointer;
  transition: all 0.15s ease-out;
  display: inline-flex;
  align-items: center;
  justify-content: center;
  text-decoration: none;
}
.button-primary:hover,
.button-primary:focus-visible {
  background-color: #2f3034; /* 加深微灰 */
  outline: none;
}
.button-primary:disabled {
  background-color: #f8f9fc;
  color: #6a6a71;
  cursor: not-allowed;
}
```

### 4.2 磨砂次级按钮 (Button Secondary)

利用高斯模糊与极淡微冷紫灰打造的“反重力浮动层”：

```css
.button-secondary {
  font-family: "Google Sans Flex", sans-serif;
  font-size: 17.5px;
  font-weight: 450;
  padding: 10px 24px;
  border-radius: 9999px;
  color: #121317;
  background: rgba(183, 191, 217, 0.1);
  backdrop-filter: blur(6px);
  border: 1px solid rgba(33, 34, 38, 0.06);
  transition: all 0.15s ease-out;
}
.button-secondary:hover {
  background: #f0f1f5;
  outline: none;
}
```

### 4.3 暗夜逆向按钮 (Inverse Primary & Secondary)

专用于底部纯黑 Download Section 等深色容器：

```css
/* 纯白逆向主按钮 */
.button-primary-inverse {
  background: #ffffff;
  color: #121317;
  border-radius: 9999px;
  padding: 10px 24px;
  font-weight: 450;
}
.button-primary-inverse:hover {
  background: #eff2f7;
}

/* 磨砂逆向次要按钮 */
.button-secondary-inverse {
  color: #ffffff;
  background: rgba(183, 191, 217, 0.2);
  backdrop-filter: blur(8px);
  border: 1px solid rgba(230, 234, 240, 0.06);
  border-radius: 9999px;
  padding: 10px 24px;
}
.button-secondary-inverse:hover {
  background: rgba(170, 177, 204, 0.3);
}
```

### 4.4 磁吸智能光标 (Smart Custom Cursor)

在大型视频卡片或交互视听容器内，鼠标原生光标隐藏，由悬浮白色胶囊接管：

```css
.custom-cursor {
  position: absolute;
  top: 0;
  left: 0;
  pointer-events: none;
  z-index: 100;
  will-change: transform;
}
.cursor-content {
  background: #ffffff;
  color: #000000;
  padding: 16px 24px 16px 16px;
  border-radius: 999px;
  border: 1px solid rgba(33, 34, 38, 0.06);
  box-shadow: 0 8px 24px rgba(0, 0, 0, 0.08);
  display: flex;
  align-items: center;
  gap: 8px;
  white-space: nowrap;
}
.cursor-content .symbol {
  font-family: "Google Symbols";
  font-size: 24px;
  font-variation-settings: "FILL" 1, "wght" 400, "GRAD" 0, "ROND" 50, "opsz" 48 !important;
}
```

### 4.5 桌面级 Logo 右键菜单 (Context Menu)

在导航栏的 Antigravity Logo 上，右键交互被重塑为桌面级浮动工具栏：
* 尺寸: `min-width: 235px`, 边距 `padding: 8px`
* 倒角: `border-radius: 16px`
* 阴影: `box-shadow: 0 16px 40px rgba(0,0,0,0.12), 0 3px 10px rgba(0,0,0,0.04);`
* 动作项: 支持“复制 SVG 图标”、“复制 PNG 资产”，并带绿色 Check 确认状态。

---

## 五、 物理动效与视差控制 (Motion Physics & Parallax)

Antigravity 的动效哲学是**平滑的惯性流体与无重力缓冲**，杜绝生硬的线性突变：

### 5.1 官方贝塞尔曲线 (Bezier Curves)

```css
/* 进入与微交互主要曲线 */
--ease-out-cubic: cubic-bezier(0.215, 0.61, 0.355, 1);
--ease-out-quart: cubic-bezier(0.165, 0.84, 0.44, 1);
--ease-out-expo: cubic-bezier(0.19, 1, 0.22, 1);
/* 弹性微动效 (如弹窗弹出、小图标复位) */
--ease-out-back: cubic-bezier(0.34, 1.85, 0.64, 1);
```

### 5.2 核心动效模式

1. **视差缩放 (Feature Media Parallax)**：
   视频外框固定在 `--shape-corner-xl: 36px` 剪裁区内，内部媒体在滚动时应用 GSAP ScrollTrigger，执行从 `scale(1.08)` 到 `scale(1.0)` 的自然减速回弹。
2. **反重力浮动球 (The Bouncers)**：
   直径 98px、`border-radius: 50%`、背景色 `#b7bfd917`，结合鼠标位移或陀螺仪产生微小的惯性反向漂浮（Anti-gravity Drift）。
3. **打字机光标闪烁 (Terminal Blink)**：
   终端与代码提示区域，光标以 `0.5s infinite` 进行微透明度闪烁（`0% { opacity: 0; } 10% { opacity: 1; } 100% { opacity: 0; }`）。

---

## 六、 AI Agent 代码实施与生成规范 (Rules for Coding Agents)

当 AI 编程助手（Cursor / Claude / Antigravity 等）依据本规范编写或生成 UI 时，**必须严格遵守以下法则**：

### 6.1 强制规范 (DO)
1. **严格使用语义 Token**：背景必须调用 `var(--palette-grey-10)` 或 `var(--theme-surface-surface)`，绝不随意手写 `#f3f4f6` 或任意随机色值。
2. **强制负字距**：页面中所有 H1~H3 大标题必须配比对应的负字距（如 54px 标题强制配合 `-0.95px` letter-spacing）。
3. **大卡片必须使用 36px 圆角**：任何承载核心视频、产品截图或图文特性的卡片，其外框必须采用 `border-radius: 36px` 并设置 `overflow: hidden;`。
4. **按钮必须为全胶囊 9999px**：所有普通按钮、次级按钮统一使用 `border-radius: 9999px;`，严禁写成 4px 或 6px 的普通方角。
5. **暗夜黑卡必须处于结构底部**：落地页末尾的转化/下载模块必须以 `#121317` 作为背景底板，并在其内部全部使用 `Inverse` 系列变量。

### 6.2 严厉禁止反模式 (DON'T)
1. **禁止生成高饱和度大彩块**：禁止把主按钮做成亮紫、亮绿或大红；主交互统一为纯黑 `#121317` 或极光蓝 `#3279f9`。
2. **禁止使用浓黑粗阴影**：严禁出现 `box-shadow: 0 10px 30px rgba(0,0,0,0.5)` 这种脏污阴影；只允许使用 6% 细描边或 4%~8% 的弥散微阴影。
3. **禁止遗漏 WCAG 状态闭环**：按钮必须提供完整的 `:hover`、`:focus-visible` 和 `:disabled` 状态。
4. **禁止破坏 12 栏响应式间距**：大屏幕上下间距严禁小于 80px，保证太空般的呼吸节奏。

# Google Antigravity 官方展示页前端规范与高保真技术复现方案

> **文档性质**：面向零上下文智能体（AI Agent）与高精前端团队的 100% 像素级复现工程技术方案  
> **配套资产包**：[`resources/`](file:///c:/Users/huangfei/Documents/Antigravity/antigravity-official-backup/resources/) / [`resources.zip`](file:///c:/Users/huangfei/Documents/Antigravity/antigravity-official-backup/resources.zip)  
> **基准参考站点**：Google Antigravity 官方展示页 (`https://antigravity.google/`)  
> **规范版本**：`v1.0.0-PROD`

---

## 零、 给“无上下文 Agent”的初始化指引 (Agent Initialization Prompt)

> 🤖 **致正在阅读本文档的 AI Agent**：
> 
> 你正在执行 **Google Antigravity 官方展示落地页** 的 100% 像素级高保真复现任务。你无需任何历史会话上下文，**本文档与配套的 `resources/` 资产包（或 `resources.zip`）是你的唯一真理来源（Single Source of Truth）**。
> 
> 请严格遵守以下执行纪律：
> 1. **零假设原则**：不要臆测样式或替换图片。所有尺寸、颜色、圆角、字重、动效均在本文档中做了工业级定量定义。
> 2. **资源路径 1:1 映射**：页面所需的全部媒体（图片、视频、字体、粒子贴图）均已就绪在 `resources/` 目录中，严禁使用外部未经验证的外链或生成占位图。
> 3. **极简落地策略**：若需极速启动生产级展示，可直接使用【路径 A：原生零依赖静态复现】；若需集成进现代前端工程（React / Vue / Astro / Vite），请遵循【路径 B：现代组件化工程重构】。

```
                                  【复现执行全景】
 ┌───────────────────────────┐                     ┌───────────────────────────┐
 │   TECH-SPEC-REPRODUCTION  │                     │     resources/ 资产包     │
 │  (本文档：规范/结构/交互)   │                     │  (字体/图片/视频/样式/JS)   │
 └─────────────┬─────────────┘                     └─────────────┬─────────────┘
               │                                                 │
               └───────────────────────┬─────────────────────────┘
                                       ▼
                     ┌───────────────────────────────────┐
                     │ 零上下文 Agent 自动化解析与构建      │
                     └─────────────────┬─────────────────┘
                                       │
        ┌──────────────────────────────┴──────────────────────────────┐
        ▼                                                             ▼
┌─────────────────────────────────┐                 ┌─────────────────────────────────┐
│  路径 A：原生零依赖极速组装        │                 │  路径 B：现代组件化工程重构       │
│  - 纯原生 HTML5 + server.js     │                 │  - Vite / Astro / Vue / React   │
│  - 10 分钟 100% 像素级完美运行   │                 │  - 基于 Design Tokens 组件化解耦 │
└─────────────────────────────────┘                 └─────────────────────────────────┘
```

---

## 一、 架构总览与复现路径 (Architecture & Replication Pathways)

### 1.1 路径 A：原生零依赖静态复现（推荐首选，10 分钟 100% 还原）

如果你的目标是**最快速度、零环境风险、绝对 100% 保真**地拉起运行环境，采用此方案。

#### 步骤 1：解压并定位资源目录
确保目标项目根目录下具备以下拓扑结构（直接从 `resources/` 复制或解压 `resources.zip`）：
```text
my-antigravity-project/
├── index.html                   # 从 resources/template/index.html 复制至根目录
├── favicon.ico                  # 从 resources/icons/favicon.ico 复制至根目录
├── apple-touch-icon.png         # 从 resources/icons/apple-touch-icon.png 复制
├── apple-touch-icon-precomposed.png
├── assets/                      # 直接完整映射 resources/assets/
│   ├── fonts/
│   │   ├── GoogleSymbols.ttf    # 核心矢量符号库 (33.5MB)
│   │   └── fonts.css            # 字体 @font-face 声明
│   ├── image/                   # 全套官方图片 (logo, cursor, blog, landing)
│   ├── textures/                # WebGL / Canvas 粒子纹理贴图
│   └── video/                   # 官方高清演示视频 (hero_video.mp4 等)
├── _astro/                      # 直接完整映射 resources/_astro/
│   ├── BaseLayout.BS3t_nql.css
│   ├── SmoothScrollLayout.D7KgMQYn.css
│   ├── index.BMvyDU_X.css
│   └── *.js                     # 全套 24 个 Astro 构建后的 JS 运行时模块
├── server.js                    # 原生 Node.js 流式静态服务脚本 (见下文)
└── package.json
```

#### 步骤 2：配置零依赖流媒体服务器 (`server.js`)
落地页中包含大体积高清演示视频（如 `assets/video/hero_video.mp4`），必须支持 **HTTP 206 Partial Content Range** 请求以保证视频流畅播放与拖动进度条。

编写并使用如下原生 Node.js 服务器：
```javascript
import http from 'http';
import fs from 'fs';
import path from 'path';
import { fileURLToPath } from 'url';

const __filename = fileURLToPath(import.meta.url);
const __dirname = path.dirname(__filename);
const PORT = process.env.PORT || 3000;

const MIME_TYPES = {
  '.html': 'text/html; charset=utf-8',
  '.css': 'text/css; charset=utf-8',
  '.js': 'application/javascript; charset=utf-8',
  '.mjs': 'application/javascript; charset=utf-8',
  '.json': 'application/json; charset=utf-8',
  '.png': 'image/png',
  '.jpg': 'image/jpeg',
  '.jpeg': 'image/jpeg',
  '.gif': 'image/gif',
  '.svg': 'image/svg+xml',
  '.ico': 'image/x-icon',
  '.mp4': 'video/mp4',
  '.webm': 'video/webm',
  '.woff': 'font/woff',
  '.woff2': 'font/woff2',
  '.ttf': 'font/ttf',
  '.xml': 'application/xml; charset=utf-8'
};

const server = http.createServer((req, res) => {
  res.setHeader('Access-Control-Allow-Origin', '*');

  let reqPath = decodeURI(req.url.split('?')[0]);
  if (reqPath === '/') reqPath = '/index.html';

  const filePath = path.normalize(path.join(__dirname, reqPath));
  if (!filePath.startsWith(__dirname)) {
    res.writeHead(403, { 'Content-Type': 'text/plain' });
    res.end('403 Forbidden');
    return;
  }

  fs.stat(filePath, (err, stats) => {
    if (err || !stats.isFile()) {
      res.writeHead(404, { 'Content-Type': 'text/plain' });
      res.end(`404 Not Found: ${reqPath}`);
      return;
    }

    const ext = path.extname(filePath).toLowerCase();
    const contentType = MIME_TYPES[ext] || 'application/octet-stream';

    // 支持视频流 HTTP 206 Range 传输
    const range = req.headers.range;
    if (range && (ext === '.mp4' || ext === '.webm')) {
      const parts = range.replace(/bytes=/, '').split('-');
      const start = parseInt(parts[0], 10);
      const end = parts[1] ? parseInt(parts[1], 10) : stats.size - 1;
      const chunksize = end - start + 1;

      res.writeHead(206, {
        'Content-Range': `bytes ${start}-${end}/${stats.size}`,
        'Accept-Ranges': 'bytes',
        'Content-Length': chunksize,
        'Content-Type': contentType
      });
      fs.createReadStream(filePath, { start, end }).pipe(res);
      return;
    }

    res.writeHead(200, {
      'Content-Length': stats.size,
      'Content-Type': contentType,
      'Accept-Ranges': 'bytes',
      'Cache-Control': 'no-cache'
    });
    fs.createReadStream(filePath).pipe(res);
  });
});

server.listen(PORT, '0.0.0.0', () => {
  console.log(`Antigravity local server running at http://localhost:${PORT}/`);
});
```

#### 步骤 3：一键启动
在 `package.json` 中配置：
```json
{
  "name": "antigravity-reproduction",
  "version": "1.0.0",
  "type": "module",
  "scripts": {
    "dev": "node server.js",
    "start": "node server.js"
  }
}
```
执行 `pnpm dev` 或 `node server.js`，浏览器打开 `http://localhost:3000` 即可完全再现。

---

### 1.2 路径 B：现代组件化工程重构（现代框架开发方案）

若要在现代工程（React / Vue 3 / Astro / Svelte）中组件化解耦重构，项目需拆解为以下组件树：

```
App (Root / SmoothScrollLayout)
├── Header (导航、Logo 上下文菜单、胶囊按钮)
├── WelcomeSection (首屏 Hero、打字机光标、MainParticles 粒子 Canvas)
├── LandingVideoSection (36px 视听大卡、Custom Cursor、YouTube 模态框)
├── AgentFirstSection (概念叙事网格、对比卡片)
├── FeatureExplorerSection (特性卡片组、视差滚动、交互说明)
├── UseCasesSection (用例横向轮播 Slider、左右切换控制器)
├── TrySolutionsSection (解决方案引导)
├── LandingLatestBlogs (3 列响应式博客卡片网格)
├── DownloadSection (标志性暗夜黑卡、纯白药丸下载按钮)
└── AntigravityFooter (多栏底部链接、语言选择器、Google 法律声明)
```

---

## 二、 完整设计系统规范 (Design System & Design Tokens)

页面所有视觉呈现严格遵循以下物理级 Design Tokens。严禁脱离 Token 随意手写样式。

### 2.1 调色板与材质阶梯 (Color Palette)

#### 13 档微冷 Slate Greys 灰阶体系
| 变量名 | 色值 (Hex / RGBA) | 语义与用途 | 对比度 (WCAG) |
| :--- | :--- | :--- | :--- |
| `--palette-grey-0` | `#ffffff` | 纯白底色、高光面板、主要按钮白字、暗夜反转按钮底 | 1:1 |
| `--palette-grey-10` | `#f8f9fc` | 极浅冷灰底板、卡片默认底色 (`--theme-surface-surface-container`) | 1.05:1 |
| `--palette-grey-15` | `#f0f1f5` | 次要按钮 Hover 态轻微增色 | 1.12:1 |
| `--palette-grey-20` | `#eff2f7` | 导航激活高亮底、药丸槽底色 (`surface-container-high`) | 1.15:1 |
| `--palette-grey-50` | `#e6eaf0` | 分割槽底色、微弱描边槽 (`surface-container-higher`) | 1.25:1 |
| `--palette-grey-100` | `#e1e6ec` | 次级结构强调浅灰 | 1.35:1 |
| `--palette-grey-300` | `#b2bbc5` | 暗夜反转面板上的副文本颜色 (`on-surface-inverse-variant`) | 3.5:1 (对黑底) |
| `--palette-grey-400` | `#b7bfd9` | 通透玻璃态按钮底色的基调 (带微弱紫冷调) | - |
| `--palette-grey-800` | `#45474d` | **官方副标题与第二正文色** (`on-surface-variant`) | **9.5:1 (AAA)** |
| `--palette-grey-900` | `#2f3034` | 主行动纯黑按钮悬停加深色 (`primary-hover`) | 12.8:1 |
| `--palette-grey-1000` | `#212226` | 标题链接点击按压态 | 15.6:1 |
| `--palette-grey-1200` | `#121317` | **全局绝对主文本色、主要按钮底、暗夜黑卡底板** | **18.2:1 (AAA)** |

#### 品牌点缀色 (Google Brand Accents)
- **核心交互极光蓝**：`--theme-primary-primary: #3279f9;` (交互链接、Focus 光环、品牌强调)
- **极光蓝悬停深色**：`#1557b0`
- **浅通透蓝容器底**：`#e8f0fe` (徽章 Tag、通知底色)

#### 激光手术刀级透明描边 (Hairline Outlines)
- **浅色背景主描边**：`border: 1px solid rgba(33, 34, 38, 0.06);` (6% 炭黑透明度，绝不割裂内容)
- **交互控件浅色描边**：`border: 1px solid rgba(33, 34, 38, 0.12);` (12% 炭黑透明度，用于输入框、按钮)
- **暗夜黑卡逆向描边**：`border: 1px solid rgba(230, 234, 240, 0.06);` (6% 冷白微折痕)

#### 光学毛玻璃参数 (Backdrop Blur)
- **导航栏 Header**：`background: rgba(255, 255, 255, 0.85); backdrop-filter: blur(5px);`
- **次要胶囊按钮**：`background: rgba(183, 191, 217, 0.1); backdrop-filter: blur(6px);`
- **Logo 右键菜单 & 视频控制器**：`background: rgba(255, 255, 255, 0.95); backdrop-filter: blur(16px);`

---

### 2.2 可变字体与 12 档排版阶梯 (Typography Mechanics)

系统依赖两套核心字体体系：
1. **Google Sans Flex**：主文字体系，动态调节 `opsz`（视觉尺寸 8..144）、`wght`（字重 400..500）、`wdth`（字宽 25..150）。
2. **Google Symbols**：系统矢量符号字体，通过 `font-variation-settings: "FILL" 1, "wght" 400, "opsz" 48` 精密控制图标渲染。

#### 字体引入规则 (`<head>` 中必须加载)
```html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link rel="stylesheet" href="https://fonts.googleapis.com/css2?family=Google+Sans+Flex:opsz,slnt,wdth,wght,ROND@8..144,-10..0,25..150,400..500,0..100&display=swap">
<link rel="stylesheet" href="/assets/fonts/fonts.css">
```
*注：本地备用矢量符号字体位于 `assets/fonts/GoogleSymbols.ttf`。*

#### 12 档排版比例尺 (Typography Ladder)
| 级别代号 | 桌面字号 / 行高 | 负字距 (Tracking) | 轴设置与字重 | 推荐场景 |
| :--- | :--- | :--- | :--- | :--- |
| **`landing-main`** | **107px / 107px** | `-2.14px` | `opsz: 144, wght: 450` | 首屏主视觉 Slogan |
| **`display-9xl`** | **148px / 145px** | `-2.96px` | `opsz: 144, wght: 450` | 巨幅数据与艺术大标 |
| **`heading-7xl`** | **98px / 82px** | `-1.80px` | `opsz: 98, wght: 450` | 备用超大标题 |
| **`heading-6xl`** | **72px / 72px** | `-1.44px` | `opsz: 72, wght: 450` | 模块 Section 一级大标 |
| **`heading-5xl`** | **54px / 56.16px** | `-0.95px` | `opsz: 54, wght: 450` | 二级大区块统领标题 |
| **`heading-4xl`** | **42px / 43.68px** | `-0.73px` | `opsz: 42, wght: 450` | 视听演示、特性大卡标题 |
| **`heading-3xl`** | **32px / 33.92px** | `-0.15px` | `opsz: 32, wght: 450` | 卡片组主标、Markdown H1 |
| **`heading-2xl`** | **28px / 30.24px** | `-0.10px` | `opsz: 28, wght: 450` | 模态框标题、卡片子项标题 |
| **`heading-xl`** | **24px / 25.92px** | `-0.07px` | `opsz: 24, wght: 700` | 小节加粗标题、技术模块头部 |
| **`body-lead`** | **20px / 26px** | `-0.05px` | `opsz: 20, wght: 450` | 引导摘要、大号导读语 |
| **`body-base`** | **17.5px / 25.38px** | `+0.18px` | `opsz: 17.5, wght: 400` | **系统基准正文 (默认段落)** |
| **`caption-sm`** | **14.5px / 21.02px** | `+0.16px` | `opsz: 15, wght: 400` | 辅助说明、元数据、紧凑按钮 |
| **`caption-xs`** | **12.5px / 15.5px** | `+0.11px` | `opsz: 12.5, wght: 450` | 微型徽章、浮层状态提示、版权注脚 |

> ⚠️ **排版三大铁律**：
> 1. **严禁粗重 700 轰炸**：标题普遍严格采用 **`font-weight: 450`**。
> 2. **大字距强制收敛**：凡字号 $\ge 24\text{px}$，必须配备负字距（`-0.07px` 至 `-2.96px`），消除字体疏离感。
> 3. **等宽代号标注**：对于代码指令与环境参数，统一使用 `Google Sans Code`（20px / 行高 28px / Tracking `-0.08px`）。

---

### 2.3 几何与圆角体系 (Geometry & Radii)

Antigravity 的辨识度建立在**宏观柔润大倒角**与**全胶囊药丸交互**的并存上：

```
--shape-corner-xs: 4px;         /* 输入框内角、行内代码 */
--shape-corner-sm: 8px;         /* 表格容器、图标底板 */
--shape-corner-md: 16px;        /* 右键菜单浮层、标准特性卡片 */
--shape-corner-lg: 24px;        /* 弹窗面板外框 */
--shape-corner-xl: 36px;        /* ★ 标志性视听演示巨卡、Download 纯黑卡片外框 */
--shape-corner-rounded: 9999px; /* ★ 所有主次按钮、自定义光标 Badge、轮播控制器 */
```

### 2.4 响应式栅格与间距系统 (Layout & Responsive Grids)

- **容器标准**：12 栏响应式流体网格，通过 `calc(-1 * var(--grid-gutter) / 2)` 抵消内边距以实现边缘齐平。
- **断点规格**：
  - `xs`: $\le 425\text{px}$（4 栏，槽宽 16px，页边距 16px）
  - `sm`: $\le 767\text{px}$（4 栏，槽宽 16px，页边距 16px）
  - `md`: $\le 1024\text{px}$（8 栏，槽宽 40px，页边距 40px）
  - `lg`: $\le 1440\text{px}$（12 栏，槽宽 48px，页边距 72px）
  - `xl / max`: $1600\text{px}$（12 栏，槽宽 64px，最大限制 $1728\text{px} + 144\text{px}$）
- **垂直节奏 (Vertical Rhythm)**：
  - 大 Section 必须保持 `padding-block: 120px 0 88px;`，绝不压缩高度，确保高维呼吸感。

---

## 三、 10 大核心区块 DOM 结构与组件还原蓝图 (Section-by-Section Blueprint)

以下为页面自上而下 10 大核心功能模块的 1:1 精确结构、属性、语义与素材映射。

```
┌────────────────────────────────────────────────────────────────────────┐
│ 1. Header (Sticky Nav, Vector Logo + Desktop Context Menu, Pill CTA)   │
├────────────────────────────────────────────────────────────────────────┤
│ 2. Welcome / Hero Section (107px Slogan, Terminal Blink, Canvas Mesh)  │
├────────────────────────────────────────────────────────────────────────┤
│ 3. Landing Video Section (36px Macro Media, Custom Cursor, YouTube)    │
├────────────────────────────────────────────────────────────────────────┤
│ 4. Agent-First Section (Narrative Grid, Concept Cards)                 │
├────────────────────────────────────────────────────────────────────────┤
│ 5. Feature Explorer Section (Alternating 2-Col Cards, Parallax Media)  │
├────────────────────────────────────────────────────────────────────────┤
│ 6. Use Cases Section (Horizontal Card Slider, Pill Drag Controls)      │
├────────────────────────────────────────────────────────────────────────┤
│ 7. Try Solutions Section (Guidance CTAs & Links)                       │
├────────────────────────────────────────────────────────────────────────┤
│ 8. Landing Latest Blogs (3-Column Responsive Cards, Media Badges)      │
├────────────────────────────────────────────────────────────────────────┤
│ 9. Download Section (Inverse Pure Black Hero #121317, White Pill CTA)  │
├────────────────────────────────────────────────────────────────────────┤
│ 10. Antigravity Footer (Multi-col Navigation, Language Dropdown)       │
└────────────────────────────────────────────────────────────────────────┘
```

---

### 3.1 Header (吸顶毛玻璃导航与桌面级右键菜单)

#### 结构与功能要点
- **吸顶行为**：`position: fixed; top: 0; left: 0; width: 100%; z-index: 1000;`，通过 `data-scroll-reactive="true"` 监听滚动，滚动超过 20px 时添加背景毛玻璃 `rgba(255, 255, 255, 0.85)` 与细下边框。
- **Logo 矢量定义**：包含完整的 Google Antigravity 高精度 SVG，右键点击 Logo 触发桌面级浮动上下文菜单。
- **右键上下文菜单 (Desktop Context Menu)**：
  - 容器：`border-radius: 16px; background: #ffffff; backdrop-filter: blur(16px); box-shadow: 0 16px 40px rgba(0,0,0,0.12); min-width: 235px;`
  - 菜单项：`copy-logo`（一键复制 SVG 源码到剪贴板，成功时图标变为对勾并提示）。

#### 关键 DOM 片段
```html
<header data-analytics-nav="header" class="header" data-scroll-reactive="true" data-opaque="false" data-header>
  <div class="grid-container">
    <div class="main-content">
      <div class="logo-container">
        <a class="logo-link" href="/" aria-label="Google Antigravity" data-logo-link>
          <!-- Google Antigravity 完整 SVG 图标 (见 resources/template/index.html 第 49 行) -->
          <svg class="logo" viewBox="0 0 869 113" height="21" width="161.49" fill="none">...</svg>
        </a>
        <!-- Logo 上下文菜单 -->
        <div class="logo-context-menu" data-logo-context-menu aria-hidden="true">
          <button class="context-menu-item" data-context-action="copy-logo">
            <span class="item-icon">...</span>
            <span class="item-label">Copy Antigravity Logo SVG</span>
          </button>
        </div>
      </div>
      <!-- 导航项与胶囊 Action 按钮 -->
      <nav class="nav-links">
        <a href="#features" class="button-nav">Features</a>
        <a href="#use-cases" class="button-nav">Use Cases</a>
        <a href="#download" class="button button-primary button-compact">Download</a>
      </nav>
    </div>
  </div>
</header>
```

---

### 3.2 Welcome / Hero Section (首屏科技张力与粒子流)

#### 结构与功能要点
- **标题体系**：
  - 主 Slogan：`Google Antigravity`，采用 `landing-main`（107px 字号 / `-2.14px` 字距 / 450 字重）。
  - 副标题：打字机终端动画（`data-typed-header`），包含带 `0.5s infinite blink` 动画的光标。
- **CTA 按钮组合**：
  - 主按钮：`button-primary`（纯黑 `#121317`，`padding: 10px 24px`，`border-radius: 9999px`）。
  - 次按钮：`button-secondary`（磨砂冷紫灰 `rgba(183, 191, 217, 0.1)` + `backdrop-filter: blur(6px)`）。
- **背景画布 (Canvas Mesh)**：
  - 承载 `<canvas>`，全屏绝对定位，运行 `MainParticlesComponent`，展现漂浮微重力粒子。贴图由 `assets/textures/icons/icon_cube.png` 驱动。

#### 关键 CSS 类与属性
```css
.welcome-wrapper {
  position: relative;
  min-height: 85vh;
  display: flex;
  align-items: center;
  justify-content: center;
  padding-block: var(--space-6xl) var(--space-5xl);
}
.hero-title {
  font-family: "Google Sans Flex", sans-serif;
  font-size: 107px;
  line-height: 1.0;
  letter-spacing: -2.14px;
  font-weight: 450;
  color: var(--palette-grey-1200);
}
.blinking-cursor {
  display: inline-block;
  width: 2px;
  height: 1.1em;
  background-color: var(--palette-grey-1200);
  animation: 0.5s infinite blink;
}
@keyframes blink {
  0%, 100% { opacity: 0; }
  50% { opacity: 1; }
}
```

---

### 3.3 Landing Video Section (36px 视听大卡与磁吸光标)

#### 结构与功能要点
- **宏观倒角**：卡片外层包裹框严格设置 `border-radius: 36px; overflow: hidden;`。
- **本地高清视频**：内嵌 `<video>`，源文件路径指向 `/assets/video/hero_video.mp4`，设置 `playsinline autoplay muted loop`。
- **智能跟随光标 (Custom Cursor)**：
  - 鼠标在 `.video-wrapper` 内移动时，隐藏默认系统鼠标指针（`cursor: none`）。
  - 唤醒跟随的 `.custom-cursor` 胶囊，显示白底微阴影药丸（内嵌 Google Symbols 播放图标 `play_arrow` 与文字 `Watch Video`）。
- **右下角视频控制钮**：`48px × 48px` 全圆毛玻璃按钮，悬停时微弱缩放。
- **点击交互**：点击视频卡片唤出全屏模态框 (`#youtube-dialog`)，居中播放 YouTube 4K 演示。

#### 关键 DOM 片段
```html
<section class="landing-video-section" id="youtube-video-section" data-youtube-video-section>
  <div class="video-header">
    <h2 class="heading-4xl">Experience Agent-First IDE</h2>
    <p class="body-base">Built from the ground up to pair programmer with intelligent agents.</p>
  </div>
  <div class="video-wrapper" data-video-trigger>
    <video class="landing-video" autoplay muted loop playsinline>
      <source src="/assets/video/hero_video.mp4" type="video/mp4">
    </video>
    <!-- 自定义悬浮光标胶囊 -->
    <div class="custom-cursor" data-custom-cursor>
      <div class="cursor-content">
        <span class="symbol">play_arrow</span>
        <span class="label">Play Demo</span>
      </div>
    </div>
    <!-- 右下角常驻微型控件 -->
    <button class="video-control-button" aria-label="Play Fullscreen">
      <span class="symbol">fullscreen</span>
    </button>
  </div>
</section>
```

---

### 3.4 Feature Explorer Section (特性资源管理器)

#### 结构与功能要点
- **布局形式**：双列网格，左右交替排列（奇数行：左文右图；偶数行：左图右文）。
- **图片规格**：外框设置 `border-radius: 36px; overflow: hidden;`，图片设置 `object-fit: cover; width: 100%;`。
- **绑定的核心素材**：
  - 核心特性 1：`/assets/image/landing/antigravity-cli.png`（命令行交互与智能体调用）
  - 核心特性 2：`/assets/image/landing/feature-3.jpg`（可视化多智能体协作网络）
  - 核心特性 3：`/assets/image/product/new-chat.png`（上下文对话与代码生成）

---

### 3.5 Use Cases Section (用例轮播与横向拖拽 Slider)

#### 结构与功能要点
- **轨道容器**：`.slider-track`，横向 CSS Grid 布局，每张用例卡片占据固定视口宽度比例。
- **交互控制器**：
  - 包含 `.slider-controls` 胶囊控制器，内嵌左右圆形切换按钮。
  - 支持触摸横向滑动与鼠标惯性拖拽（底层由 `Draggable.CK_AoxCI.js` 支持）。
- **绑定的核心素材**：
  - 前端工程：`/assets/image/landing/landing-thumbnail-frontend.jpg`
  - 全栈开发：`/assets/image/landing/landing-thumbnail-fullstack.jpg`
  - 企业级协同：`/assets/image/landing/landing-thumbnail-enterprise.jpg`

---

### 3.6 Landing Latest Blogs (3 列响应式博客卡片网格)

#### 结构与功能要点
- **网格规范**：标准 CSS Grid，桌面端 `grid-template-columns: repeat(3, 1fr); gap: 24px;`。
- **卡片形态**：`border-radius: 24px; background: #ffffff; border: 1px solid rgba(33, 34, 38, 0.06);`。悬停时产生 `-4px` 向上微浮动与柔和弥散阴影 `0 12px 32px rgba(0,0,0,0.06)`。
- **绑定的 9 张官方博客素材**：
  1. Gemini 3.8 Flash：`/assets/image/blog/3.8-Flash---Square.png`
  2. Gemini 3.7 Flash：`/assets/image/blog/3.7-Flash---Square.jpg`
  3. AGY Enterprise：`/assets/image/blog/AGY-Enterprise---Square.png`
  4. Custom Agents in Plugins：`/assets/image/blog/Custom_Agents_in_Plugins_1x1.png`
  5. IDE Extensions：`/assets/image/blog/IDE-Extensions-Square.png`
  6. Remote Control：`/assets/image/blog/remote-control-square.png`
  7. Teamwork with AI：`/assets/image/blog/teamwork-square.jpg`
  8. Visualizing with Antigravity：`/assets/image/blog/visualizing-with-antigravity-square.png`
  9. VS Code Integration：`/assets/image/blog/VSC-Blog-1x1.png`

---

### 3.7 Download Section (标志性暗夜沉浸黑卡)

#### 结构与功能要点
这是整个页面**情绪与心理反转的终极高潮点**：
- **底板表面**：`background: #121317; border-radius: 36px;`，纵向超大内边距 `padding-block: 280px;`（移动端 180px）。
- **文字反转**：
  - 大标题：`color: #f8f9fc; font-size: 72px; font-weight: 450;`
  - 副文本：`color: #b2bbc5; font-size: 20px;`
- **反转纯白药丸按钮 (`button-primary-inverse`)**：
  - `background: #ffffff; color: #121317; border-radius: 9999px; padding: 12px 32px;`
  - 悬停：`background: #eff2f7;`
- **平台支持**：提供 Windows、macOS (Apple Silicon / Intel)、Linux 的一键下载入口。

#### 关键 DOM 片段
```html
<section class="download-section-container" id="download-section" data-download-section>
  <div class="download-section">
    <div class="download-section-backdrop"></div>
    <div class="download-section-content">
      <h2 class="display-6xl text-inverse">Experience liftoff with Antigravity</h2>
      <p class="body-lead text-inverse-variant">Download the next-generation agent-first engineering platform.</p>
      <div class="download-section-cta">
        <a href="#download-windows" class="button button-primary-inverse">
          <span class="symbol">download</span>
          <span>Download for Windows</span>
        </a>
        <a href="#download-all" class="button button-secondary-inverse">
          <span>All Platforms</span>
        </a>
      </div>
    </div>
  </div>
</section>
```

---

### 3.8 Footer (多栏底部链接与法律信息)

#### 结构与功能要点
- **布局**：顶部 1px 细线分隔（`border-top: 1px solid rgba(33, 34, 38, 0.06);`）。
- **内容组织**：产品链接（Overview, Features, Pricing）、开发者生态（Docs, API, GitHub）、法律与隐私（Privacy Policy, Terms of Service）。
- **语言切换器**：右下角药丸下拉菜单，文字与 Google 经典灰色相契合。

---

## 四、 核心交互逻辑与实现代码 (Core Interactive Mechanics)

若 Agent 需编写或注入纯原生 JavaScript 以独立实现核心动效，以下提供开箱即用的轻量级实现范式：

### 4.1 磁吸智能光标 (Smart Custom Cursor)
```javascript
export function initCustomCursor() {
  const triggerArea = document.querySelector('[data-video-trigger]');
  const cursor = document.querySelector('[data-custom-cursor]');
  if (!triggerArea || !cursor) return;

  let mouseX = 0, mouseY = 0;
  let cursorX = 0, cursorY = 0;

  triggerArea.addEventListener('mouseenter', () => {
    cursor.style.opacity = '1';
    cursor.style.transform = 'scale(1)';
  });

  triggerArea.addEventListener('mouseleave', () => {
    cursor.style.opacity = '0';
    cursor.style.transform = 'scale(0)';
  });

  triggerArea.addEventListener('mousemove', (e) => {
    const rect = triggerArea.getBoundingClientRect();
    mouseX = e.clientX - rect.left;
    mouseY = e.clientY - rect.top;
  });

  function render() {
    cursorX += (mouseX - cursorX) * 0.15; // 缓动插值跟随
    cursorY += (mouseY - cursorY) * 0.15;
    cursor.style.transform = `translate3d(${cursorX}px, ${cursorY}px, 0)`;
    requestAnimationFrame(render);
  }
  requestAnimationFrame(render);
}
```

### 4.2 Logo 桌面级右键菜单 (Context Menu)
```javascript
export function initLogoContextMenu() {
  const logo = document.querySelector('[data-logo-link]');
  const menu = document.querySelector('[data-logo-context-menu]');
  if (!logo || !menu) return;

  logo.addEventListener('contextmenu', (e) => {
    e.preventDefault();
    menu.classList.add('is-open');
    menu.setAttribute('aria-hidden', 'false');
  });

  document.addEventListener('click', (e) => {
    if (!menu.contains(e.target)) {
      menu.classList.remove('is-open');
      menu.setAttribute('aria-hidden', 'true');
    }
  });

  const copyBtn = menu.querySelector('[data-context-action="copy-logo"]');
  if (copyBtn) {
    copyBtn.addEventListener('click', async () => {
      const svgCode = logo.querySelector('svg').outerHTML;
      await navigator.clipboard.writeText(svgCode);
      const label = copyBtn.querySelector('.item-label');
      const originalText = label.textContent;
      label.textContent = 'Copied to Clipboard!';
      setTimeout(() => {
        label.textContent = originalText;
        menu.classList.remove('is-open');
      }, 1500);
    });
  }
}
```

---

## 五、 Resources 资产字典与 1:1 映射表 (Asset Manifest & Mapping)

在 `resources/` 资产包内共包含 **56 个核心文件，总大小约 47.11 MB**。以下是其对应的映射字典：

| 资产相对路径 | 文件类别 | 对应页面组件 / DOM 节点 | 引用方式与作用 |
| :--- | :--- | :--- | :--- |
| `assets/fonts/GoogleSymbols.ttf` | 矢量字体 (33.5MB) | 全局图标、光标徽章、按钮箭头 | 由 `fonts.css` 声明为 `font-family: "Google Symbols"` |
| `assets/fonts/fonts.css` | 样式表 | `<head>` 全局加载 | 本地字体声明 |
| `assets/video/hero_video.mp4` | MP4 视频 (3.36MB) | `.landing-video-section video` | 首屏产品核心演示视频 (支持 206 流式分发) |
| `assets/video/landing/an-ai-ide-core.mp4`| MP4 视频 (1.87MB) | `.feature-explorer-section` | 特性视听演示插片 |
| `assets/image/antigravity-logo.png` | PNG 图片 | Header Logo 备用、Favicon 备用 | 品牌高清标识 |
| `assets/image/antigravity-cursor.png` | PNG 图片 | 自定义光标备用素材 | 首屏悬浮标识 |
| `assets/image/landing/antigravity-cli.png`| PNG 图片 | 特性区块：CLI 命令行展示卡片 | 产品界面高清截图 |
| `assets/image/landing/feature-3.jpg` | JPG 图片 | 特性区块：协同网络展示卡片 | 产品界面高清截图 |
| `assets/image/landing/landing-thumbnail-enterprise.jpg` | JPG 图片 | 用例区块：企业级场景卡片 | 场景展示图 |
| `assets/image/landing/landing-thumbnail-frontend.jpg` | JPG 图片 | 用例区块：前端工程场景卡片 | 场景展示图 |
| `assets/image/landing/landing-thumbnail-fullstack.jpg` | JPG 图片 | 用例区块：全栈研发场景卡片 | 场景展示图 |
| `assets/image/product/new-chat.png` | PNG 图片 | 特性区块：智能对话面板 | 界面截图 |
| `assets/image/sitecards/sitecard-default.png` | PNG 图片 | HTML `<head>` OpenGraph / Twitter Card | 社交分享卡片 |
| `assets/image/blog/*.png / *.jpg` (共 9 张)| 图片列表 | `.landing-latest-blogs` 卡片网格 | 官方博客 3 列封面图 |
| `assets/textures/icons/icon_cube.png` | PNG 纹理 | `MainParticlesComponent` | WebGL / Canvas 零重力粒子贴图 |
| `_astro/BaseLayout.BS3t_nql.css` | 生产 CSS (36KB) | 全局基准重置、排版、栅格样式 | 官方完整样式系统基础层 |
| `_astro/SmoothScrollLayout.D7KgMQYn.css`| 生产 CSS (15KB) | 平滑滚动层容器样式 | 官方视差滚动样式 |
| `_astro/index.BMvyDU_X.css` | 生产 CSS (9KB) | 首页特有模块样式 | 落地页定制样式 |
| `_astro/*.js` (全套 24 个脚本) | ES 模块运行时 | GSAP 动效、Draggable、Particles 粒子 | 官方打包的全套前端运行时脚本 |
| `icons/favicon.ico` | 网站图标 | `<link rel="icon">` | 浏览器标签图标 |
| `template/index.html` | 单页 HTML 骨架 | 项目入口 `index.html` | 100% 官方渲染完成的落地页基准结构 |
| `manifest.json` | 机器可读元数据 | 自动化解析脚本 | 完整的包含全部 56 个文件的哈希与尺寸清单 |

---

## 六、 零上下文 Agent 100% 复现核对清单 (Acceptance Checklist)

当 Agent 完成页面组装与启动后，必须逐条对照此验收清单进行自检：

### 1. 基础架构与运行状态
- [ ] 页面在 `http://localhost:3000/` 无报错拉起，控制台无阻塞性 Uncaught Error。
- [ ] 视频资源（`assets/video/hero_video.mp4`）支持 HTTP 206 Partial Content 流式传输，播放流畅且可拖动进度条。
- [ ] `favicon.ico` 及根目录图标正常显示。

### 2. 视觉一致性 (Pixel-level Fidelity)
- [ ] **字体表现**：标题正确呈现 Google Sans Flex，字重为 **450**，字号 $\ge 24\text{px}$ 的标题均带有 **负字距 (Tracking)**。
- [ ] **色彩阶梯**：背景纯净清爽，严格遵循 13 档微冷 Slate Greys；无脏污粗阴影。
- [ ] **几何轮廓**：
  - 核心视听大卡为 **36px** 宏观圆角；
  - 所有按钮均为 **9999px** 纯胶囊药丸轮廓；
  - 容器描边为极淡透明度（6% 炭黑细线）。
- [ ] **暗夜反转黑卡**：页面底部的 Download Section 成功切换为深邃纯黑（`#121317`），且内部按钮反转为纯白药丸。

### 3. 核心交互与动效表现 (Interactions & Motion)
- [ ] **Logo 右键菜单**：在 Header Logo 上点击右键，能够弹出 16px 圆角磨砂菜单，并支持一键复制 SVG。
- [ ] **磁吸光标**：鼠标移入视频大卡区域时，系统光标隐藏，显示白色药丸跟随光标（带 Google Symbols 播放图标）。
- [ ] **打字机光标**：首屏副标处光标具有 `0.5s` 闪烁动效。
- [ ] **Slider 轮播**：用例卡片组支持左右箭头点击切换及平滑拖动。
- [ ] **响应式适配**：在 375px（手机）、768px（平板）、1440px（桌面）各断点下，栅格与间距均自适应伸缩无溢出。

---

> 🎯 **复现成果宣告**：满足上述所有清单项即代表 **100% 成功复现 Google Antigravity 官方展示落地页**。

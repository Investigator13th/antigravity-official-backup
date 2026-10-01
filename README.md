# Google Antigravity 官方展示页归档 & 设计系统规范

> **Google Antigravity (Official Archive & Design System Specification)**  
> 高保真离线归档 Google 官方面向下一代智能体协作工程（Agent-First Engineering）的平台级展示页，内置原生流媒体静态服务与工业级设计规范文档。

---

## 🌟 项目亮点

- **完整离线归档**：完整封装着陆页 HTML、Astro 构建产物、Google Sans Flex 变量字体、Google Symbols 矢量图标库及全套演示视频。
- **高性能原生服务**：内置轻量原生 Node.js HTTP 静态服务器（[`server.js`](file:///c:/Users/huang/Documents/Antigravity/antigravity-official-backup/server.js)），零第三方重型依赖，原生支持视频流式传输（HTTP 206 Partial Content Range）与路径防穿越校验。
- **工业级设计系统规格**：内含机器可读与人类可读兼备的 [`DESIGN-antigravity.md`](file:///c:/Users/huang/Documents/Antigravity/antigravity-official-backup/DESIGN-antigravity.md) 详细设计规范文档（含 13 档 Slate Greys 阶梯、36px 宏观柔润圆角、9999px 药丸交互与反重力物理隐喻）。

---

## 📁 目录结构

```text
antigravity-official-backup/
├── _astro/                      # Astro 静态打包产物（编译后的 CSS / JS 资源）
├── assets/                      # 离线静态多媒体资产
│   ├── fonts/                   # Google Sans Flex、Google Symbols 等高精度字体
│   ├── images/                  # 界面截图、图标与位图资源
│   └── videos/                  # 高清产品演示视频（支持 206 流式分段传输）
├── DESIGN-antigravity.md        # 完整设计规范系统与 Design Tokens 规范文档
├── index.html                   # 官方展示落地页单页入口
├── package.json                 # 项目元数据与启动脚本定义
├── pnpm-lock.yaml               # 依赖锁定文件
├── server.js                    # 原生 Node.js 静态文件与视频流分发服务
└── README.md                    # 项目说明文档
```

---

## 🚀 快速启动

### 运行环境
- Node.js >= 18.0.0
- 包管理器：`pnpm`

### 1. 安装依赖（可选）
本项目基于原生 Node.js 构建，如需管理脚本可直接执行：
```bash
pnpm install
```

### 2. 启动本地服务
```bash
# 使用 pnpm 启动
pnpm dev

# 或者直接使用 Node.js 原生运行
node server.js
```

服务启动后，在浏览器访问：
```text
http://localhost:3000
```

> **提示**：可通过环境变量自定义端口，例如 `$env:PORT=8080; node server.js`（PowerShell）或 `PORT=8080 node server.js`。

---

## 🎨 设计系统速览 (Design System)

详细规范请参阅 [`DESIGN-antigravity.md`](file:///c:/Users/huang/Documents/Antigravity/antigravity-official-backup/DESIGN-antigravity.md)。

- **排版引擎**：以 `Google Sans Flex` 为核心，精细调节 `opsz`（视觉尺寸）与 `wght`（权重 400 ~ 700）。
- **色彩调色板**：纯粹单色克制（13 档 Slate Greys），搭配纯正 Google 经典电光蓝（`#3279f9`）作为核心交互锚点。
- **物理悬浮形态**：
  - 核心大卡：`36px` 柔润大倒角（`--shape-corner-xl: 36px`）
  - 行动按钮：`9999px` 全胶囊药丸轮廓（Pill Control）
  - 背景材质：`5px ~ 16px` 光学高斯毛玻璃与透光层

---

## 📄 版权与免责声明

- 本仓库所有官方页面结构、文案、字体及视觉素材版权归 **Google LLC** 所有。
- 本项目仅供技术归档、前端工程学习与设计系统研究之用，请勿用于商业用途。

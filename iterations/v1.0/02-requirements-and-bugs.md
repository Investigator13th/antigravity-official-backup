# 📋 迭代 v1.0 · 需求与 BUG 清单及根因澄清 (Triage & Clarification)

> **当前阶段**：环节 2（逐点澄清与清单转化）  
> **审批状态**：【待用户审核确认】  
> **关联诉求**：`iterations/v1.0/01-user-request.md` 及图 1 ~ 4

---

## 📌 问题 1：页脚品牌去 Antigravity 化与联系方式更新 (图 1)

### 1.1 移除页脚巨幅 Antigravity 矢量字符
- **定性归类**：`[需求 / 视觉重构]`
- **根因分析**：当前页面 `<footer>` 包含 `#antigravity-footer-wrapper`，内置了一个宽 1297px 的原生 SVG 巨幅描边字标，并由 `AntigravityFooter.astro...js` 绑定微动效。
- **原因说明**：该字标为原版官方展示页的品牌强资产，作为 Felix Huang 的个人主页，该巨幅字符不仅占位过高（270px），且严重混淆个人品牌主权。
- **预期交付标准**：
  - 彻底移除 `antigravity-footer-wrapper` 及其内部的 SVG 节点；
  - 检查并确保相关脚本 `AntigravityFooter.astro...js` 移除或静默安全降级，不抛出 JS 控制台报错；
  - 页脚整体垂直空间恢复紧凑、留白舒适。

### 1.2 底部版权信息清理
- **定性归类**：`[需求 / 文案调整]`
- **根因分析**：此前在 `.footer-google-links` 内配置了 `© 2026 Felix Huang · Built with Google Antigravity Engine`。
- **原因说明**：该小字非法律或系统必须项，且带有 Antigravity 字样。
- **预期交付标准**：
  - 精简为纯净个人版权：`© 2026 Felix Huang`，彻底清除所有 Antigravity 痕迹。

### 1.3 页脚导航（Navigation）去除中文保留纯英文
- **定性归类**：`[需求 / 视觉微调]`
- **根因分析**：此前在页脚中间列配置了带中文的跳转标签（如 `Academia · 教育经历`、`Experience · 核心实战` 等）。
- **预期交付标准**：
  - 4 个导航锚点统一修改为纯英文：`Academia` (`#academia`)、`Experience` (`#experience`)、`Projects` (`#projects`)、`Contact` (`#contact`)。

### 1.4 Email 路由与 WeChat 联系方式更新
- **定性归类**：`[需求 / 核心信息更新]`
- **预期交付标准**：
  - Email 链接修改为 `mailto:huangfei503@163.com`，展示文案为 `Email: huangfei503@163.com`（请确认是否为 163.com，诉求原文写 1633.com）；
  - WeChat 展示文案与复制脚本更新为 `FelixHuang0713`，点击按钮或链接一键复制到剪贴板。

---

## 📌 问题 2：Contact 暗夜黑卡定位文案重塑 (图 2)

### 2.1 合作标语与方向文案替换
- **定性归类**：`[需求 / 文案与定位调整]`
- **根因分析**：当前模块 09（`#contact`）副文案为通用的“兼具商业洞察与全栈代码能力。期待就 AI PM / FDE 机会...”，信息密度较低。
- **预期交付标准**：
  - 保持原版 3D 粒子流光环与主标打字机 `Let's Build the Future Together.` 不变；
  - 副文案精准替换为用户的核心定位与目标方向（双段工整排版）：
    > 兼具商业背景、产品思维与全栈代码能力。关注 Agent Memory、AI2B 落地应用的前沿进展。  
    > 目标方向：B 端 AI 产品经理（电商/金融等行业 AI 应用）、内部提效 AI 产品经理（办公、Data、Coding Agent）、FDE。

---

## 📌 问题 3：Projects 模块项目替换与重大交互修复 (图 3)

### 3.1 替换为 3 个真实自研项目并提炼精炼简介
- **定性归类**：`[需求 / 内容重构]`
- **预期交付标准**：
  1. **项目 1: Take a walk**
     - 标题：`Take a walk`
     - 标语/短简介：`反内耗出门工具 · React+FastAPI 融合腾讯 LBS 与 DeepSeek，真实 POI 与静默降级抗幻觉，根据心理状态给出出行建议。`
     - 作品外链：`https://takeawalk.huangfei7273.xyz/` (开新标签页跳转)
  2. **项目 2: Troupe**
     - 标题：`Troupe`
     - 标语/短简介：`Agents 展台项目 · 基于 DeepSeek Harness 与 Open-Harness，以多 Agent 形式具象化展示个人工作流与提效 Skills。`
     - 作品外链：`https://huangfei7273.xyz/` (开新标签页跳转)
  3. **项目 3: Anchor**
     - 标题：`Anchor`
     - 标语/短简介：`面向产品经理的 PM Harness（开发中） · Slogan: "Coding Harness 让程序员敢让 Agent 改代码；Product Harness 让 PM 敢让 Agent 深度参与产品决策"`
     - 作品外链：状态标签标注 `In Development`

### 3.2 修复大图左下角文字重叠/乱码 BUG
- **定性归类**：`[BUG 修复]`
- **根因定位与分析**：
  - 在当前 `slider-copy-wrapper` 结构中，原版使用了 GSAP `fromTo` 控制 `data-copy-index`。
  - 当前代码中，未激活项与激活项的容器缺少独立的定位上下文或隐藏属性（如未激活项应该 `display: none` 或 `position: absolute; opacity: 0; pointer-events: none`），导致三张卡片底部的文字（`AI NATIVE & FULL-STACK` 等）在同一个物理流中叠合挤压，产生视觉重叠与“乱码”假象。
- **预期交付标准**：
  - 彻底解决重叠现象，确保滑动到第 N 项时，仅清晰渲染对应的项目简介，其余未激活项完全不可见且不占据物理空间。

### 3.3 修复底部居中左右箭头无法点击切换轮播 BUG
- **定性归类**：`[BUG 修复]`
- **根因定位与分析**：
  - 原版 `UseCases.astro...js` 依赖 `SliderHelper` 监听 `[data-arrow-left]` 和 `[data-arrow-right]`。
  - 当前在改造 HTML 时，部分父级容器层级（z-index）或事件穿透样式（`pointer-events`）导致控制按钮虽然渲染，但被上层的透明占位图层或视口拦截，点击事件无法穿透到底部按钮；或者由于 `disabled` 属性判断锁死导致左右点击失效。
- **预期交付标准**：
  - 确保左右箭头具备独立的 `z-index: 10` 与 `pointer-events: auto`；
  - 确保与 `SliderHelper` 的滑动与循环切换无缝绑定，点击左/右箭头滑块顺滑滑动，左右键翻页流畅。

### 3.4 替换 Antigravity 原版外国人肖像大图
- **定性归类**：`[视觉资产替换]`
- **根因分析**：当前使用的是原版 Google 团队成员的肖像（黑人小哥与亚裔青年大头照），与用户个人主页完全不搭。
- **预期交付标准**：
  - 移出人物照片；
  - 替换为极简、极具科技质感的**贝塞尔曲线/流动矢量线框插图（Dark Minimalist SVG / Canvas）**，或与项目主题契合的高级纯色抽象线稿，保持卡片大圆角与高级感。

---

## 📌 问题 4：标题层级精简与极简微质感分割线 (图 4)

### 4.1 精简 Experience 模块标头
- **定性归类**：`[视觉重构 / 标题精简]`
- **预期交付标准**：
  - 移除原版过重的两层冗余标头 `Professional Experience`；
  - 仅保留极简大气的 `核心实战经历` 标题，间距与呼吸感对齐原版。

### 4.2 Projects 模块标头重构为【Personal Projects】
- **定性归类**：`[视觉重构 / 标题精简]`
- **预期交付标准**：
  - 删除原版冗长复杂的 `Featured Projects ## 精选自研与实战工程 **Evaluation Frameworks · Compilers...`；
  - 替换为极其精炼的单行标题：**`Personal Projects`**；
  - 彻底删除右侧多余的长句副文案（`以确定性交付为准绳，兼具全栈工程与提示词编译能力...`），恢复 Google 极简设计呼吸感。

### 4.3 引入微质感极细分割线 (Subtle Divider)
- **定性归类**：`[视觉质感调优]`
- **根因分析**：图 4 蓝框中有一条极细微、高质感的分割线（`rgba(33, 34, 38, 0.08)` 或 `rgba(255, 255, 255, 0.06)` 的微光线），赋予页面极强的段落节奏感。
- **预期交付标准**：
  - 在 `Academia`（教育经历）与 `Experience`（实战经历）之间，以及相关主模块过渡处，注入完全一致的 1px 微质感居中分割线，提升模块呼吸感与层次感。

---

### 🛑 阻断审批点 (Approval Required)
请您审核以上《需求与 BUG 清单及根因澄清》。若您确认无误，请回复“**认可清单，开始撰写技术方案**”，我将立即进入**环节 3**深入代码层输出详尽的《技术实施方案》！

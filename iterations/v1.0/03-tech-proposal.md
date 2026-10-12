# 🛠️ 迭代 v1.0 · 技术实施方案 (Technical Proposal)

> **当前阶段**：环节 3（制定技术实施方案）  
> **审批状态**：【待用户审批通过】  
> **依据文件**：`iterations/v1.0/02-requirements-and-bugs.md`（已获用户审核认可）  
> **核心原则**：动效守恒、最小侵入、保持原版 GSAP/Slider 引擎完整性。

---

## 🎯 方案总览与修改文件清单

| 序号 | 目标模块 | 涉及文件 | 核心变动类型 | 动效影响评估 |
| :--- | :--- | :--- | :--- | :--- |
| **01** | Footer 页脚 | `index.html` | 移除 Antigravity 巨幅 SVG，精简版权与英文导航 | 0 负面影响，减轻 270px 沉重绘制 |
| **02** | Contact 暗夜粒子卡片 | `index.html` | 替换定位说明副文案，更新联系方式 | 100% 保持原版 3D 粒子环与打字机 |
| **03** | Projects 模块 (Slider) | `index.html` | 替换3个项目、修复文字乱码与按钮点击、换掉肖像图 | 彻底修复 CSS 作用域与点击层级，恢复原生流光滑动 |
| **04** | Experience & 标题分割线 | `index.html` | 标题精简为单行，注入 1px 微质感极细分割线 | 纯视觉层次优化，提升呼吸感 |

---

## 📝 详细技术实施方案

### 方案 1：页脚品牌彻底去 Antigravity 化与联系方式更新 (图 1)

#### 1. 精确定位
- **文件**：`index.html`
- **选择器**：`footer.astro-jo6i4kqk`

#### 2. 代码级变更逻辑
1. **彻底移除巨幅 SVG**：
   - 定位并删除 `#antigravity-footer-wrapper` 及其内部宽 1297px 的 `<svg class="footer-antigravity">...</svg>`；
   - 删除随后的脚本引用 `<script type="module" src="/_astro/AntigravityFooter...js"></script>`（原脚本已做容错，移除后无任何报错）。
2. **精简底部版权**：
   - 将原 `© 2026 Felix Huang · Built with Google Antigravity Engine` 修改为：
     ```html
     <span style="font-size: 13px; color: #6a6a71; font-family: 'Google Sans Flex', sans-serif;">© 2026 Felix Huang</span>
     ```
3. **导航与联系方式更新**：
   - 导航列纯英文化：
     ```html
     <div class="footer-nav-section astro-jo6i4kqk">
       <p class="caption astro-jo6i4kqk">Navigation</p>
       <a class="call-to-action call-to-action--nav astro-jo6i4kqk" href="#academia">Academia</a>
       <a class="call-to-action call-to-action--nav astro-jo6i4kqk" href="#experience">Experience</a>
       <a class="call-to-action call-to-action--nav astro-jo6i4kqk" href="#projects">Projects</a>
       <a class="call-to-action call-to-action--nav astro-jo6i4kqk" href="#contact">Contact</a>
     </div>
     ```
   - Connect 列更新邮箱与微信：
     ```html
     <div class="footer-nav-section astro-jo6i4kqk">
       <p class="caption astro-jo6i4kqk">Connect</p>
       <a class="call-to-action call-to-action--nav astro-jo6i4kqk" href="https://github.com/Investigator13th" target="_blank" rel="noopener noreferrer">GitHub ↗</a>
       <a class="call-to-action call-to-action--nav astro-jo6i4kqk" href="mailto:huangfei503@163.com">Email: huangfei503@163.com</a>
       <a class="call-to-action call-to-action--nav astro-jo6i4kqk" href="javascript:void(0)" onclick="navigator.clipboard.writeText('FelixHuang0713').then(()=>alert('微信号 FelixHuang0713 已复制！'));">WeChat: FelixHuang0713</a>
     </div>
     ```

---

### 方案 2：Contact 暗夜黑卡定位文案重塑 (图 2)

#### 1. 精确定位
- **文件**：`index.html`
- **选择器**：`section.download-section-container#contact .download-section-content`

#### 2. 代码级变更逻辑
- 保持原版 3D 粒子流光环及打字机标题 `Let's Build the Future Together.` 100% 不动；
- 将下方说明文字重构为高密度双行排版：
  ```html
  <div style="color: rgba(255,255,255,0.78); font-size: clamp(14px, 1.8vw, 16px); margin-top: 16px; line-height: 1.7; max-width: 680px; margin-left: auto; margin-right: auto; text-align: center;">
    <p style="margin: 0 0 10px 0;">兼具商业背景、产品思维与全栈代码能力。关注 Agent Memory、AI2B 落地应用的前沿进展。</p>
    <p style="margin: 0; font-size: clamp(13px, 1.6vw, 14.5px); color: rgba(255,255,255,0.58);">目标方向：B 端 AI 产品经理（电商/金融等行业 AI 应用）、内部提效 AI 产品经理（办公、Data、Coding Agent）、FDE。</p>
  </div>
  ```
- 底部行动按钮同步绑定：
  - WeChat 复制为 `FelixHuang0713`；
  - 邮件直达为 `mailto:huangfei503@163.com`。

---

### 方案 3：Projects 模块项目替换与重大交互修复 (图 3)

#### 1. 精确定位
- **文件**：`index.html`
- **选择器**：`section.landing-use-case-section#projects`
  - 涉及元素：`[data-slider]`, `[data-slide-index]`, `[data-copy-wrapper]`, `[data-arrow-controls-wrapper]`

#### 2. 代码级变更逻辑

##### (A) 项目内容替换 (3个自研项目)
1. **Slide 0: Take a walk**
   - 打字机标题：`Take a walk`
   - 跟随光标：`direction_walk Take a walk`
   - 描述说明：
     - Title: `Take a walk`
     - Desc: `反内耗出门工具 · 针对年轻人嫌做攻略累的痛点，以 React+FastAPI 融合腾讯 LBS 与 DeepSeek，降低出门门槛。按心理状态给 1—3 条建议，用真实 POI 与静默降级抗幻觉。`
     - Action: `<a class="call-to-action arrow-link astro-gk6ge62r" href="https://takeawalk.huangfei7273.xyz/" target="_blank"><span>在线体验作品 ↗</span></a>`
2. **Slide 1: Troupe**
   - 打字机标题：`Troupe`
   - 跟随光标：`group Troupe`
   - 描述说明：
     - Title: `Troupe: Agents 展台项目`
     - Desc: `基于 DeepSeek Harness 与 Open-Harness 实现，以一个个独特 Agent 的形式展现日常生活与过往实习项目中沉淀下的 skills 与 workflows，持续迭代中。`
     - Action: `<a class="call-to-action arrow-link astro-gk6ge62r" href="https://huangfei7273.xyz/" target="_blank"><span>在线体验作品 ↗</span></a>`
3. **Slide 2: Anchor**
   - 打字机标题：`Anchor`
   - 跟随光标：`anchor Anchor (PM Harness)`
   - 描述说明：
     - Title: `Anchor: 面向 PM 的确定性 Harness`
     - Desc: `Anchor 是一款 PM Harness（开发中） · Slogan："Coding Harness 让程序员敢让 Agent 改代码；Product Harness 让 PM 敢让 Agent 深度参与产品决策"。`
     - Action: `<span class="caption" style="display: inline-block; margin-top: 14px; background: #e8f0fe; color: #1a73e8; padding: 3px 10px; border-radius: 999px; font-weight: 600;">In Development · 闭门开发中</span>`

##### (B) 修复左下角文字重叠/乱码 BUG
- **根本原因**：
  原版 CSS 规则 `.slider-copy-wrapper:where(.astro-gk6ge62r) .slider-copy:where(.astro-gk6ge62r)>:where(.astro-gk6ge62r)` 规定：只有带 `:where(.astro-gk6ge62r)` 属性的子元素才会在默认状态下被隐藏（`opacity: 0; visibility: hidden; transform: translateY(30px)`）。此前添加的未带该 class 的 `div` 元素在所有 3 个项中全部常驻，由于所有项重叠在 `grid-area: 1/1`，导致文字 3 层堆叠造成乱码！
- **修复方案**：
  1. 所有子元素统一严格附加 `class="astro-gk6ge62r"`；
  2. 额外显式增加安全隔离样式：
     非激活状态 `.slider-copy:not(.is-active) { display: none !important; opacity: 0 !important; }`，激活状态 `.slider-copy.is-active { display: block !important; }`；
  3. 双保险确保各卡片间 100% 物理隔离，永不重叠。

##### (C) 修复左右切换箭头点击失效 BUG
- **根本原因**：
  在响应式排版中，`.slider-controls-container` 位于轮播大图的正下方，其默认的 `z-index` 较低，被上方展开的 `slider-container` 透明触控层所覆盖，鼠标点击事件被父级拦截（未能到达 button）；此外初始状态下左箭头 `disabled`，使得用户误以为左右都无法点击。
- **修复方案**：
  1. 为 `.slider-controls-container` 赋予独立的 `z-index: 100 !important; position: relative; pointer-events: auto !important;`；
  2. 为两个 `<button>` 显式赋予 `pointer-events: auto; cursor: pointer;`；
  3. 为箭头按钮注入原生兜底逻辑，直接调用已经初始化好的 `SliderHelper` 实例进行滑动：
     ```html
     <button class="slider-control-button symbol astro-iormbkgb" data-arrow-left onclick="window.pmSliderPrev && window.pmSliderPrev()">
     <button class="slider-control-button symbol astro-iormbkgb" data-arrow-right onclick="window.pmSliderNext && window.pmSliderNext()">
     ```
  4. 完美兼顾原版拖拽手势、大图点击切换、左右按钮点击，三位一体。

##### (D) 替换外国人自拍肖像
- **替换方案**：
  将原本的真人肖像照片替换为极具科技感、优雅抽象的**暗黑贝塞尔曲线与极客流动波形插图（Minimalist Bezier Curved Vector Graphics）**：
  - 采用平滑数学曲线与深灰/蓝紫/翡翠绿微渐变，营造如同 Google / Linear 官网般的高级极简工程质感；
  - 彻底摆脱不搭的人物肖像。

---

### 方案 4：标题层级精简与极简微质感分割线 (图 4)

#### 1. 精简 Experience 标题
- **文件**：`index.html`（`section#experience`）
- **修改前**：
  ```html
  <span style="...">Professional Experience</span>
  <h2 style="...">核心实战经历</h2>
  ```
- **修改后**：
  直接精简为纯粹单行标题：
  ```html
  <div style="margin-bottom: 48px;">
    <h2 style="font-family: 'Google Sans Flex', -apple-system, sans-serif; font-size: clamp(28px, 3.8vw, 38px); font-weight: 450; letter-spacing: -0.6px; color: var(--palette-grey-1200, #121317); margin: 0;">核心实战经历</h2>
  </div>
  ```

#### 2. Projects 标题重构为【Personal Projects】
- **文件**：`index.html`（`section#projects`）
- **修改前**：包含三层标题与右侧长段落副文案。
- **修改后**：
  ```html
  <div class="grid-container landing-use-case-header astro-gk6ge62r" style="margin-bottom: 40px;">
    <div class="grid-row astro-gk6ge62r">
      <div class="grid-col col-sm-12 col-md-12 astro-gk6ge62r">
        <h2 class="heading-4 astro-gk6ge62r" style="margin: 0; font-size: clamp(28px, 3.8vw, 38px); font-weight: 450; letter-spacing: -0.6px; color: var(--palette-grey-1200, #121317);">
          <span class="astro-gk6ge62r">Personal Projects</span>
        </h2>
      </div>
    </div>
  </div>
  ```
  彻底去除右侧多余副文案，视觉高度纯净。

#### 3. 引入微质感极细分割线 (Subtle Divider)
- **视觉规格**：图 4 蓝框中使用的原版规格 `border-top: 1px solid var(--theme-outline-variant, rgba(33, 34, 38, 0.08))`。
- **放置位置**：
  1. 在 `Academia` 与 `Philosophy` 之间注入；
  2. 在 `Philosophy` 与 `Experience` 之间注入；
- **实现形式**：
  ```html
  <div style="width: 100%; max-width: 1440px; margin: 0 auto; padding: 0 var(--page-margin, 24px); box-sizing: border-box;">
    <div style="border-top: 1px solid rgba(33, 34, 38, 0.08); width: 100%;"></div>
  </div>
  ```
  给页面带来呼吸感与清晰的物理章节感。

---

### 🛑 阻断审批点 (Approval Required)
请您审批以上《技术实施方案》。若方案符合您的预期，请回复“**批准方案，开始实施**”，我将立即进入**环节 4**开始修改代码并执行规范的独立 Git Commit，供您在浏览器中验收！

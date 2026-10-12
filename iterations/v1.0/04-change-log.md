# 📋 迭代 v1.0 · 变更日志 (Change Log)

> **迭代版本**：v1.0（全站体验精修与问题修复）  
> **实施状态**：已完成实施，待用户肉眼验收  
> **变更时间**：2026-10-12  
> **依据技术方案**：`iterations/v1.0/03-tech-proposal.md`  

---

## 📌 变更汇总表

| 序号 | 模块 | 变更类型 | 修改文件 | 核心变动与收益 |
| :--- | :--- | :--- | :--- | :--- |
| **01** | Footer 页脚 | `[BUG修复/去品牌化]` | `index.html` | 彻底移除 1297px Antigravity 巨幅 SVG 与脚本；精简版权为 `© 2026 Felix Huang`；导航英文化；联系方式更新为 `huangfei503@163.com` 与微信 `FelixHuang0713`。 |
| **02** | Contact 暗夜黑卡 | `[需求/文案重构]` | `index.html` | 保留原版 3D 粒子流光环与打字机动效；重构双段高密度定位文案（聚焦 Agent Memory、AI2B，目标 B 端 AI PM / 提效 AI PM / FDE）；更新微信复制与邮件链接。 |
| **03** | Projects 模块 (Slider) | `[BUG修复/动效恢复]` | `index.html`<br>`assets/image/landing/*.svg` | ① 标题精简为 `Personal Projects`；<br>② 上线 3 个自研项目（`Take a walk`、`Troupe`、`Anchor`）；<br>③ 换掉外国肖像照，采用 3 张暗黑极客高精度贝塞尔流光矢量图；<br>④ 挂载 `UseCases.astro...js` 脚本并赋权按钮层级，恢复左右箭头点击与拖拽联动；<br>⑤ 注入 scoped 类名与样式物理隔离，彻底根治左下角 3 层文字重叠乱码。 |
| **04** | Experience & 标题分割线 | `[视觉/层次调优]` | `index.html` | ① Experience 标题精简为纯粹单行《核心实战经历》；<br>② 在 `Academia`、`Philosophy`、`Experience` 各章节间注入 1px 微质感极细微光分割线（`rgba(33, 34, 38, 0.08)`），提升页面呼吸感。 |

---

## 🔍 代码级详细变更点

### 1. 页脚去品牌化与联系方式更新
- 删除 `#antigravity-footer-wrapper` 及其内宽 1297px 的 `<svg class="footer-antigravity">` 和 `AntigravityFooter` 脚本引用；
- 底部版权精简为：
  ```html
  <span style="font-size: 13px; color: #6a6a71; font-family: 'Google Sans Flex', sans-serif;">© 2026 Felix Huang</span>
  ```
- 导航链接更新为纯英文：`Academia`, `Experience`, `Projects`, `Contact`；
- Connect 模块邮箱更新为 `huangfei503@163.com`，微信号更新为 `FelixHuang0713`。

### 2. Contact 暗夜黑卡文案重塑
- 保留 3D 粒子流光环及打字机标题 `Let's Build the Future Together.`；
- 说明文字更新为：
  > 兼具商业背景、产品思维与全栈代码能力。关注 Agent Memory、AI2B 落地应用的前沿进展。  
  > 目标方向：B 端 AI 产品经理（电商/金融等行业 AI 应用）、内部提效 AI 产品经理（办公、Data、Coding Agent）、FDE。
- CTA 按钮微信号绑定复制 `FelixHuang0713`，邮件唤起 `huangfei503@163.com`。

### 3. Projects 模块修复与项目替换
- **标题精简**：单行标题 `<h2 class="heading-4"><span>Personal Projects</span></h2>`；
- **三个项目上线**：
  1. `Take a walk: 反内耗出门工具`（React + FastAPI · 腾讯 LBS · DeepSeek，带在线体验链接 `https://takeawalk.huangfei7273.xyz/`）；
  2. `Troupe: Agents 展台项目`（DeepSeek Harness · Open-Harness，带在线体验链接 `https://huangfei7273.xyz/`）；
  3. `Anchor: 面向 PM 的确定性 Harness`（PM Harness · Deterministic Eval，带 `In Development · 闭门开发中` 标签）；
- **质感视觉资产**：在 `assets/image/landing/` 产出并应用 3 张符合 Linear / Google 官网质感的暗黑贝塞尔流光矢量图（`project-takeawalk.svg`、`project-troupe.svg`、`project-anchor.svg`）；
- **交互与文字乱码根治**：
  - 引入了原版缺失的 `UseCases.astro_astro_type_script_index_0_lang.u0DwWsgt.js` 驱动脚本；
  - 为所有子元素补齐 `astro-gk6ge62r` 属性选择器；
  - 在全局注入 `#slider-text-safeguard`，强制非激活项 `display: none !important; opacity: 0 !important;`，彻底避免 3 层文字物理堆叠；
  - 为左右切换按钮设置 `z-index: 100 !important; pointer-events: auto; cursor: pointer;`。

### 4. 章节微质感分割线与标题层级精简
- 在 `Academia` 与 `Philosophy` 之间、以及 `Philosophy` 与 `Experience` 之间注入原版规制极细分割线：
  ```html
  <div style="width: 100%; max-width: 1440px; margin: 0 auto; padding: 0 var(--page-margin, 24px); box-sizing: border-box;">
    <div style="border-top: 1px solid rgba(33, 34, 38, 0.08); width: 100%;"></div>
  </div>
  ```
- 将 Experience 顶部的双层冗长标头精简为纯粹单行标题。

---

## 🚀 验收指引 (Sign-off Guide)
本地开发服务常驻于：`http://localhost:3000/`  
请在浏览器中肉眼验收以下 4 处：
1. **页面底部 Footer**：巨幅 SVG 是否已彻底消失？版权是否为 `© 2026 Felix Huang`？邮箱与微信是否已更新？
2. **Contact 暗夜黑卡**：说明文字是否准确呈现双段定位文案？点击复制微信号是否为 `FelixHuang0713`？
3. **Projects 模块**：
   - 标题是否为简洁的 `Personal Projects`？
   - 3 张轮播图是否已替换为暗黑极客科技矢量流光图（无外国人自拍肖像）？
   - 左下角文字是否清晰独立、绝无乱码叠字？
   - 点击右箭头（或拖拽大图、点击大图）是否能丝滑平移切换、打字机和文字入场动画是否自然？
4. **分割线与标题**：Experience 标题是否为纯粹单行？章节间是否有极细微光分割线？

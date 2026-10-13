# 🛠️ 迭代 v1.1 · 代码级技术实施方案 (Technical Proposal)

> **当前阶段**：环节 3（制定技术实施方案）  
> **审批状态**：【待用户审批通过】  
> **关联依据**：[01-user-request.md](./01-user-request.md) 与已确认清单 [02-requirements-and-bugs.md](./02-requirements-and-bugs.md)  
> **动效与准则**：严格遵循 [AGENTS.md](../../AGENTS.md) 的“动效守恒与最小侵入原则”及“双阻断审批流程”

---

## 📑 实施方案全局概览

| 诉求编号 | 涉及模块 | 文件路径 | 变更性质 | 核心技术路径 |
| :--- | :--- | :--- | :--- | :--- |
| **诉求 1** | 全站矢量图形 | `assets/image/vector/` & `index.html` | `[视觉资产轻量化]` | 绘制纯内联 SVG 贝塞尔曲线与像素网格线条画，替代大位图 |
| **诉求 2** | 导航平滑滚动 | `index.html` | `[动效/交互调优]` | 注入 GSAP `power3.out` 缓动代理，实现“先快后慢、缓缓停靠”的物理加速度 |
| **诉求 3** | Contact 模块 | `index.html` (L1334-1340) | `[视觉/交互增强]` | 文字左对齐、文案更新；构建 WeChat 二维码毛玻璃弹窗；邮件双重兜底协议 |
| **诉求 4** | 个人项目卡片 | `index.html` (L1180-1330) | `[组件重构]` | 重构为一体化大卡片横向轮播；左文字+右线画+线性透明渐变；Anchor 弹 Toast；控制器居中 |
| **诉求 5** | 核心实战经历 | `index.html` (L737-850) | `[结构精简/STAR重排]` | 删除标题与分割线；落点精准校准；隐藏推演按钮；重构为 2 段实习 4 个项目 STAR 徽章 |
| **诉求 6** | 学业与科研 | `academia-sandbox.html` & `index.html` | `[沙盒开发/动效修复]` | 根治 ScrollTrigger `center center` 屏幕中央 1.0 动效；独立沙盒实现 3D 翻转卡片与双轨时间轴 |

---

## 🧩 逐项技术实施细节

### 1. 诉求 1：轻量化矢量图形/贝塞尔曲线画方案 (SVG 矢量引擎)

#### 1.1 资产设计定位
告别笨重、高成本的位图制作，结合项目具体业务逻辑，通过纯 SVG 矢量代码实现一套极简现代工程风线条画：
1. **Take a walk**：腾讯 LBS 路径拓扑 + 心理状态波动贝塞尔波形曲线（`M0,100 C150,20 300,180 450,80 S600,120`）；
2. **Troupe**：多 Agent 协作网络（Agent Mesh）蜂窝节点与数据流向脉冲线条；
3. **Anchor**：PM Harness 确定性评测双环靶心与三元状态机流转连线；
4. **同花顺数据 Agent 语义层**：上千金融底表抽象矩阵网格 + 汇聚至核心 Wiki 语义层节点的流动曲线；
5. **同花顺指标治理与 AI 提效**：多阶段 workflow 筛选管道 + 80人天降至4人天的量化阶梯折线；
6. **一知智能 AI 直播互动系统 2.0**：音画直播推流时序波形 + 弹幕长短期记忆与多轮上下文索引流；
7. **一知智能纯 AIGC 直播搭建**：数字人持品模特骨架线 + 多模态 SOP 流水线节拍图。

#### 1.2 动效与样式契合
- 统一采用透明背景与精细描边（`stroke-width="1.5"`，色彩使用科技蓝 `#1a73e8`、墨灰 `#202124`、淡绿 `#34a853`，带细微 `stroke-dashoffset` 流动动效）；
- 零外部 HTTP 请求，完全内联，保障页面首屏秒开。

---

### 2. 诉求 2：顶部导航点击平滑滚动加速度调优

#### 2.1 代码定位与根因
- **位置**：`_astro/SmoothScrollLayout.astro...js` 与 `index.html`；
- **现状**：原有 ScrollSmoother 点击仅做了简单插值，持续时间较短（约 0.6s），缺少“高加速度冲刺、末段缓缓吸附”的高级流体质感。

#### 2.2 核心逻辑变更方案
在 `index.html` 注入专用的 **GSAP 物理平滑滚动调度器**：
- 监听所有顶部导航栏链接（`#academia`、`#experience`、`#projects`、`#contact` 等）；
- 核心算法实现：
  ```javascript
  document.querySelectorAll('a[href^="#"]').forEach(anchor => {
    anchor.addEventListener('click', function(e) {
      const targetId = this.getAttribute('href');
      if (targetId === '#' || targetId === '') return;
      const targetElement = document.querySelector(targetId);
      if (!targetElement) return;

      e.preventDefault();
      const offset = 76; // 顶部导航避让高度
      const targetY = targetElement.getBoundingClientRect().top + window.pageYOffset - offset;
      const smoother = window.ScrollSmootherInstance;

      // 使用 GSAP 驱动高阶物理减速缓动
      const scrollProxy = { y: smoother ? smoother.scrollTop() : window.pageYOffset };
      gsap.to(scrollProxy, {
        y: targetY,
        duration: 1.25, // 从容舒展的滑行周期
        ease: "power3.out", // 关键：前段高加速度掠过，后段缓缓减速柔和靠泊
        overwrite: "auto",
        onUpdate: () => {
          if (smoother) smoother.scrollTop(scrollProxy.y);
          else window.scrollTo(0, scrollProxy.y);
        }
      });
      history.pushState(null, '', targetId);
    });
  });
  ```
- **决策理由**：通过 GSAP 驱动 ScrollSmoother 代理，100% 保持原有页面 ScrollTrigger 视差动效的同步更新，同时赋予完美的物理加速度与优雅靠泊手感。

---

### 3. 诉求 3：Contact 模块排版、文案与交互闭环

#### 3.1 代码精确定位
- **文件**：`index.html`
- **行数**：第 1334 行至第 1340 行

#### 3.2 变更方案
1. **两段中文文本左对齐**：
   - 将行 1334 容器样式中的 `text-align: center;` 修改为 `text-align: left;`，并设置 `margin-left: 0;`。
2. **第二段中文文案校准**：
   - 替换为：`目标岗位：B 端 AI 产品经理（行业 AI 应用、办公/Data/Coding Agent）、FDE`。
3. **按钮文案调整**：
   - `💬 加微信交流 (点击复制)` 修改为 `💬 加微信交流`；
   - 保持 `✉️ 发起邮件对话`。
4. **加微信悬浮二维码弹窗 (WeChat Modal)**：
   - 将 `iterations/v1.1/assets/wechat-qr.jpg` 部署至公共资源目录 `assets/image/contact/wechat-qr.jpg`；
   - 在 `index.html` 尾部挂载毛玻璃弹窗容器：
     ```html
     <div id="wechat-qr-modal" class="custom-modal-backdrop" style="display:none; position:fixed; inset:0; z-index:9999; background:rgba(0,0,0,0.65); backdrop-filter:blur(16px); justify-content:center; align-items:center;">
       <div class="custom-modal-card" style="background:#ffffff; border-radius:28px; padding:32px 28px; max-width:320px; width:88%; text-align:center; box-shadow:0 24px 64px rgba(0,0,0,0.28); position:relative;">
         <button type="button" onclick="closeWechatModal()" style="position:absolute; top:16px; right:16px; border:none; background:none; cursor:pointer; font-size:20px; color:#5f6368;">✕</button>
         <h4 style="margin:0 0 16px 0; font-size:18px; color:#121317; font-weight:550;">微信交流</h4>
         <img src="/assets/image/contact/wechat-qr.jpg" alt="WeChat QR Code" style="width:200px; height:200px; border-radius:16px; object-fit:contain; border:1px solid rgba(0,0,0,0.06);">
         <p style="margin:16px 0 8px 0; font-size:14px; color:#45474d;">微信号：<strong>FelixHuang0713</strong></p>
         <button type="button" onclick="copyWechatId()" class="button button-primary button-compact" style="margin-top:8px; width:100%; justify-content:center;"><span>一键复制微信号</span></button>
       </div>
     </div>
     ```
   - 包含平滑淡入缩放动效（GSAP/CSS 缓动）、ESC 键退出及点击外部遮罩退出。
5. **邮件对话双重兜底防失效**：
   - 点击时执行原有 `mailto:huangfei503@163.com`，同时自动拷贝邮箱地址到剪贴板，并触发轻量 Toast：“已复制邮箱 huangfei503@163.com，正在尝试呼起邮件应用...”，彻底消除 Windows 无默认邮件客户端时的困惑。

---

### 4. 诉求 4：个人项目改版为大卡片轮播（左文字 + 右渐变线画）

#### 4.1 代码精确定位
- **文件**：`index.html`
- **行数**：第 1180 行至第 1330 行（Projects 模块）

#### 4.2 组件架构重构
原版左右分栏（左 8 列图、右 4 列文字）改造为**一体化大卡片横向轮播轴 (Unified Carousel Track)**：
1. **大卡片尺寸与圆角**：
   - 宽度自适应（单张卡片占满视口主容器宽，宽屏约 1080px ~ 1160px），高度约为 460px ~ 500px；
   - 遵循 Antigravity 官方 `36px` 宏观圆角（`border-radius: var(--shape-corner-xl, 36px)`）。
2. **左文字 + 右图示 + 线性透明渐变**：
   - **左侧内容区（占宽约 54%）**：
     - 左上角：项目大标（`Take a walk` / `Troupe` / `Anchor`）与分类徽章；
     - 中部：精炼介绍文案与架构标签；
     - 下部：行动链接按钮；
     - 实色底背景（100% 不透明度），确保文字极高辨识度与阅读体验；
   - **右侧图示区（占宽约 46%）**：
     - 嵌入诉求 1 的专属轻量贝塞尔线条/像素画；
   - **线性渐变遮罩**：
     - 叠加由左至右平滑过渡渐变：
       `linear-gradient(90deg, #ffffff 45%, rgba(255,255,255,0.85) 65%, rgba(255,255,255,0) 100%)`；
       使左侧文字区完全纯白清晰，向右平滑渐融至完全透明，展露右侧纯净科技线条。
3. **点击逻辑与 Toast**：
   - 卡片 1（Take a walk）：跳转 `https://takeawalk.huangfei7273.xyz/`；
   - 卡片 2（Troupe）：跳转 `https://huangfei7273.xyz/`；
   - 卡片 3（Anchor）：点击触发原生胶囊 Toast，提示：
     > **“Anchor 项目紧密开发中，敬请期待！”**
4. **居中控制器**：
   - 左右切换箭头移至轮播轨道正下方居中排列（`margin: 28px auto 0 auto; display: flex; justify-content: center;`）；
   - 保留原版平滑翻页脚本与禁用态逻辑。

---

### 5. 诉求 5：【核心实战经历】结构精简、落点校准与 STAR 标准化重构

#### 5.1 代码精确定位
- **文件**：`index.html`
- **行数**：第 737 行至第 850 行

#### 5.2 实施步骤
1. **清理小标题与分割线**：
   - 彻底删除第 737 行 `<div style="border-top: 1px solid rgba(33, 34, 38, 0.08)...">`；
   - 彻底删除第 743 行 `<h2 ...>核心实战经历</h2>`；
   - 将原 Section 的 `padding-top: 72px` 压缩为 `padding-top: 24px`，保持与打字机标题的紧凑舒适过渡。
2. **Experience 导航跳转锚点重定位**：
   - 在打字机大标下方、第一段实习卡片上方安放锚点容器：
     `<div id="experience" style="position: relative; top: -64px; visibility: hidden;"></div>`；
   - 使得点击导航后，视口自然聚焦在实习正文，打字机标头作为视觉背景自然衬托。
3. **隐藏深度推演与架构按钮**：
   - 移除/隐藏【案例深度推演 · Deep Dive】按钮与二级弹窗触发器。
4. **重构为 2 段实习、4 个核心项目 STAR 矩阵**：
   - **实习段 1**：浙江核新同花顺网络信息股份有限公司（同花顺｜金融大数据终端 AI 产品经理｜2026.05-至今）
     - **项目 1：数据 Agent 语义层建设**
       - `<tag class="star-badge bg-blue">背景</tag>` 面对上千张金融底表、脚本与业务规则查数瓶颈，核心卡点在缺少业务语义层；
       - `<tag class="star-badge bg-indigo">选型</tag>` 综合准确性、可追溯性与成本对比 RAG、知识图谱与 Wiki，推动 Wiki Skill 落地与模型选型；
       - `<tag class="star-badge bg-green">成果</tag>` 搭建 50+ 条真实问句多维评测闭环，Bad Case 针对性调优校验，**基准得分由 58.0 提升至 81.5（+40.5%）**。
     - **项目 2：金融数据指标治理与 AI 提效**
       - `<tag class="star-badge bg-blue">背景</tag>` 数据浏览器 PM 日常事项繁杂依赖人工，指标体系分类混乱、竞品覆盖不足；
       - `<tag class="star-badge bg-amber">行动</tag>` 结合数据 Agent 沉淀提效方法论，高频场景落地 10+ Skills；
       - `<tag class="star-badge bg-green">攻坚</tag>` 对齐竞品 2,000+ 指标，设计多阶段匹配 workflow 解决匹配幻觉；落地 PRD 生成 Skill，推动 **100+ 新增指标交付由 80 人天降至 4 人天（20x）**。
   - **实习段 2**：杭州一知智能科技有限公司（一知智能｜直播数字人产品经理｜2026.01-2026.05）
     - **项目 1：AI 直播互动系统 2.0**
       - `<tag class="star-badge bg-blue">背景</tag>` 数字人直播互动在多 SKU 与多轮复杂问答场景下表现不佳；
       - `<tag class="star-badge bg-purple">导购</tag>` 针对张冠李戴优化主体识别与上下文索引，推动被动客服向智能导购升级；
       - `<tag class="star-badge bg-green">成果</tag>` 设计长期记忆与画像机制；千条评测集驱动问答合理率提升 54pct；23 个直播间灰度，**场均停留时长提升 39%，跨期 GPM 提升 17%**。
     - **项目 2：纯 AIGC 直播搭建**
       - `<tag class="star-badge bg-blue">背景</tag>` 海外大客户希望实现纯 AIGC 生成持品数字人模特用于直播带货；
       - `<tag class="star-badge bg-amber">行动</tag>` 拆解比例失调与长时耗材卡点，从零搭建 AIGC 直播 SOP 并落地可复用 Skill；
       - `<tag class="star-badge bg-green">成果</tag>` 内部盲测得分超竞品 19%，产出素材击败 3 家竞品成功签单。
5. **右侧图示轻量化**：
   - 4 个项目右侧分别匹配诉求 1 的专属轻量矢量线条画，保留左右分栏的原版优雅对齐。

---

### 6. 诉求 6：【学业与科研】卡片重构、独立沙盒与动效彻底根治

#### 6.1 主站文案与滚动缩放动效根治
1. **标题文案更新**：
   - `index.html` 第 167 行：修改为 `学业与科研`。
2. **ScrollTrigger 动效根因根治**：
   - 原版在 `_astro/YoutubeVideoSection...js` 中配置了 `end: 'top center'`，导致滚动露出约 30% 时卡片 scale 就已经达到 1.0；
   - **精准重构方案**：
     在 `index.html` 注入覆盖逻辑（或重载 ScrollTrigger）：
     ```javascript
     gsap.fromTo(".academia-carousel-card", 
       { scale: 0.84, opacity: 0.8 }, 
       {
         scale: 1.0,
         opacity: 1.0,
         ease: "power2.out",
         scrollTrigger: {
           trigger: ".academia-carousel-card",
           start: "top 90%", // 当卡片顶部进入视口底部时启动
           end: "center center", // 核心修复：恰好处在屏幕正中央时才达到 1.0 满尺寸
           scrub: 1.2
         }
       }
     );
     ```
     确保卡片在向上滚动时持续平滑放大，只有当卡片正好处在屏幕视口正中央时才恢复为 1.0 大小！

#### 6.2 独立沙盒文件：`academia-sandbox.html`
遵照用户明确要求“【学业与科研】这个卡片，请单独建一个Index修改，后续再合并”：
- **文件创建**：在根目录下创建 `academia-sandbox.html`；
- **核心组件功能**：
  1. **3D 翻转卡片 (Flip Card)**：
     - 正反两面结构（`transform-style: preserve-3d; transition: transform 0.8s cubic-bezier(0.16, 1, 0.3, 1);`）；
     - 正面：江南大学（本科，2020.09 – 2024.08）；
     - 反面：东南大学（硕士）；
     - 右上角胶囊切换动效按钮：“点击翻转查看硕士经历 ↻ / 翻转回本科经历 ↺”；
  2. **本科阶段双轨时间轴 (Dual-Track Timeline)**：
     - **主线时间轴（绿色 `#34a853`）**：
       2020.09 至 2024.08（工商管理主修）；
     - **支线时间轴（蓝色 `#1a73e8`）**：
       从 2021.09 节点平滑分叉而出（信息与计算科学辅修）；
     - **交互手感**：时间节点支持 Hover 悬浮激活，平滑展开抽屉卡片显示详细项目、省级大创、竞赛与获奖成果；
  3. **校徽水印融合**：
     - 分别将 `iterations/v1.1/assets/jiangnan-logo.png` 与 `iterations/v1.1/assets/seu-logo.png` 作为正反两面的右侧柔和透明渐变水印底纹；
- **验收方式**：用户在本地 `http://localhost:3000/academia-sandbox.html` 独立体验与肉眼验收，满意后再合并至主页。

---

## 🛡️ 动效守恒与最小侵入原则评估

1. **原版动效完整性**：
   - 彻底保留终端打字机引擎、SplitText 字符流光、3D 粒子流光环与光标跟随系统；
   - 新增的滚动加速度与弹窗动效统一遵循 Google / Apple 级弹簧与减速曲线（`cubic-bezier(0.16, 1, 0.3, 1)` 与 `power3.out`）。
2. **零引入重量级外部库**：
   - 充分利用页面已有的 GSAP 核心库与原生 CSS3，不额外引入无谓的三方包；
   - 矢量图示全部内联，杜绝图片加载阻塞。

---

## 🚦 阻断审批点 (Sign-off)

按照 `AGENTS.md` 严格四环节 SOP：
- 当前为 **环节 3（制定技术实施方案）**；
- **【阻断等待】请用户审批本实施方案**；
- 审批通过后，Agent 将进入 **环节 4：精准手术刀式代码实施与独立 Git Commit**。

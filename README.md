# From LLM to Agent — OpenClaw Lecture Slides

> 使用 Claude Code 制作的单文件 HTML 演示文稿，面向设计专业学生讲授「从 LLM 到 Agent」的概念演进。

**在线预览**: [GitHub Pages](https://yate-ge.github.io/openclaw-lecture-202603/)

![28 slides](https://img.shields.io/badge/slides-28%20pages-00E8C6) ![HTML](https://img.shields.io/badge/tech-single%20file%20HTML-0A0A0A) ![commits](https://img.shields.io/badge/commits-58-blue)

---

## 这是什么

这是一个用 **Claude Code** 从零到一制作演示文稿的完整示范项目。核心产出是一个 3400+ 行的单文件 HTML（`index.html`），包含 28 页 slides，所有 CSS、JavaScript、SVG 图表和动画全部内嵌，零外部依赖，双击即可打开。

### Slides 内容

为设计学本科/研究生讲授「从 LLM 到 Agent — 以交互设计视角理解 OpenClaw」：

| Part | 主题 | 内容 |
|------|------|------|
| **Part 1** | 从 LLM 到 CLaw | LLM → Chatbot → Agent → OpenClaw 的技术演进，配有逐步动画图表 |
| **Part 2** | 设计机会与挑战 | 主动交互、记忆与自适应、终端用户编程、多端协同、人-Agent 共生 |
| **Part 3** | 实例：Temi 机器人 | OpenClaw + Temi 机器人的真实应用场景 |

---

## 方法论：Claude Code + 单文件 HTML

### 为什么选择这个方案

- **零依赖**：不需要 reveal.js、Marp 等框架，任何浏览器直接打开
- **AI 友好**：单文件 = Claude Code 可以直接读写全部内容，无需跨文件协调
- **高度可控**：CSS 动画、SVG 图表、p5.js 粒子效果，想要什么就加什么
- **离线可用**：p5.js 已内联，完全不依赖网络

### 工作流程

```
1. 准备内容底稿（Markdown）
2. 用 CLAUDE.md 定义设计规范（配色、字体、布局、动画）
3. 配置 frontend-slides skill（slides 制作的通用规范）
4. 用 Claude Code 逐步生成 HTML slides
5. 每次修改立即 commit（极细粒度版本控制）
6. 反复迭代：预览 → 调整 → commit
```

### 关键：CLAUDE.md 是设计系统

`CLAUDE.md` 定义了完整的设计规范，使 Claude Code 在每次生成新 slide 时保持一致的设计语言：

- **配色**：暗色主题 `#0A0A0A` + 强调色 `#00E8C6`，5 级灰度文字层级
- **字体**：DM Sans（英文）+ Noto Sans SC（中文）+ DM Mono（代码）
- **布局模式**：split / vs-split / v-center / columns / flow-row
- **动画库**：breathe / heartbeat / orbit-spin / bubble-float 等
- **内容约束**：每页 100vh，overflow hidden，可用高度约 500-550px

### 关键：frontend-slides Skill

自定义 Claude Code skill，封装了 slides 制作的通用最佳实践：零依赖原则、Viewport Fitting 强制要求、字体配色审美指导、动画模式模板。下次做新 slides 可直接复用。

---

## 技术亮点

| 特性 | 实现方式 |
|------|---------|
| 粒子动画封面 | p5.js（已内联，支持离线） |
| 架构图与流程图 | Inline SVG + SMIL animate + CSS @keyframes |
| 图标 | Lucide-style 线条 SVG（stroke, no fill） |
| 响应式字号 | 全部使用 CSS `clamp()`，无断点 media query |
| 导航 | 键盘方向键 / 空格 / URL hash 路由 / TOC 面板 / 进度条 |
| 噪点纹理 | SVG feTurbulence 叠加，增强质感 |

---

## 开发过程

跨 2 天，约 12 小时，58 次 git commit：

| 阶段 | 时间 | 关键产出 |
|------|------|---------|
| 骨架搭建 | 03-16 凌晨 | 内容底稿 + 基础 HTML + skill 配置 |
| Part 1 图表 | 03-16 晚间 | 4 大演进 SVG 动画 + Agent Loop 架构图 |
| Part 2 扩展 | 03-17 凌晨 | 主动交互、记忆、EUD、多端 + 学术案例 |
| 收尾 | 03-17 上午 | 真实图片替换 + 离线支持 + favicon |

### 踩过的坑

1. **内容溢出**：100vh + overflow hidden，内容多了直接被截断 → 在 CLAUDE.md 中明确高度约束，内容过多时拆页
2. **SVG 图表迭代**：OpenClaw 架构图重做了 5-6 次（线条连接 → orbit → grid → 竖向堆叠）→ 复杂可视化需要多次试错
3. **file:// CORS**：双击打开 HTML 时 p5.js CDN 加载失败 → 将 p5.js 完整内联
4. **设计一致性**：28 页 slides 容易风格飘移 → CLAUDE.md 定义 CSS 变量 + 统一 class

---

## 经验总结

1. **CLAUDE.md 是项目灵魂** — 越详细越好，配色、字号、动画、约束都写清楚
2. **极细粒度 commit** — 57 次 commit，每次只改一个功能点，任何改动都可回溯
3. **迭代 > 一步到位** — SVG 图表平均迭代 3-5 次，slide 顺序调整至少 5 次
4. **单文件架构适合一次性演示** — 部署简单、AI 操作方便，但 3000+ 行后期定位需要耐心
5. **真实素材 > AI 生成插图** — 学术案例和产品展示用真实图片更有说服力
6. **用 Skill 封装方法论** — 可复用的 Claude Code 能力包，下次直接用

---

## 使用方式

```bash
# 直接双击打开（已支持离线）
open index.html

# 或启动本地服务器
python3 -m http.server 8080
# 访问 http://localhost:8080/index.html
```

**导航操作**：
- `←` `→` 方向键 或 `空格` 翻页
- 左上角汉堡菜单打开目录
- URL hash 支持直接跳转：`#/0`, `#/1`, ...

---

## 项目结构

```
├── index.html                 # 核心产出：28 页单文件 HTML slides
├── openclaw-slides-202603.md  # 原始 Markdown 内容底稿
├── CLAUDE.md                  # Claude Code 设计规范（配色/字体/布局/动画）
└── assets/                    # 图片资源
    ├── claw.png               # OpenClaw logo
    ├── temiRobot.png          # Temi 机器人
    ├── cocobo-*.jpg           # Cocobo 案例图
    ├── genfaceui-*.png/jpg    # GenFaceUI 案例图
    ├── docko-*.png            # Docko 案例图
    └── wx.jpg                 # 微信二维码
```

---

## License

MIT

# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

这是一个**讲课用 slides 项目**。核心产出是一个单文件 HTML 演示文稿（`presentation.html`），用于大学课堂讲授 AI Agent 概念，面向设计专业本科生和研究生。

**主题**: 从 LLM 到 Agent — 以交互设计视角理解 OpenClaw 的架构与设计启发。

**核心文件**: `presentation.html` — 完整的 HTML slides，包含所有样式、动画、SVG 图表和导航逻辑。

**辅助文件**:
- `openclaw-slides-202603.md` — 原始 Markdown 版本的内容底稿（Obsidian 格式）
- `assets/` — 图片资源（claw.png 等）

## Slides 内容结构

当前共 23 页（data-index 0-22），分为三个 Part：

1. **Part 1** — 从 LLM 到 CLaw：技术演进与本质
   - 封面（p5.js 粒子动画背景）
   - 目录
   - Part 1 标题页
   - LLM → Chatbot → Agent → 六大核心组件 → OpenClaw（车库比喻）→ Workspace & Context → Agent Loop
2. **Part 2** — OpenClaw 启发的设计机会点与挑战
   - 主动交互、记忆、终端用户编程、多端交互、范式对比、设计挑战
3. **Part 3** — 实例：OpenClaw + Tami 机器人（有 TODO 待填充）
4. **参考资料 + Thank you**

## 设计规范

### 主题与配色
- **暗色主题**，背景 `#0A0A0A`
- **强调色**: `#00E8C6`（青绿），用于高亮、边框、图标、动画
- 文字层级: `#FFFFFF`（标题）→ `#E0E0E0`（正文）→ `#888888`（次要）→ `#666666`（辅助）→ `#2A2A2A`（分割线/底色）

### 字体
- **英文/数字**: `DM Sans`（正文）、`DM Mono`（代码/标签）
- **中文**: `Noto Sans SC`
- 字号使用 `clamp()` 响应式：h1 `clamp(28px, 4vw, 56px)`、h2 `clamp(20px, 2.6vw, 36px)`、正文 `clamp(13px, 1.4vw, 16px)`

### 图表与图示
- 使用 **inline SVG** 绘制架构图和流程图（不用外部图片）
- 图标风格: **Lucide-style** 线条 SVG path（stroke, no fill），统一 stroke-width 1-1.5
- 动画使用 **SVG SMIL animate** + **CSS @keyframes**
- 图表在 `.slide.active` 时播放动画，非活动页暂停
- 图表配色与主题一致：accent 绿用于核心/Agent 元素，灰色用于传统/辅助元素

### 常用动画
- `core-breathe`: 核心圆轻微缩放呼吸
- `heartbeat-pulse`: 心跳脉动
- `action-ring`: 向外扩散的脉冲环
- `orbit-spin`: 工具节点环绕旋转
- `memory-rotate`: 记忆环缓慢旋转
- `bubble-float`: 聊天气泡上浮
- 粒子背景: p5.js，带随机微弱波纹（仅封面页）

### 布局模式
- `.split` — 左右两栏（左文字右图）
- `.vs-split` / grid 对比 — 左 Traditional vs 右 Agent Mode
- `.v-center` — 垂直居中单栏
- `.columns-5` / `.columns-6` — 等宽多列网格
- `.flow-row` — 水平流程图

### 导航
- 键盘方向键 / 空格翻页
- URL hash 路由 `#/0`, `#/1`, ...（支持直接跳转和书签）
- 左上角 TOC 面板（汉堡按钮）
- 底部进度条 + 页码

## 开发注意事项

- 语言: **中文**（普通话）。所有内容编辑保持中文。
- 本地预览需启动 HTTP 服务器（`python3 -m http.server 8080`），不可直接 file:// 打开（p5.js CORS 限制）。
- **每次修改后立即 git commit**，不要攒到最后。
- 单文件架构：所有 CSS、JS、SVG 都内嵌在 `presentation.html` 中，不拆分。
- Part 3 的 Tami 机器人部分有未完成的 TODO 待填充技术细节。

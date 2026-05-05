# math-ppt-html

> 零依赖，纯 HTML/CSS/JS 即可生成专业数学幻灯片。一个 教学Skill，输入主题即可获得交互式课件。

<p align="center">
  <img src="https://img.shields.io/badge/platform-browser-blue" alt="Platform">
  <img src="https://img.shields.io/badge/dependencies-zero-green" alt="Dependencies">
  <img src="https://img.shields.io/badge/license-MIT-yellow" alt="License">
  <img src="https://img.shields.io/badge/Coding-Skill-orange" alt="Skill">
</p>

## 这是什么

让 Claude Code 直接帮你生成数学课件——不是 PPTX 文件，而是可以在浏览器中打开的**纯静态网页**，支持：

- **PPT 式分页浏览**：← → 翻页、T 键缩略图、F 键全屏、触摸滑动
- **KaTeX 数学公式渲染**：所有公式排版级显示
- **交互式 2D/3D 可视化**：基于 Plotly.js，支持旋转/缩放/参数调节
- **深色/浅色主题切换**：深色护眼，浅色适合投影

不需要安装 Python、Node.js、LaTeX 或任何运行时——生成的 `.html` 文件双击即开。

## 快速开始

1. 在 Claude Code 中安装本 Skill
2. 说一句话即可：

```
帮我做曲面方程的课件
生成线性变换的数学幻灯片
可视化展示傅里叶级数
```

3. 生成的课件在 `workspace/学习/{分类}/{主题名}/` 下，用浏览器打开 `index.html`

也可以直接提供 `.pptx` 文件让 AI 转化，或列出知识点让它自动组织。

## 技术栈

| 组件 | 方案 | 加载方式 |
|------|------|----------|
| 公式渲染 | [KaTeX](https://katex.org) v0.16.9 | CDN |
| 2D/3D 图形 | [Plotly.js](https://plotly.com) v2.27.0 | CDN |
| 动画 | 纯 CSS `@keyframes` + `transition` | 零依赖 |
| 导航逻辑 | 原生 JavaScript | 零依赖 |

## 支持的数学主题

- 函数与极限、微分学、积分学
- 多元函数、曲面方程、空间曲线
- 线性代数（矩阵变换、特征向量可视化）
- 概率分布与统计推断
- 微分方程（方向场、相平面）
- 无穷级数（部分和逼近动画）

详细的可视化模式见 [references/visualization-patterns.md](references/visualization-patterns.md)。

## 项目结构

```
workspace/学习/{分类}/{主题名}/
├── index.html          # 主幻灯片文件
├── css/slides.css      # 样式（含深色/浅色主题）
├── js/
│   ├── slides.js       # 翻页/导航/动画逻辑
│   └── math-viz.js     # Plotly.js 可视化封装
└── assets/images/      # 插图资源
```

## 设计理念

- **零运行时依赖**：不调用 Python、Node.js 或任何脚本，AI 直接写文件
- **内容优先**：卡片式排版，定义/定理/例题/警告各有专属样式
- **渐进交互**：推导步骤可逐步展开，参数滑块实时影响图形
- **开箱即用**：生成的课件是完整的独立网页，拷到任何电脑都能用

## 兼容性

Chrome / Edge / Firefox / Safari 均完整支持。移动端适配触摸滑动翻页。

## License

MIT

---
name: math-ppt-html
description: 当用户说"生成数学课件"、"帮我做数学PPT"、"数学幻灯片"、"带我学习XXX"（数学相关）或类似表达时触发。直接生成纯 HTML/CSS/JS 数学幻灯片演示文稿，具备PPT式分页浏览、KaTeX公式渲染、交互式2D/3D可视化。不依赖任何 Python、Node.js 等运行时，生成的课件是纯静态网页文件。
---

# 数学PPT生成HTML (Math Slides Generator)

将数学内容直接生成为纯 HTML + CSS + JS 幻灯片演示文稿，**不使用任何脚本语言或构建工具**。生成的文件可直接用浏览器打开。

## 触发条件

当用户说以下任意表达时触发：
- "生成数学课件XXX"
- "帮我做数学PPT XXX"
- "数学幻灯片XXX"
- "做一个XXX的PPT"
- "把XXX做成幻灯片"
- "带我学习XXX"（数学相关主题）
- "可视化展示XXX"（数学相关主题）

## 输入方式

用户可通过以下方式提供内容：
1. **指定主题**：如"帮我做曲面方程的课件" → 由 AI 根据数学知识生成内容
2. **提供 PPTX 文件**：AI 直接查看文件内容，理解其中的文字、公式、图形，然后转化为 HTML 幻灯片
3. **描述内容要点**：用户列出要讲的知识点，AI 组织成幻灯片

> **重要**：无论哪种输入方式，最终输出都是纯 HTML/CSS/JS 文件，不需要运行任何脚本。

## 工作流程

### 1. 理解数学主题

从用户输入中提取数学主题和章节信息：
- "帮我做曲面方程的PPT" → 主题：曲面及其方程，分类：高等数学
- "生成线性变换课件" → 主题：线性变换，分类：线性代数
- "做一个傅里叶级数的幻灯片" → 主题：傅里叶级数，分类：高等数学

如果用户提供了 `.pptx` 文件，直接查看并理解其中的内容结构。

### 2. 创建项目目录

在 `workspace/学习/` 下按数学分支创建分类文件夹：

```
workspace/学习/
├── 高等数学/
│   ├── 曲面及其方程/
│   ├── 微分方程/
│   └── 重积分/
├── 线性代数/
│   ├── 矩阵运算/
│   └── 特征值与特征向量/
├── 概率论与数理统计/
│   ├── 随机变量/
│   └── 概率分布/
├── 微分方程/
├── 离散数学/
└── 其他/
```

每个课件项目的目录结构：

```
workspace/学习/{分类}/{主题名}/
├── index.html          # 主幻灯片文件（所有内容在此）
├── css/
│   └── slides.css      # 幻灯片样式（深色/浅色主题）
├── js/
│   ├── slides.js       # 幻灯片导航/翻页/动画逻辑
│   └── math-viz.js     # 数学可视化（Plotly图形生成）
└── assets/
    └── images/         # 插图（如需要用generate_image生成）
```

### 3. 规划幻灯片页面

每份课件应包含以下类型的幻灯片：

| 页面类型 | 说明 |
|---------|------|
| 标题页 | 课程名称、章节编号、副标题 |
| 概念引入页 | 背景知识、问题引导、直觉说明 |
| 定义页 | 数学定义，公式用 KaTeX 渲染，配以几何直觉图 |
| 定理页 | 定理陈述 + 证明过程（可逐步展开） |
| 推导页 | 公式推导，支持逐步显示动画 |
| 例题页 | 典型例题 + 详细解题过程 |
| 可视化页 | 交互式2D/3D图形（函数图像、曲面、向量场等） |
| 练习页 | 课后思考题或练习 |
| 总结页 | 本节要点回顾 |

### 4. 直接编写 HTML/CSS/JS 文件

**所有代码由 AI 直接编写**，不调用任何外部脚本或构建工具。

#### 技术栈（仅 CDN 引用，无需安装）

```html
<!-- KaTeX 公式渲染 -->
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/katex@0.16.9/dist/katex.min.css">
<script src="https://cdn.jsdelivr.net/npm/katex@0.16.9/dist/katex.min.js"></script>
<script src="https://cdn.jsdelivr.net/npm/katex@0.16.9/dist/contrib/auto-render.min.js"></script>

<!-- Plotly.js 交互式图形 -->
<script src="https://cdn.plot.ly/plotly-2.27.0.min.js"></script>
```

> 所有依赖通过 CDN 加载，无需 npm install、pip install 或任何包管理器。

#### HTML 结构模板

```html
<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>{主题名称} - 数学课件</title>
    <!-- KaTeX -->
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/katex@0.16.9/dist/katex.min.css">
    <script defer src="https://cdn.jsdelivr.net/npm/katex@0.16.9/dist/katex.min.js"></script>
    <script defer src="https://cdn.jsdelivr.net/npm/katex@0.16.9/dist/contrib/auto-render.min.js"></script>
    <!-- Plotly.js -->
    <script src="https://cdn.plot.ly/plotly-2.27.0.min.js"></script>
    <link rel="stylesheet" href="css/slides.css">
</head>
<body>
    <!-- 幻灯片容器 -->
    <div class="slides-container" id="slidesContainer">
        <!-- 每一页是一个 .slide -->
        <div class="slide active" data-index="0">
            <div class="slide-content title-slide">
                <h1>课件标题</h1>
                <h2>章节编号 · 副标题</h2>
            </div>
        </div>
        <div class="slide" data-index="1">
            <div class="slide-content">
                <h2>定义</h2>
                <div class="card card-definition">
                    <p>公式用 KaTeX 语法: \( f(x) = ax^2 + bx + c \)</p>
                </div>
            </div>
        </div>
        <!-- 可视化页示例 -->
        <div class="slide" data-index="2">
            <div class="slide-content viz-slide">
                <h2>交互式可视化</h2>
                <div class="viz-layout">
                    <div class="viz-info">
                        <p>说明文字和公式</p>
                        <div class="param-controls">
                            <!-- 参数滑块 -->
                        </div>
                    </div>
                    <div class="viz-plot" id="plot-1"></div>
                </div>
            </div>
        </div>
        <!-- ... 更多幻灯片 -->
    </div>

    <!-- 导航控件 -->
    <nav class="slide-nav">
        <button class="nav-btn prev" id="prevBtn" aria-label="上一页">‹</button>
        <span class="page-indicator" id="pageIndicator">1 / N</span>
        <button class="nav-btn next" id="nextBtn" aria-label="下一页">›</button>
    </nav>

    <!-- 底部进度条 -->
    <div class="progress-bar"><div class="progress-fill" id="progressFill"></div></div>

    <!-- 缩略图侧栏（按 T 键切换） -->
    <aside class="thumbnail-sidebar" id="sidebar"></aside>

    <!-- 主题切换按钮 -->
    <button class="theme-toggle" id="themeBtn" aria-label="切换主题">🌙</button>

    <script src="js/slides.js"></script>
    <script src="js/math-viz.js"></script>
</body>
</html>
```

#### 幻灯片功能要求

**PPT式分页浏览（必须）：**
- 全屏幻灯片布局（16:9）
- `←` `→` 键翻页
- 页码指示器（如 3/15）
- 底部进度条
- `T` 键切换缩略图侧栏
- `F` 键全屏 / `ESC` 退出
- 触摸滑动翻页（移动端适配）

**数学公式渲染（必须）：**
- KaTeX 自动渲染：`\(...\)` 行内，`\[...\]` 独立
- 支持 `aligned`、`cases`、`matrix`、`bmatrix` 等环境
- 公式字号足够大，保证可读性

**交互式可视化（重要）：**
- 2D函数图：Plotly.js 折线/散点图，支持缩放/平移
- 3D曲面/曲线：Plotly.js `surface`/`scatter3d`，支持旋转/缩放
- 参数滑块：HTML `<input type="range">`，实时更新图形
- 无需 Three.js 等额外库，Plotly.js 足够覆盖大部分场景

**公式推导动画（加分项）：**
- 逐步显示推导（点击按钮或按空格展开下一步）
- 用 CSS class 控制显示/隐藏：`.step { opacity: 0; }` → `.step.visible { opacity: 1; }`
- 当前步骤高亮，已展开步骤变灰

**主题切换：**
- 深色模式（默认）：深色背景 + 浅色文字，护眼
- 浅色模式：白色背景 + 深色文字，适合投影

### 5. 预览课件

直接在浏览器中打开 `index.html` 即可预览。如需启动本地服务器：

```
# 在项目目录下启动（仅可选，不是必须）
npx -y serve . -p 9898
```

## 设计指南

### UI/UX 原则

1. **幻灯片布局**
   - 每页内容不宜过多，保持简洁清晰
   - 标题区域固定在顶部
   - 内容主体居中显示，适当留白
   - 公式字体足够大，确保可读性

2. **视觉设计**
   - 标题使用渐变色或醒目颜色
   - 关键公式/定理使用卡片式高亮背景
   - 定义用蓝色边框卡片 `.card-definition`
   - 定理用绿色边框卡片 `.card-theorem`
   - 注意事项用橙色 `.card-warning`
   - 例题用紫色 `.card-example`

3. **交互反馈**
   - 翻页有平滑过渡动画（CSS transition）
   - 可视化图形操作时有实时反馈
   - 参数滑块拖动时图形实时更新
   - 步骤展开有渐显动画

4. **动画设计**
   - 页面切换：CSS `transform: translateX()` + `transition`
   - 元素入场：`@keyframes fadeInUp`
   - 公式显示：逐行 `opacity` 过渡
   - 不依赖任何动画库，纯 CSS 实现

5. **色彩方案**

   **深色主题（默认）：**
   ```css
   --bg-primary: #0d1117;
   --bg-card: #161b22;
   --text-primary: #e6edf3;
   --accent-blue: #58a6ff;
   --accent-green: #3fb950;
   --accent-orange: #f0883e;
   --accent-purple: #bc8cff;
   --formula-color: #ffffff;
   ```

   **浅色主题：**
   ```css
   --bg-primary: #ffffff;
   --bg-card: #f6f8fa;
   --text-primary: #1f2328;
   --accent-blue: #0969da;
   --accent-green: #1a7f37;
   ```

### 数学可视化模式参考

| 数学主题 | 可视化方案 |
|---------|-----------|
| 函数与极限 | 2D函数图 + ε-δ动态区间 + 极限逼近动画 |
| 微分学 | 切线动画 + 导函数对照图 + 极值标注 |
| 积分学 | 黎曼和动画（矩形逼近）+ 面积着色 + 旋转体3D |
| 多元函数 | 3D曲面图 + 等高线 + 梯度向量场 |
| 曲面方程 | 3D交互曲面 + 参数滑块 + 截面显示 |
| 线性代数 | 矩阵变换动画 + 特征向量箭头 + 行列式面积变化 |
| 概率分布 | 分布曲线 + 面积计算 + 参数影响 |
| 微分方程 | 方向场 + 解曲线族 + 相平面图 |
| 级数 | 部分和逼近动画 + 收敛/发散可视化 |
| 向量分析 | 向量场箭头图 + 通量 + 散度/旋度着色 |

### 常见幻灯片模板

#### 定义/定理页模板
- 卡片式容器 + 彩色左边框
- 公式居中大号显示
- 下方附带简明文字说明
- 几何直觉图（如有）

#### 推导过程页模板
- 分步公式序列，初始仅显示第一步
- 点击/按键逐步展开后续步骤
- 当前步骤高亮，已展开步骤变灰
- 每步之间添加简短解释

#### 交互可视化页模板
- 左侧或上方：说明文字 + 公式
- 右侧或下方：Plotly.js 交互图形
- 底部：参数控制面板（滑块、按钮）
- 信息面板：当前参数值、坐标信息

#### 例题页模板
- 题目区域：带序号和题目背景
- 解答区域：可折叠/逐步展开
- 关键步骤公式高亮
- 答案用醒目颜色标注

## 目录结构

```
workspace/学习/{分类}/{主题名}/
├── index.html          # 主幻灯片文件
├── css/
│   └── slides.css      # 幻灯片样式（含深色/浅色主题）
├── js/
│   ├── slides.js       # 幻灯片导航/翻页/动画逻辑
│   └── math-viz.js     # 数学可视化（Plotly图形生成）
├── assets/
│   └── images/         # 插图（如需要）
└── README.md           # 课件说明
```

## 注意事项

1. **纯静态文件输出**：只生成 `.html`、`.css`、`.js` 文件，不生成任何 `.py`、`.sh`、`.bat` 等脚本文件
2. **CDN 依赖**：KaTeX 和 Plotly.js 通过 CDN 加载，需要网络连接；如需离线使用，下载到 `assets/` 目录
3. **浏览器兼容**：确保 Chrome / Edge / Firefox 均可正常显示
4. **性能**：3D 可视化数据点控制在 50×50 以内，避免卡顿
5. **可访问性**：幻灯片支持键盘完整导航，图形提供文字说明
6. 每次创建新课件前检查是否已存在同名项目，如存在则询问用户
7. 确保 9898 端口未被占用（如果使用本地服务器预览）

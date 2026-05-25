# 产学研小程序 - 设计规范文档

## 1. 概述

本文档定义产学研参访 Pro 应用的完整设计规范，包括视觉设计、组件、交互模式和代码实现标准。

### 1.1 设计理念

- **移动优先**：以 414px 为设计基准，最大宽度限制
- **简洁清晰**：充足的留白，清晰的视觉层次
- **卡片美学**：采用卡片式设计，圆润边角，柔和阴影
- **易读性**：严格的颜色对比度，优化字号和行距

### 1.2 技术栈

- **CSS 框架**：Tailwind CSS (CDN)
- **图标库**：Font Awesome 6.4.0
- **字体**：PingFang SC, Hiragino Sans GB, Microsoft YaHei
- **动画**：CSS animations + transitions

---

## 2. 色彩系统

### 2.1 核心色板

```css
/* 主品牌色 */
--primary: #2563eb              /* 核心蓝色 */
--primary-soft: #eff6ff         /* 浅蓝色背景 */
--primary-dark: #1d4ed8         /* 深蓝色（悬停状态） */

/* 辅助功能色 */
--success: #10b981              /* 成功/免费标签 */
--warning: #f59e0b              /* 橙色价格/强调 */
--error: #ef4444                /* 错误提示 */
--info: #3b82f6                 /* 信息提示 */

/* 中性灰度 */
--slate-50: #f8fafc             /* 最小背景 */
--slate-100: #f1f5f9            /* 卡片边框 */
--slate-200: #e2e8f0            /* 分隔线 */
--slate-300: #cbd5e1            /* 次要元素 */
--slate-400: #94a3b8            /* 次要文字 */
--slate-500: #64748b            /* 普通文字 */
--slate-600: #475569            /* 主要文字 */
--slate-700: #334155            /* 重要文字 */
--slate-800: #1e293b            /* 标题文字 */
--slate-900: #0f172a            /* 最深文字 */
--white: #ffffff
```

### 2.2 色彩使用规范

| 用途 | 颜色 | 示例 |
|------|------|------|
| 主品牌色 | `#2563eb` | 主要按钮、导航激活态、标签 |
| 成功状态 | `#10b981` | 免费标签、成功提示 |
| 警告强调 | `#f59e0b` | 价格数字、高亮信息 |
| 主标题 | `#0f172a` / `#1e293b` | H1/H2 文字 |
| 正文内容 | `#334155` / `#475569` | 描述、正文 |
| 次要信息 | `#94a3b8` | 标签说明、时间信息 |
| 背景填充 | `#f8fafc` | 页面背景、卡片背景 |
| 分隔线 | `#e2e8f0` | 边框、分割线 |

### 2.3 玻璃拟态效果

```css
/* 玻璃态背景 */
.glass-header {
  background: rgba(255, 255, 255, 0.9);
  backdrop-filter: blur(16px);
  -webkit-backdrop-filter: blur(16px);
}
```

---

## 3. 排版系统

### 3.1 字体栈

```css
font-family: "PingFang SC", "Hiragino Sans GB", "Microsoft YaHei", sans-serif;
```

**首选**：PingFang SC（苹方）- macOS 和 iOS 系统字体
**备选**：Microsoft YaHei（微软雅黑）- Windows 系统字体

### 3.2 字号层级

| 层级 | 字号 | 字重 | 行距 | 使用场景 |
|------|------|------|------|---------|
| Display | 28px | 800 | 36px | 首页主标题 (text-2xl font-black) |
| H1 | 24px | 800 | 32px | 详情页标题 (text-2xl font-black) |
| H2 | 20px | 700 | 28px | 分区标题 (text-lg font-black) |
| H3 | 18px | 700 | 24px | 卡片标题 (text-base font-bold) |
| H4 | 16px | 700 | 22px | 卡片副标题 (text-sm font-bold) |
| Body | 14px | 400 | 20px | 正文描述 (text-[12px]/text-sm) |
| Caption | 12px | 400 | 16px | 辅助文字 (text-xs) |
| Label | 10px | 600 | 14px | 标签、时间戳 (text-[10px] font-bold) |

**行距比例**：1.4 - 1.6，保证可读性

### 3.3 字重规范

- **800 (Black/Extra Bold)**：主标题、导航激活态、重点强调
- **700 (Bold)**：分区标题、卡片标题、按钮文字
- **600 (Semi Bold)**：标签、分类说明
- **500 (Medium)**：次要信息
- **400 (Regular)**：正文内容、描述文字

---

## 4. 间距与布局

### 4.1 间距单位

使用 Tailwind 的标准间距体系：

| Token | 值 | 使用场景 |
|-------|-----|---------|
| px-1 | 4px | 微调间距 |
| px-2 | 8px | 图标内边距 |
| px-3 | 12px | 标签内边距 |
| px-4 | 16px | 卡片内容、按钮间距 |
| px-5 | 20px | 多卡片间距 |
| px-6 | 24px | 页面水平内容边距 |
| px-8 | 32px | 宽屏容器边距 |
| gap-3 | 12px | 图标与文字间距 |
| gap-4 | 16px | 表单字段间距 |
| gap-5 | 20px | 卡片区块间距 |
| gap-8 | 32px | 主分区间距 |
| gap-10 | 40px | 大分区间距 |

### 4.2 容器宽度

```css
/* 手机框架限制 */
.phone-frame {
  max-width: 414px;  /* iPhone Max 宽度 */
  margin: 0 auto;
  min-height: 100vh;
}
```

### 4.3 安全区域

```css
/* 适配刘海屏 */
.safe-area-bottom {
  padding-bottom: calc(1.5rem + env(safe-area-inset-bottom));
}
```

---

## 5. 圆角系统

### 5.1 圆角规范

| 变量名 | 值 | 使用场景 |
|--------|-----|---------|
| radius-sm | 0.75rem (12px) | 按钮、标签 |
| radius-md | 1rem (16px) | 输入框、小卡片 |
| radius-lg | 1.5rem (24px) | 卡片、按钮 |
| radius-xl | 2rem (32px) | 主卡片、详情页面板 |
| radius-2xl | 2.5rem (40px) | 用户头像、圆形按钮 |
| radius-full | 9999px | 完全圆形（徽章、图标按钮） |

**常见值映射**：
- `rounded-xl` ≈ `2rem` - 卡片圆角
- `rounded-2xl` ≈ `2.5rem` - 头像外框
- `rounded-full` - 圆形元素

---

## 6. 阴影系统

### 6.1 阴影层级

```css
/* 卡片阴影 - 最常用 */
.card-shadow {
  box-shadow: 0 10px 30px -5px rgba(0, 0, 0, 0.04);
}

/* 模态/浮层阴影 */
.shadow-2xl {
  box-shadow: 0 25px 50px -12px rgba(0, 0, 0, 0.25);
}

/* 按钮按压阴影 */
.shadow-lg {
  box-shadow: 0 10px 15px -3px rgba(0, 0, 0, 0.1);
}

/* 品牌色辉光 */
.shadow-blue-100 {
  box-shadow: 0 4px 14px 0 rgba(37, 99, 235, 0.15);
}
```

**阴影原则**：
- 卡片使用轻阴影（0 10px 30px -5px rgba(0,0,0,0.04)）
- 重要操作按钮增加品牌色辉光
- 浮层使用深阴影提升层级感

---

## 7. 组件规范

### 7.1 底部导航栏

```html
<nav class="fixed bottom-0 max-w-[414px] w-full glass-header border-t border-slate-100 flex justify-around py-3 safe-area-bottom z-50">
  <button class="nav-item flex flex-col items-center gap-1 text-slate-400 transition-all">
    <i class="fa-solid fa-house-chimney text-xl"></i>
    <span class="text-[10px]">首页</span>
  </button>
  ...
</nav>
```

**样式要点**：
- 高度：约 60-70px（含 safe-area）
- 背景：玻璃拟态（rgba(255,255,255,0.9) + blur(16px)）
- 激活态：`text-blue-600 font-black`
- 图标大小：text-xl (20px)
- 标签文字：text-[10px] font-bold

### 7.2 活动卡片（主页横滑）

```html
<div class="min-w-[280px] bg-white rounded-[2rem] overflow-hidden card-shadow border border-slate-50 btn-press">
  <div class="h-40 relative">
    <img class="w-full h-full object-cover">
    <span class="absolute top-3 left-3 bg-white/90 backdrop-blur text-[10px] font-black px-2 py-1 rounded-lg text-blue-600 shadow-sm">标签</span>
  </div>
  <div class="p-5">
    <h4 class="font-black text-slate-900 leading-tight">标题</h4>
    <p class="text-[11px] text-slate-400 mt-2">摘要</p>
    <!-- 公司标签 -->
  </div>
</div>
```

**规格**：
- 主页最小宽度：280px
- 全屏宽度：w-full（详情页）
- 圆角：rounded-[2rem] (32px)
- 图片高度：h-40 (160px)
- 内边距：p-5 (20px)
- 标题：font-black，禁止换行

### 7.3 课程卡片（列表项）

```html
<div class="bg-white p-3 rounded-[1.5rem] flex items-center gap-4 card-shadow border border-slate-50 btn-press">
  <img class="w-16 h-16 rounded-xl object-cover">
  <div class="flex-1">
    <h4 class="text-sm font-bold text-slate-800 leading-snug">课程标题</h4>
    <p class="text-[10px] text-slate-400 font-bold mt-1">讲师</p>
  </div>
  <div class="text-right">
    <span class="text-sm font-black text-emerald-500">免费</span>
  </div>
</div>
```

**规格**：
- 圆角：rounded-[1.5rem] (24px)
- 内边距：p-3 (12px)
- 缩略图：w-16 h-16 (64px)，rounded-xl (16px)
- 标题：text-sm font-bold
- 讲师：text-[10px] font-bold

**免费价格样式**：`text-emerald-500 font-black`

### 7.4 职位卡片

```html
<div class="bg-white p-6 rounded-[2rem] border border-slate-50 card-shadow btn-press">
  <div class="flex justify-between items-start gap-4">
    <div class="flex-1">
      <h4 class="text-base font-black text-slate-800">职位名称</h4>
      <p class="text-xs text-blue-600 font-bold mt-1">公司名称</p>
      <p class="text-[11px] text-slate-400 mt-2">职位摘要</p>
    </div>
    <span class="text-sm font-black text-orange-500 whitespace-nowrap">薪资</span>
  </div>
  <!-- 技能标签 -->
</div>
```

**规格**：
- 内边距：p-6 (24px)
- 标题字号：text-base (14px)
- 薪资颜色：text-orange-500

### 7.5 详情页面板

```html
<div class="detail-panel px-6 py-8 bg-white rounded-t-[3rem] shadow-2xl">
  <!-- 详情内容 -->
</div>
```

**特效**：
- 顶部大图渐变遮罩：
```css
.detail-hero::after {
  content: "";
  position: absolute;
  bottom: 0;
  height: 90px;
  background: linear-gradient(180deg, rgba(255,255,255,0) 0%, rgba(255,255,255,0.9) 72%, #ffffff 100%);
}
```

---

## 8. 交互规范

### 8.1 按钮按压反馈

```css
.btn-press:active {
  transform: scale(0.96);
  transition: transform 0.1s;
}
```

**应用范围**：所有可点击元素（卡片、按钮、导航项）

### 8.2 页面切换动画

```css
@keyframes fadeInPage {
  from { opacity: 0; }
  to { opacity: 1; }
}

.page-animate {
  animation: fadeInPage 0.25s ease-out forwards;
}
```

### 8.3 悬浮按钮

```html
<div class="floating-shell floating-back">
  <button class="w-10 h-10 rounded-full glass-header flex items-center justify-center shadow-lg border border-white/20">
    <i class="fa-solid fa-arrow-left"></i>
  </button>
</div>
```

**固定定位组合**：
```css
.floating-shell {
  position: fixed;
  left: 50%;
  transform: translateX(-50%);
  width: min(100%, 414px);
  z-index: 60;
}
.floating-back { top: calc(2.75rem + env(safe-area-inset-top)); }
.floating-action { bottom: 0; }
```

### 8.4 Toast 提示

```html
<div class="fixed top-1/2 left-1/2 -translate-x-1/2 -translate-y-1/2 bg-slate-900/90 text-white px-6 py-3 rounded-full text-sm font-medium z-[100] shadow-2xl"></div>
```

- 背景：`rgba(15, 23, 42, 0.9)` (slate-900 90%)
- 圆角：rounded-full (完全圆形)
- 文字：text-sm font-medium
- 显示时长：1600ms

---

## 9. 标签与徽章

### 9.1 类别标签

```html
<span class="bg-blue-50 text-blue-600 text-[10px] px-2 py-0.5 rounded-md font-bold">热门路线</span>
```

**样式**：
- 背景：bg-blue-50
- 文字：text-blue-600
- 字号：text-[10px]
- 内边距：px-2 py-0.5
- 圆角：rounded-md
- 字重：font-bold

### 9.2 技能标签（职位）

```html
<span class="bg-slate-50 text-slate-400 text-[10px] px-2 py-1 rounded-md font-bold uppercase">Python</span>
```

**区别**：大写字母、更多内边距

### 9.3 公司名称标签（卡片）

```html
<span class="bg-blue-50 text-blue-600 text-[10px] px-2 py-0.5 rounded-md font-bold">DJI 大疆</span>
```

**样式**：与类别标签相同

---

## 10. 内容展示规范

### 10.1 参访路线步骤

```html
<div class="relative">
  <div class="route-line"></div>
  <div class="flex items-start gap-6 mb-8 relative">
    <div class="w-10 h-10 rounded-full bg-blue-600 text-white flex items-center justify-center font-black z-10 shadow-lg shadow-blue-100">1</div>
    <div class="flex-1 bg-slate-50 p-4 rounded-2xl border border-slate-100">
      <!-- 公司信息 -->
    </div>
  </div>
</div>
```

**样式要点**：
- 步骤数字：w-10 h-10, rounded-full, bg-blue-600, text-white, font-black
- 蓝光效果：shadow-lg shadow-blue-100
- 虚线：border-left: 2px dashed #e2e8f0
- 信息卡：bg-slate-50, border border-slate-100, rounded-2xl

### 10.2 课程模块列表

```html
<div class="bg-white px-5 py-4 rounded-[1.5rem] border border-slate-100 shadow-sm flex items-center gap-4">
  <div class="w-9 h-9 rounded-2xl bg-blue-600 text-white flex items-center justify-center font-black text-sm">1</div>
  <div class="flex-1">
    <h4 class="text-sm font-bold text-slate-800">模块标题</h4>
  </div>
</div>
```

---

## 11. 渐变与特殊背景

### 11.1 子页面渐变背景

```html
<div class="subpage-gradient min-h-screen pb-8">
  <!-- 子页面内容 -->
</div>
```

```css
.subpage-gradient {
  background: linear-gradient(180deg, #f8fbff 0%, #ffffff 100%);
}
```

### 11.2 用户中心渐变

```html
<div class="pt-20 px-8 pb-10 bg-gradient-to-b from-blue-50/50 to-white">
```

**渐变**：从 blue-50 (50% 透明度) 到纯白

---

## 12. 状态管理

### 12.1 Toast 提示

```javascript
function showToast(message) {
  const toast = document.getElementById('toast');
  toast.textContent = message;
  toast.classList.remove('hidden');
  setTimeout(() => toast.classList.add('hidden'), 1600);
}
```

**调用方式**：
```javascript
showToast('演示版暂未接入报名流程');
```

### 12.2 导航激活状态

```javascript
function setNav(tab) {
  document.querySelectorAll('.nav-item').forEach(el => el.classList.remove('nav-active'));
  document.getElementById(`nav-${tab}`).classList.add('nav-active');
}
```

**激活态样式**：`text-blue-600 font-black`

---

## 13. 图标使用规范

### 13.1 图标库版本

Font Awesome 6.4.0，使用 Solid 风格（fa-solid）

### 13.2 常用图标映射

| 用途 | 图标类名 | 大小 |
|------|---------|------|
| 首页 | fa-house-chimney | text-xl |
| 职位 | fa-compass | text-xl |
| 我的 | fa-circle-user | text-xl |
| 搜索 | fa-magnifying-glass | 按钮内 w-10 h-10 |
| 返回 | fa-arrow-left | 圆形按钮 w-10 h-10 |
| 地点 | fa-location-dot | text-sm |
| 日历 | fa-calendar | text-xs |
| 用户组 | fa-user-group | text-xs |
| 公司建筑 | fa-building | w-8 h-8 |
| 相机 | fa-camera | text-[10px] |
| 右箭头 | fa-chevron-right | text-[10px] |

**图标颜色**：
- 主要图标：`text-slate-400`（未激活），`text-blue-600`（激活）
- 功能图标：`text-blue-600`（按钮内）、`text-slate-700`（导航项）

---

## 14. 响应式与适配

### 14.1 视口设置

```html
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
```

**关键点**：
- 禁止用户缩放（适合原生 App 体验）
- 宽度锁定到设备宽度

### 14.2 安全区域

```css
.safe-area-bottom {
  padding-bottom: calc(1.5rem + env(safe-area-inset-bottom));
}
```

**应用位置**：底部导航栏、浮动操作栏

### 14.3 最大宽度限制

```css
.max-w-414 {
  max-width: 414px;  /* iPhone 14 Pro Max */
  margin: 0 auto;
}
```

**桌面端显示**：浏览器中居中显示，两侧留白

---

## 15. 性能优化建议

### 15.1 图像优化

- 使用 WebP 格式优先
- 设置明确的宽高比例避免布局偏移
- 懒加载非首屏图片（可考虑 loading="lazy"）

### 15.2 CSS 优化

- 使用 Tailwind 的 JIT 模式减少 CSS 体积
- 避免过度使用 box-shadow（性能敏感）
- 使用 `transform` 代替 `top/left` 做动画

### 15.3 字体加载

- 使用系统字体栈避免网络请求
- 确保中文字体可用性（Windows vs macOS）

---

## 16. 开发工作流

### 16.1 文件结构建议

```
/
├── index.html              # 主入口
├── assets/
│   ├── images/            # 图片资源
│   ├── icons/             # 自定义图标
│   └── fonts/             # 自定义字体（如有）
├── components/
│   ├── header.html        # 页面头部组件
│   ├── bottom-nav.html    # 底部导航
│   ├── card-activity.html # 活动卡片
│   └── ...
├── styles/
│   ├── main.css           # 主样式（覆盖 Tailwind）
│   ├── animations.css     # 动画定义
│   └── utilities.css      # 自定义工具类
├── js/
│   ├── app.js             # 主逻辑
│   ├── components.js      # 组件渲染函数
│   └── router.js          # 路由管理
└── docs/
    └── DESIGN_SYSTEM.md   # 设计规范（本文档）
```

### 16.2 命名规范

- **类名**：kebab-case（短横线分隔）
- **CSS 变量**：kebab-case（如 --primary-color）
- **JavaScript 函数**：camelCase（如 renderHome）
- **常量**：UPPER_SNAKE_CASE（如 MOCK_DATA）
- **HTML 属性**：kebab-case（如 data-id）

### 16.3 代码扩展原则

- **遵循现有模式**：新功能遵循已有的样式规范
- **复用组件**：避免重复编写相似 HTML
- **渐进增强**：确保无 JavaScript 时基本结构可用
- **性能意识**：大图片使用 CDN 或压缩版本

---

## 17. 设计令牌索引

### 17.1 快速查找

| 令牌 | 值 | 用途 |
|------|-----|------|
| `--primary` | #2563eb | 主品牌色 |
| `--success` | #10b981 | 成功/免费 |
| `--warning` | #f59e0b | 橙色强调 |
| `--slate-900` | #0f172a | 最深文字 |
| `--slate-400` | #94a3b8 | 次要文字 |
| `--white` | #ffffff | 白色背景 |
| `--radius-lg` | 1.5rem | 卡片圆角 |
| `--shadow-card` | 见 6.1 | 卡片阴影 |
| `--font-primary` | 苹方/微软雅黑 | 正文字体 |

### 17.2 代码片段

```css
/* 主按钮 */
.btn-primary {
  @apply bg-blue-600 text-white px-10 py-4 rounded-2xl font-bold shadow-xl shadow-blue-100 active:scale-95 transition-all;
}

/* 次要按钮 */
.btn-secondary {
  @apply bg-white text-slate-700 px-6 py-3 rounded-xl border border-slate-200 font-medium active:scale-95 transition-all;
}

/* 信息卡片 */
.card-info {
  @apply bg-blue-50/60 rounded-[1.6rem] p-5 border border-blue-100;
}

/* 徽章 */
.badge-default {
  @apply bg-blue-50 text-blue-600 text-[10px] px-2 py-0.5 rounded-md font-bold;
}
```

---

## 18. 常见设计问题清单

### 18.1 检查清单

- [ ] 是否使用系统字体栈？
- [ ] 文字对比度是否符合 WCAG AA 标准？
- [ ] 按钮是否至少有 44×44px 可点击区域？
- [ ] 卡片圆角是否统一（2rem / 1.5rem）？
- [ ] 间距是否使用 Tailwind 标准值？
- [ ] 图片是否设置宽高比例？
- [ ] 是否避免使用纯黑（#000）？
- [ ] 是否添加按压反馈（active:scale-95）？
- [ ] 底部导航是否考虑安全区域？
- [ ] 颜色是否使用设计令牌而非硬编码？

---

## 19. 附录：Tailwind 配置参考

### 19.1 推荐配置

```javascript
// tailwind.config.js
module.exports = {
  content: ['./**/*.html'],
  theme: {
    extend: {
      colors: {
        primary: {
          50: '#eff6ff',
          100: '#dbeafe',
          500: '#2563eb',
          600: '#1d4ed8',
          700: '#1e40af',
        },
        slate: {
          100: '#f1f5f9',  // 边框
          200: '#e2e8f0',  // 分隔线
          300: '#cbd5e1',
          400: '#94a3b8',  // 次要文字
          500: '#64748b',
          600: '#475569',
          700: '#334155',
          800: '#1e293b',  // 标题
          900: '#0f172a',  // 最深文字
        },
      },
      borderRadius: {
        '2xl': '2rem',    // 卡片
        '3xl': '2.5rem',  // 头像外框
      },
      boxShadow: {
        'card': '0 10px 30px -5px rgba(0, 0, 0, 0.04)',
        'glass': '0 8px 32px 0 rgba(31, 38, 135, 0.15)',
      },
      fontSize: {
        '10px': ['10px', '14px'],
        '11px': ['11px', '16px'],
        '12px': ['12px', '16px'],
      },
    },
  },
  plugins: [],
}
```

### 19.2 常用工具类速查

| 样式 | Tailwind 类 | 备注 |
|------|-------------|------|
| 字重黑 | `font-black` | weight: 900 |
| 字重粗 | `font-bold` | weight: 700 |
| 字重半粗 | `font-semibold` | weight: 600 |
| 白色文字 | `text-white` | - |
| 次要文字 | `text-slate-400` | - |
| 主要文字 | `text-slate-800` | - |
| 圆角卡片 | `rounded-[2rem]` | 32px |
| 圆角输入 | `rounded-xl` | 16px |
| 浅蓝背景 | `bg-blue-50` | - |
| 品牌蓝背景 | `bg-blue-600` | - |
| 玻璃态 | `glass-header` | 自定义类 |
| 按压反馈 | `btn-press` | 自定义类 |
| 溢出隐藏 | `overflow-hidden` | - |
| 绝对定位 | `absolute` | - |
| 固定定位 | `fixed` | - |
| Flex 布局 | `flex` | - |
| 水平居中 | `items-center` | - |
| 垂直居中 | `justify-center` | - |
| 两端对齐 | `justify-between` | - |

---

## 20. 版本记录

| 版本 | 日期 | 变更内容 |
|------|------|---------|
| v1.0 | 2025-03-30 | 初始版本，基于 demo v2.1.84.845 创建 |


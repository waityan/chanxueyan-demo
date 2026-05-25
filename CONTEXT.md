# 产学研参访 Pro — 增强体验版 Demo

> 移动端 H5 演示原型，模拟「企业参访 + 社区 + 求职」一体化产学研小程序。
> 单 HTML 文件，纯前端 Mock 数据，浏览器直接运行。

---

## 目录结构

```
chanxueyan-demo/
├── index-with-community.html     ← 主页面（单页应用，含社区模块）
├── DESIGN_STYLE.md               ← 设计风格指南
├── DESIGN_SYSTEM.md              ← 设计规范文档
├── CONTEXT.md                    ← 本文件
├── .gitignore
├── .claude/                      ← Claude Code 配置（本地，不提交）
└── demo-enhanced-assets/         ← 配图资源（6 组，每组 jpg/png/svg）
    ├── route-bay.*               ← 大湾区路线
    ├── route-shanghai.*          ← 上海路线
    ├── course-ai.*               ← AI 产品课程
    ├── course-interview.*        ← 面试技巧课程
    ├── job-algorithm.*           ← 算法职位
    └── job-pr.*                  ← 公关职位
```

## 技术栈

| 层 | 技术 |
|---|---|
| CSS 框架 | Tailwind CSS (CDN) |
| 图标库 | Font Awesome 6.4.0 (CDN) |
| 字体 | PingFang SC / Microsoft YaHei |
| 路由 | 原生 JS SPA（无框架） |
| 状态 | 全局 STATE 对象 + Mock 数据 |
| 存储 | 无持久化（纯内存 Mock） |

## 功能模块

### 底部导航（4 Tab）

| Tab | 路由函数 | 内容 |
|---|---|---|
| 首页 | `renderHome()` | 参访路线横向滚动 + 职场课程列表 |
| 社区 | `renderCommunity()` | 帖子流 + 话题筛选 + 发帖 FAB |
| 职位 | `renderJobs()` | 职位列表 + 类型筛选（全部/全职/实习/管培生） |
| 我的 | `renderMine()` | 个人中心 + 票券/收藏 + 设置入口 |

### 子页面

| 页面 | 函数 | 触发入口 |
|---|---|---|
| 路线列表 | `renderRoutes()` | 首页「更多路线」 |
| 课程列表 | `renderCourses()` | 首页「全部课程」 |
| 路线详情 | `renderDetail(id, source)` | 点击路线卡片 |
| 课程详情 | `renderCourseDetail(id, source)` | 点击课程卡片 |
| 职位详情 | `renderJobDetail(id)` | 点击职位卡片 |
| 帖子详情 | `renderPostDetail(postId)` | 点击帖子卡片 |
| 搜索 | `renderSearch()` | 首页搜索图标 |
| 设置 | `renderSettings()` | 我的页面 → 设置 |

### 交互功能

| 功能 | 实现方式 |
|---|---|
| **搜索** | 全屏搜索页，输入实时过滤路线/课程/职位/帖子，可按类型筛选 |
| **发帖** | 底部模态框，输入内容 + 选择话题标签，提交后插入帖子列表首位 |
| **评论** | 帖子详情页底部输入框，提交后加入 `post.commentsList`，实时显示 |
| **点赞** | toggle `post.liked`，更新 `post.likes` 计数 |
| **话题筛选** | 社区页顶部标签栏，按帖子 `post.tags` 过滤 |
| **职位筛选** | 按 `job.type`（全职/实习/管培生）过滤，状态存在 `STATE.jobFilter` |
| **确认弹窗** | `showConfirmModal(title, message, onConfirm)` 通用确认对话框 |
| **操作菜单** | `showModal(title, bodyHtml)` 通用底部模态框 |
| **Toast** | 居中深色提示，1600ms 自动消失 |

## 数据模型

### Mock 数据（`MOCK_DATA`）

```js
activities: [
  { id, title, city, date, price, tag, summary, image,
    companies: [{ name, intro, focus, duration }] }
]
courses: [
  { id, title, teacher, price, image, summary, suitable,
    sections: [string] }
]
jobs: [
  { id, title, company, salary, city, type, tags, image, summary,
    companyIntro, responsibilities: [string], requirements: [string] }
]
posts: [
  { id, author, avatar, time, content, images, tags, likes, comments,
    liked, commentsList: [{ author, avatar, content, time }] }
]
user: { name, school, major }
```

### 全局状态（`STATE`）

```js
{
  currentTab: 'home',          // 当前 Tab
  currentPost: null,           // 当前查看的帖子 ID
  communityFilter: 'all',      // 社区话题筛选
  jobFilter: 'all'             // 职位类型筛选
}
```

## 路由与导航

- SPA 模式，`setView(html, options)` 替换 `#view-container` 内容
- 主 Tab 切换通过 `switchTab(tab)` 分发到各 render 函数
- 子页面通过 `showNav: false` 隐藏底部导航栏
- 详情页使用悬浮返回按钮（`floating-back`），通过 `getBackAction(source)` 确定返回目标
- 详情页底部操作栏使用 `renderFixedActionBar(content)` 固定定位

## 设计系统

详细设计规范见 `DESIGN_STYLE.md` 和 `DESIGN_SYSTEM.md`。

核心参数：

- 手机框架：max-width 414px，居中
- 主色：`#2563eb`（科技蓝）
- 卡片圆角：24-32px
- 阴影：`box-shadow: 0 10px 30px -5px rgba(0,0,0,0.04)`
- 底部导航：玻璃拟态（backdrop-filter blur）
- 按压反馈：scale(0.96) 0.1s
- 页面切换：fadeIn 0.25s ease-out

## 关键实现细节

### Toast 系统
- 唯一 DOM 节点 `#toast`，复用而非创建/销毁
- `showToast.timer` 挂在函数对象上，避免全局变量

### 弹窗系统
- `showModal(title, bodyHtml)` — 通用底部模态框
- `showConfirmModal(title, message, onConfirm)` — 确认对话框
- 模态框通过 `modal-overlay` 覆盖层 + 底部卡片实现
- 点击遮罩不关闭（需点击关闭按钮）

### 评论功能
- 每个帖子自带 `commentsList` 数组存储评论
- 新评论使用当前用户名（`MOCK_DATA.user.name`）
- 提交后 `post.comments` 同步更新

### 发帖功能
- 帖子 ID 使用 `Date.now()` 生成，确保唯一
- 新帖子使用 `unshift` 插入列表首位
- 发帖后自动刷新社区列表（如果当前在社区 Tab）

### 图片资源
- HTML 中引用 `.jpg` 版本
- 每种素材提供 jpg/png/svg 三种格式备选
- 图片路径为相对路径 `./demo-enhanced-assets/`

### 已知限制
- 无持久化存储（刷新后数据重置）
- 无用户认证（所有用户共用 mock user）
- 图片为占位素材，非真实企业照片
- 报名/投递为模拟确认流程，无后端 API

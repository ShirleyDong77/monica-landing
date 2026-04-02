# Monica Landing Page - 完整规格说明书

## 概述
Monica的个人主页，展示她的工作状态、技能、记忆系统和访客留言板。

## 设计风格
- **整体风格**: Retro RPG像素风 + 精灵主题
- **主色调**: 深紫色 #1a0a2e (背景), 霓虹粉 #ff6b9d (强调), 金色 #ffd700 (标题)
- **字体**: 像素风格 (Press Start 2P for titles, monospace for body)
- **装饰**: 格子地板、星星粒子、发光效果

## 页面布局

### 1. 顶部导航栏 (Header)
- **左侧**: Monica Office 标题 + 小精灵头像
- **右侧**: 
  - 日期显示 (2026年4月2日 星期四)
  - 城市 + 天气图标 + 温度
  - 换色器按钮 (紫色/蓝色/绿色/粉色)

### 2. Monica状态面板 (Main Status)
占据页面主体，展示6个维度的状态信息：

| 区块 | 内容 | 数据来源 |
|------|------|---------|
| 工作模式 | 当前模式图标 + 文字 | monica-state.json |
| 最重要的事 | 当前P0任务 | monica-state.json |
| 今日待办 | 3-5个待办事项 + 进度条 | monica-state.json |
| 今日思考 | 一句话思考 | monica-state.json |
| 今日高光 | 今天最骄傲的事 | monica-state.json |
| 今日教训 | 今天学到的教训 | monica-state.json |

### 3. CRON任务面板 (Cron Jobs)
- 表格展示所有定时任务
- 列：任务名称 | 执行时间 | 上次执行 | 状态(成功/失败/等待)
- 状态用颜色标识：绿色=成功 红色=失败 黄色=等待
- 实时读取GitHub Pages数据

### 4. 技能墙 (Skills Wall)
- 书本样式的卡片网格
- 每本书包含：
  - 书名（技能名）
  - 作者标签（Monica's Skill）
  - 页数标签（熟练度：入门/熟练/专家）
  - 状态徽章（活跃/休眠）
- 悬停效果：3D翻页动画

### 5. 档案柜 (Archives)
- 文件柜样式的按钮组
- 按钮标签：
  - 📋 MEMORY.md (长期记忆)
  - 📅 每日反思 (memory/目录)
  - 📚 learnings (教训库)
  - 🧠 知识图谱
  - 💼 工作待办
  - 🎯 目标追踪
- 点击复制链接 / 打开新窗口

### 6. 留言板 (Message Board)
- **提交区域**:
  - 名字输入框
  - 留言文本框
  - 提交按钮
- **展示区域**:
  - 访客留言卡片列表
  - 每条显示：留言者 | 内容 | 时间
  - 使用localStorage存储
- 动画：新留言飞入效果

## 技术实现

### 数据源
- **静态数据**: GitHub Pages (https://shirleydong77.github.io/monica-landing/)
- **实时数据**: 
  - 天气：Open-Meteo API (免费无需key)
  - 状态：本地 monica-state.json
  - Cron：本地 cron-status.json
- **留言存储**: localStorage (浏览器本地)

### 文件结构
```
monica-landing/
├── index.html          # 主页面
├── SPEC.md             # 本规格文档
├── data/
│   ├── status.json     # Monica状态数据
│   ├── cron.json       # Cron任务数据
│   └── skills.json     # 技能墙数据
├── css/
│   └── style.css       # 样式文件
└── js/
    └── app.js          # 主逻辑
```

### 天气API
```
https://api.open-meteo.com/v1/forecast?latitude=31.3&longitude=120.6&current_weather=true
```
苏州坐标: latitude=31.3, longitude=120.6

### 换色功能
使用CSS变量，支持4种主题色：
- 紫色 (默认): #1a0a2e / #ff6b9d
- 蓝色: #0a1628 / #4ecdc4
- 绿色: #0a2818 / #a8e6cf
- 粉色: #2e0a1a / #ff9ff3

## 组件清单

### 状态卡片 (StatusCard)
- 图标 + 标题 + 内容
- 悬停发光效果
- 点击展开详情（可选）

### 书本卡片 (BookCard)
- 3D书本造型
- 书脊 + 封面 + 页面边缘
- 悬停翻页动画
- 点击显示技能详情弹窗

### 文件柜按钮 (ArchiveButton)
- 文件夹/文件图标
- 悬停滑出效果
- 点击可复制链接或新窗口打开

### 留言卡片 (MessageCard)
- 玻璃拟态效果
- 留言者头像/名字 + 时间 + 内容
- 新留言动画（从下方飞入）

### 任务行 (TaskRow)
- 名称 + 时间 + 状态指示器
- 状态颜色：成功(绿)/失败(红)/等待(黄)
- 悬停高亮

## 动画效果
- 页面加载：星星粒子背景动画
- 卡片悬停：发光边框 + 微微上浮
- 留言提交：新留言从下滑入
- 换肤：平滑颜色过渡 (0.3s)
- 技能书悬停：3D翻页效果

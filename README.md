# 江和洲 · 个人学术主页 &nbsp;|&nbsp; Hezhou Jiang · Academic Homepage

[![中文](https://img.shields.io/badge/lang-中文-red)](./README_CN.md)
[![English](https://img.shields.io/badge/lang-English-blue)](./README.md)

> 浙江大学城乡规划博士研究生 · 数据与机器学习驱动的空间分析与建模

---

## 项目简介

自托管的双语学术个人主页，展示研究方向、代表性项目、发表论文与专业履历。

**设计理念**：单文件、零依赖、双语切换。所有页面均为自包含 HTML（CSS/JS 内联），无需构建工具或后端运行环境，任何静态服务器或直接双击即可浏览。

### 在线访问

| 环境 | 地址 |
|------|------|
| 🖥️ 本地预览 | 双击 `docs/index.html` |
| 🌐 GitHub Pages | `https://<username>.github.io/jhz-homepage/` |

---

## 页面清单

```
docs/
├── index.html                   ← 主首页（双语，7 段落）
├── work-urban-industry.html     ← 城市产业空间智能助手
├── work-housing.html            ← 住房公平与绿灰基础设施
├── work-carbon-storage.html     ← 碳储量多尺度分析
├── work-carbon-transfer.html    ← 城市间碳转移与配额
├── work-ecosystem-services.html ← 生态系统服务供需与驱动力
├── project-list.html            ← 项目清单
├── cv.pdf                       ← 简历
└── portfolio.pdf                ← 规划作品集
```

### 首页结构

| 段落 | ID | 内容 |
|------|-----|------|
| Hero | — | 照片、姓名、一句话介绍、GitHub/邮箱/CV 按钮、单位信息 |
| 00 | `#about` | 背景与方向：博四、领域深度、数据建模素养 |
| 01 | `#cap` | 专业能力：4 张卡片（数据构建、ML、编程、领域背景） |
| 02 | `#proj` | 代表性项目：5 个项目卡片（全部可点击进入详情页） |
| 03 | `#pubs` | 发表论文：8 篇（SCI/SSCI + 中文核心） |
| 04 | `#practice` | 履历：时间线 + 奖项 + 作品集链接 |
| 05 | `#contact` | 联系方式 |

---

## 设计系统

```css
:root {
  --paper:  #F6F7F9;   /* 页面底色 */
  --ink:    #12161D;   /* 主文字色 */
  --muted:  #59626F;   /* 次要文字 */
  --line:   #E3E6EB;   /* 分割线 */
  --accent: #13497E;   /* 强调色（深蓝） */
  --card:   #FFFFFF;   /* 卡片底色 */
}
```

所有页面共享同一套设计令牌，保证风格统一。字体栈优先使用系统字体（PingFang SC / Microsoft YaHei / Noto Sans SC），无额外字体下载开销。

---

## 双语机制

每个可翻译元素使用 `<span class="zh">中文</span><span class="en">English</span>` 对。根元素 `<html data-lang="zh">` 通过 CSS 控制显示：

```css
html[data-lang="zh"] .en { display: none }
html[data-lang="en"] .zh { display: none }
```

语言切换按钮（EN/中文）在所有页面顶部栏中，JS 逻辑完全相同。

---

## 如何新增一篇论文详情页

使用 `paper-to-webpage` skill 的标准化流水线：

```
1. 解包 docx → 提取图片 + pandoc 转换
2. 提取表格数据（python-docx 精确读取）
3. 图片压缩为 WebP（1200px, q82）
4. 填充 page_template.html 模板
5. embed_images.py 嵌入 base64 → 单文件自包含
6. Playwright 渲染验证
7. 主页接线：卡片改 <a> 链接 + 论文列表更新
```

详情页输出：**双语、图片内嵌、表格完整、参考文献去掉**，单 HTML 文件直接可用。

---

## 部署方式

### 方式一：Nginx（当前服务器方案）

```nginx
server {
    listen 80;
    server_name your-domain.com;
    root /var/www/jhz-homepage/files;
    index index.html;
}
```

### 方式二：GitHub Pages

1. 将此仓库推送到 GitHub
2. Settings → Pages → Source: `Deploy from a branch` → 选择 `main` 分支，目录选择 `/docs`
3. 访问 `https://<username>.github.io/<repo>/`

### 方式三：本地预览

直接双击任意 `.html` 文件即可在浏览器中查看（详情页的返回链接指向 `./index.html#proj`，需所有文件在同一目录下）。

---

## 技术特点

- **零依赖**：纯 HTML + 内联 CSS/JS，无 npm/webpack/CDN
- **单文件详情页**：图片 base64 内嵌，每篇论文一个文件，方便分享与存档
- **双语架构**：`data-lang` 属性切换，无页面刷新
- **响应式**：`@media (max-width: 720px)` 适配移动端
- **无障碍**：`prefers-reduced-motion` 尊重系统设置，语义化 HTML 结构
- **性能**：系统字体栈（零字体下载）、IntersectionObserver 懒加载动画、图片 `loading="lazy"`

---

## 目录结构

```
JHZ Personal Website/
├── docs/                        ← 网站根目录（GitHub Pages 发布源）
│   ├── index.html
│   ├── work-*.html
│   ├── project-list.html
│   ├── cv.pdf
│   └── portfolio.pdf
├── README.md
└── .gitignore
```

---

## 作者

**江和洲 (Hezhou Jiang)**

- 🏫 浙江大学 · 城乡规划系 · 博士研究生
- 📧 jhezhou@163.com
- 🐙 [github.com/HirezmingD](https://github.com/HirezmingD)
- 📍 中国 · 杭州

---

## 许可

本仓库中的个人内容（照片、简历、论文摘要等）保留所有权利。HTML/CSS/JS 代码结构可自由参考。

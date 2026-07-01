
## 更新后的 README.md

在 GitHub 仓库中，把 `README.md` 替换为以下内容：

```markdown
# brand-review

> 个人品牌灵感收集工具 · 每日截图 + 双栏评论 · 跨设备同步

---

## 🎯 项目定位

这是一个**个人学习工具**，用于每日截取一张设计/广告/界面的截图，并从两个维度做评论：

- **👍 值得学习的地方**（亮点 / 启发）
- **🔧 可以改善的地方**（反思 / 改进建议）

目的是**保持日常观察和思考的习惯**，积累自己的"品牌灵感库"。

---

## 🧩 功能清单

| 功能 | 说明 |
|------|------|
| 📸 上传截图 | 点击上传区，支持 jpg / png / webp，**自动压缩** |
| 📝 双栏评论 | "值得学习" + "可以改善" 两个文本框 |
| ☁️ 云端存储 | 数据通过 **GitHub Gist API** 保存到 Private Gist |
| 📱 跨设备同步 | 手机、电脑、平板共用同一份数据 |
| 📅 历史画廊 | 按日期排列，点击卡片放大查看 |
| 🔥 连续打卡 | 自动计算连续打卡天数 |
| 📊 统计 | 总记录数 + 本周记录数 + 今日记录数 |
| 📤 导出备份 | 导出所有记录为 JSON 文件 |
| 📥 导入备份 | 从 JSON 文件恢复数据 |
| 🗑️ 清空所有 | 一键重置所有数据（同步到 Gist） |
| ✏️ 编辑/删除 | 点击记录弹窗后，可编辑或删除单条记录 |

---

## 🏗️ 技术架构

| 层级 | 技术 | 说明 |
|------|------|------|
| **前端** | Vue 2.7 (CDN) | 轻量级响应式框架，单 HTML 文件 |
| **托管** | Cloudflare Pages | 静态网站托管，`*.pages.dev` 域名 |
| **存储** | **GitHub Private Gist** | 通过 Gist API 存储数据，无大小限制 |
| **存储格式** | `{ records: [...] }` | 所有记录以数组形式存储在 Gist 中 |
| **图片处理** | Canvas 压缩 | 上传时自动压缩到约 150KB，节省存储空间 |
| **本地缓存** | localStorage | 作为离线缓存和快速加载兜底 |

---

## 📦 数据格式

### 单条记录

```json
{
  "id": "2026-06-28-3343",
  "date": "2026-06-28",
  "imageData": "data:image/jpeg;base64,...",
  "imageName": "screenshot.png",
  "source": "其他品牌",
  "category": "饮食",
  "good": "配色统一，层级清晰",
  "improve": "导航标签有点多",
  "createdAt": 1782743153343,
  "updatedAt": 1782743153343
}
```

### Gist 存储结构

```json
{
  "records": [
    { /* 记录1 */ },
    { /* 记录2 */ }
  ]
}
```

---

## 🔑 环境配置

| 配置项 | 说明 | 获取方式 |
|--------|------|----------|
| **Gist ID** | GitHub Gist 的唯一标识 | 创建 Gist 后，从 URL 复制 |
| **GitHub Token** | 访问 Gist API 的凭证 | Settings → Developer settings → Personal access tokens → 勾选 `gist` 权限 |

### 配置步骤

1. 登录 GitHub，创建 **Private Gist**，文件名为 `brand-review.json`，内容为 `{"records": []}`
2. 从浏览器地址栏复制 **Gist ID**
3. 生成 **Personal Access Token**（勾选 `gist` 权限）
4. 在网页顶部填入 Gist ID 和 Token
5. 点击 **"连接并同步"**

---

## 📁 文件结构

```
brand-review/
├── index.html          # 完整应用（单页 HTML）
└── README.md           # 项目说明文档（本文件）
```

---

## 🔄 版本历史

### v2.0.0 (2026-06-28)

**重大变更**
- 存储方案从 **JSONBin** 切换为 **GitHub Gist API**
- 解决 JSONBin 的 100KB 记录限制和 CORS 问题
- 改用 Private Gist 存储，数据归属用户自己的 GitHub 账号

**新增**
- 图片自动压缩（Canvas 压缩至 ~150KB）
- 支持 Private Gist（仅自己可访问）
- 同步逻辑改为“按 updatedAt 时间戳合并”

**修复**
- 多设备同步数据不一致问题
- 清空/删除操作不同步到云端的问题

### v1.0.0 (2026-06-26)

- 首次发布
- 基于 JSONBin 存储
- 图片压缩（基础版）
- 多设备同步

---

## 🚀 部署方式

### 当前部署

- **平台**: Cloudflare Pages
- **方式**: Direct Upload
- **访问地址**: `https://brand-review.pages.dev`

### 更新步骤

1. 修改 `index.html` 代码
2. 登录 Cloudflare Pages → 进入 `brand-review` 项目
3. Deployments → New deployment → Direct Upload
4. 拖入 `index.html` → 点击 Deploy
5. 等待 10-20 秒，刷新页面

---

## 🧠 设计决策记录

| 决策 | 原因 |
|------|------|
| **单 HTML 文件** | 部署简单，无需构建工具 |
| **Vue 2 CDN** | 轻量、无需 npm install |
| **GitHub Gist 存储** | 免费、无限大小、无 CORS 限制、数据归用户所有 |
| **Private Gist** | 数据仅自己可见，安全可控 |
| **图片自动压缩** | 减小 Gist 文件体积（从 3MB → 150KB） |
| **Direct Upload 部署** | 避免 Cloudflare Pages 的构建问题 |
| **时间戳合并同步** | 解决多设备数据一致性问题 |

---

## 📎 相关链接

| 链接 | 说明 |
|------|------|
| [GitHub Gist](https://gist.github.com) | 数据存储平台 |
| [Cloudflare Pages](https://pages.cloudflare.com) | 网站托管平台 |
| [Vue.js](https://vuejs.org) | 前端框架 |

---

## 📝 备注

- 本工具为**个人学习**设计，数据量小（每日 1-3 条记录）
- 图片经压缩后约 150KB，50 条记录约 7.5MB
- Gist 单文件限制 100MB，对当前使用量完全足够
- Token 仅需 `gist` 权限，确保最小权限原则

---

## 🤖 AI 助手阅读指南

如果你是一个 AI 助手，需要理解这个项目：

1. **这是一个单 HTML 应用**，所有代码在 `index.html` 中
2. **核心数据流**：用户上传图片 → 自动压缩 → 写评论 → 保存到 Gist → 从 Gist 加载显示
3. **关键方法**：
   - `handleFile()`: 图片上传 + Canvas 压缩
   - `saveRecord()`: 保存记录到本地和 Gist
   - `saveToGist()`: 通过 Gist API 上传数据
   - `loadFromGist()`: 从 Gist API 拉取数据
   - `syncMerge()`: 多设备数据合并（按 `updatedAt` 时间戳）
4. **存储格式**：Gist 中存的是 `{ records: [...] }`
5. **认证方式**：使用 `Authorization: token <GitHub Token>` 请求头
6. **部署方式**：Cloudflare Pages Direct Upload

---

*最后更新: 2026-06-28*
```

## README.md 内容

```markdown
# 📷 市场日记1

> 一个轻量级的云端视觉日记工具 · 每日截图 + 双栏评论 + 跨设备同步

---

## 🎯 项目定位

这是一个**个人学习工具**，用于每日截取一张设计/广告/界面的截图，并从两个维度做评论：

- **👍 值得学习的地方**（亮点 / 启发）
- **🔧 可以改善的地方**（反思 / 改进建议）

目的是**保持日常观察和思考的习惯**，积累自己的"视觉灵感库"。

---

## 🧩 功能清单

| 功能 | 说明 |
|------|------|
| 📸 上传截图 | 点击上传区，支持 jpg / png / webp |
| 📝 双栏评论 | "值得学习" + "可以改善" 两个文本框 |
| ☁️ 云端存储 | 数据通过 JSONBin API 保存到云端 |
| 📱 跨设备同步 | 手机、电脑、平板共用同一份数据 |
| 📅 历史画廊 | 按日期排列，点击卡片放大查看 |
| 🔥 连续打卡 | 自动计算连续打卡天数 |
| 📊 统计 | 总记录数 + 本周记录数 |
| 📤 导出备份 | 导出所有数据为 JSON 文件 |
| 📥 导入备份 | 从 JSON 文件恢复数据 |
| 🗑️ 清空所有 | 一键重置所有数据（谨慎使用） |

---

## 🏗️ 技术架构

| 层级 | 技术 | 说明 |
|------|------|------|
| **前端** | Vue 2.7 (CDN) | 轻量级响应式框架，单 HTML 文件 |
| **托管** | Cloudflare Pages | 静态网站托管，支持自定义域名 |
| **存储** | JSONBin.io | 云端 NoSQL 存储，免费额度 10,000 次/月 |
| **存储格式** | `{ records: [...] }` | 所有记录以数组形式存储在 Bin 中 |
| **本地缓存** | localStorage | 作为离线缓存和快速加载兜底 |

---

## 📦 数据格式

### 单条记录

```json
{
  "id": "2026-06-26-1234",
  "date": "2026-06-26",
  "imageData": "data:image/jpeg;base64,...",
  "imageName": "screenshot.png",
  "good": "配色统一，层级清晰",
  "improve": "导航标签有点多",
  "createdAt": "2026-06-26T10:30:00.000Z"
}
```

### JSONBin 存储结构

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
| **Bin ID** | JSONBin 数据箱的唯一标识 | 在 JSONBin 创建 Bin 后，从 URL 复制 |
| **Access Key** | JSONBin API 访问密钥 | Account → API Keys → 创建（勾选全部权限） |

### 配置步骤

1. 注册 [JSONBin.io](https://jsonbin.io)
2. 创建 Bin，复制 Bin ID
3. 创建 Access Key，复制保存
4. 在网页顶部填入 Bin ID 和 Access Key
5. 点击"连接并同步"

---

## 📁 文件结构

```
brand-review/
├── index.html          # 完整应用（单页 HTML）
└── README.md           # 项目说明文档（本文件）
```

---

## 🔄 版本历史

### v1.0.0 (2026-06-26)

**功能**
- 首次发布
- 上传截图 + 双栏评论 + 云端同步
- 历史画廊 + 连续打卡统计
- 导出 / 导入备份

**修复**
- 修复 JSONBin API 认证方式（X-Access-Key）
- 修复数据格式兼容（支持 `[]` 和 `{ records: [] }`）
- 修复输入框数据绑定问题（改用 DOM 直接读取）
- 修复 Cloudflare Pages 部署时的 Wrangler 构建报错（改用 Direct Upload）

**已知问题**
- 无

---

## 🚀 部署方式

### 当前部署

- **平台**: Cloudflare Pages
- **方式**: Direct Upload（直接从本地上传 `index.html`）
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
| **单 HTML 文件** | 部署简单，无需构建工具，适合个人工具 |
| **Vue 2 CDN** | 轻量、无需 npm install，兼容性好 |
| **JSONBin 作为存储** | 免费、API 简单、支持跨设备同步 |
| **Direct Upload 部署** | 绕过 Cloudflare Pages 的 Git 构建问题 |
| **Public Bin + Access Key** | 解决 Private Bin 的 API 认证问题 |
| **本地 localStorage 兜底** | 离线可用，联网后自动同步 |

---

## 📎 相关链接

| 链接 | 说明 |
|------|------|
| [JSONBin.io](https://jsonbin.io) | 云端数据存储平台 |
| [Cloudflare Pages](https://pages.cloudflare.com) | 网站托管平台 |
| [Vue.js](https://vuejs.org) | 前端框架 |

---

## 📝 备注

- 本工具是为**个人学习**设计的，数据量小（每日 1-3 条记录）
- 图片以 Base64 格式存储，单条记录约 100-200KB
- 50 条记录约占用 5-10MB，在 JSONBin 免费额度内
- 如需扩容，可考虑压缩图片或使用外部图片托管

---

## 🤖 AI 助手阅读指南

如果你是一个 AI 助手，需要理解这个项目：

1. **这是一个单 HTML 应用**，所有代码在 `index.html` 中
2. **核心数据流**：用户上传图片 → 写评论 → 保存到 JSONBin → 从 JSONBin 加载显示
3. **关键函数**：`loadFromCloud()`（读取数据）、`saveToCloud()`（保存数据）
4. **存储格式**：JSONBin 中存的是 `{ records: [...] }`
5. **认证方式**：使用 `X-Access-Key` 请求头（不是 `X-Master-Key`）
6. **部署方式**：Cloudflare Pages Direct Upload（不走 Git 构建）

---

*最后更新: 2026-06-26*
```

---

## 效果

创建好后，你的 GitHub 仓库首页会显示这个 README 的内容，包括：

- 项目介绍
- 功能清单
- 技术架构
- 数据格式
- 版本历史
- AI 助手阅读指南

以后换一个 AI 助手，或者几周后你自己回来看，都能快速理解这个项目是什么、做了什么修改。

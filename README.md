# Cloudflare Workers 内容平台后台系统

这是一个基于 Cloudflare Workers 的内容自动生成平台，包含：

- ✅ 内容自动生成（Scheduled Triggers）
- ✅ 数据库存储（D1）
- ✅ 后台管理界面（响应式 UI）
- ✅ 管理员登录系统（JWT 鉴权）
- ✅ 内容编辑 / 删除功能

---

## 📦 项目结构

```
├── public/              # 静态页面：admin, login
├── src/
│   ├── index.js         # Worker 主入口
│   ├── routes/          # 路由分发模块
│   └── utils/           # JWT 工具等
├── wrangler.toml        # 配置文件
```

---

## 🚀 部署指南

1. 安装 wrangler
```bash
npm install -g wrangler
```

2. 初始化项目（修改 wrangler.toml 中的 account_id）

3. 绑定 D1 数据库（可通过 `wrangler d1 create db_name`）

4. 部署
```bash
wrangler publish
```

---

## 🔒 管理员登录

- 登录地址：`/login`
- 成功后跳转到 `/admin`
- 使用 JWT Token 存储于 `localStorage` 并附加到 API 请求

---

## 🧩 API 接口

- `POST /auth/login` - 登录
- `GET /content/list` - 获取内容列表（需要 JWT）
- `PUT /content/edit/:id` - 编辑内容
- `DELETE /content/delete/:id` - 删除内容

---

## 📅 定时内容生成

在 `wrangler.toml` 中添加：

```toml
[[triggers]]
crons = ["0 3 * * *"]  # 每天凌晨 3 点自动运行
```

对应代码位于：`src/routes/scheduled.js`

---

## 🧪 示例账户

你可以在 `auth.js` 中硬编码初始用户名和密码，例如：

```js
if (username === "admin" && password === "123456") ...
```

---

## 🛠 环境变量

你可以在 `.env` 或 wrangler secrets 中配置：

```
JWT_SECRET=your-secret-key
```

---

## ✨ License

MIT

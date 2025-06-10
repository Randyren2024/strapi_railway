# Railway 部署快速指南

## 一键部署到 Railway

[![Deploy on Railway](https://railway.app/button.svg)](https://railway.app/template/strapi)

## 手动部署步骤

### 1. 准备代码仓库

```bash
# 初始化 git 仓库（如果还没有）
git init
git add .
git commit -m "Initial Strapi project for Railway"

# 推送到 GitHub
git remote add origin https://github.com/your-username/your-repo.git
git branch -M main
git push -u origin main
```

### 2. 在 Railway 中创建项目

1. 访问 [Railway](https://railway.app)
2. 点击 "New Project"
3. 选择 "Deploy from GitHub repo"
4. 选择你的仓库

### 3. 配置环境变量

在 Railway 项目设置中添加以下环境变量：

```bash
# 基本配置
NODE_ENV=development
PORT=1337

# 安全密钥（请生成你自己的密钥）
APP_KEYS=key1,key2,key3,key4
API_TOKEN_SALT=your-api-token-salt
ADMIN_JWT_SECRET=your-admin-jwt-secret
TRANSFER_TOKEN_SALT=your-transfer-token-salt
JWT_SECRET=your-jwt-secret

# 数据库配置
DATABASE_CLIENT=postgres
```

### 4. 添加 PostgreSQL 数据库

1. 在 Railway 项目中点击 "+ New"
2. 选择 "Database" → "PostgreSQL"
3. Railway 会自动设置 `DATABASE_URL` 环境变量

### 5. 生成安全密钥

使用以下 Node.js 命令生成安全的随机密钥：

```javascript
// 在 Node.js 控制台中运行
const crypto = require('crypto');

// 生成 APP_KEYS（需要4个）
console.log('APP_KEYS:');
for(let i = 0; i < 4; i++) {
  console.log(crypto.randomBytes(32).toString('base64'));
}

// 生成其他密钥
console.log('\nAPI_TOKEN_SALT:', crypto.randomBytes(32).toString('base64'));
console.log('ADMIN_JWT_SECRET:', crypto.randomBytes(32).toString('base64'));
console.log('TRANSFER_TOKEN_SALT:', crypto.randomBytes(32).toString('base64'));
console.log('JWT_SECRET:', crypto.randomBytes(32).toString('base64'));
```

### 6. 部署完成

1. Railway 会自动构建和部署你的应用
2. 部署完成后，访问提供的 URL
3. 首次访问 `/admin` 创建管理员账户

## 开发模式特性

✅ **热重载**: 代码更改时自动重启  
✅ **详细日志**: 开发友好的错误信息  
✅ **管理面板**: 完整的内容管理界面  
✅ **API 文档**: 自动生成的 API 文档  
✅ **数据库管理**: 通过管理面板管理数据  

## 访问你的应用

- **应用首页**: `https://your-app.railway.app`
- **管理面板**: `https://your-app.railway.app/admin`
- **API 端点**: `https://your-app.railway.app/api`

## 故障排除

### 查看部署日志

```bash
# 安装 Railway CLI
npm install -g @railway/cli

# 登录
railway login

# 查看日志
railway logs
```

### 常见问题

1. **构建失败**: 检查 `package.json` 中的依赖版本
2. **数据库连接失败**: 确保 PostgreSQL 服务已添加
3. **环境变量错误**: 检查所有必需的环境变量是否已设置

## 本地开发

```bash
# 安装依赖
npm install

# 启动开发服务器
npm run develop

# 访问本地应用
# http://localhost:1337
# http://localhost:1337/admin
```

## 下一步

- 创建内容类型
- 配置 API 权限
- 添加插件
- 自定义管理面板
- 连接前端应用
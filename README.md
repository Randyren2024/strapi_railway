# Strapi Railway 开发模式部署

这是一个配置为在 Railway 平台上以开发模式运行的 Strapi 项目。

## 功能特性

- ✅ 开发模式配置（热重载、调试功能）
- ✅ Railway 平台优化
- ✅ PostgreSQL 数据库支持
- ✅ 本地 SQLite 开发支持
- ✅ 安全的环境变量管理
- ✅ CORS 配置用于前端连接

## 本地开发

### 安装依赖

```bash
npm install
```

### 启动开发服务器

```bash
npm run develop
```

访问：
- 应用: http://localhost:1337
- 管理面板: http://localhost:1337/admin

## Railway 部署

### 1. 准备部署

1. 将代码推送到 GitHub 仓库
2. 在 Railway 中连接你的 GitHub 仓库
3. Railway 会自动检测这是一个 Node.js 项目

### 2. 配置环境变量

在 Railway 项目设置中添加以下环境变量：

```bash
# 必需的环境变量
NODE_ENV=development
APP_KEYS=生成的密钥1,生成的密钥2,生成的密钥3,生成的密钥4
API_TOKEN_SALT=生成的API令牌盐值
ADMIN_JWT_SECRET=生成的管理员JWT密钥
TRANSFER_TOKEN_SALT=生成的传输令牌盐值
JWT_SECRET=生成的JWT密钥

# 数据库配置（Railway会自动提供DATABASE_URL）
DATABASE_CLIENT=postgres
```

### 3. 生成安全密钥

你可以使用以下命令生成安全的密钥：

```bash
# 生成随机密钥
node -e "console.log(require('crypto').randomBytes(32).toString('hex'))"
```

### 4. 数据库设置

Railway 会自动提供 PostgreSQL 数据库和 `DATABASE_URL` 环境变量。项目已配置为自动使用这个连接。

### 5. 部署

1. Railway 会自动构建和部署你的应用
2. 部署完成后，你会获得一个公共 URL
3. 访问 `https://your-app.railway.app/admin` 创建管理员账户

## 项目结构

```
├── config/
│   ├── admin.js          # 管理面板配置
│   ├── api.js            # API 配置
│   ├── database.js       # 数据库配置
│   ├── middlewares.js    # 中间件配置
│   └── server.js         # 服务器配置
├── src/
│   └── index.js          # 应用入口
├── .env.example          # 环境变量示例
├── package.json          # 项目依赖
├── railway.json          # Railway 配置
└── README.md
```

## 开发模式特性

- **热重载**: 代码更改时自动重启
- **详细日志**: 开发友好的错误信息
- **管理面板**: 完整的内容管理界面
- **API 文档**: 自动生成的 API 文档

## 环境配置

### 开发环境 (本地)
- 使用 SQLite 数据库
- 端口: 1337
- 热重载启用

### 生产环境 (Railway)
- 使用 PostgreSQL 数据库
- 动态端口 (Railway 提供)
- 优化的安全设置

## 故障排除

### 常见问题

1. **数据库连接失败**
   - 确保 Railway 已提供 `DATABASE_URL`
   - 检查数据库服务是否正常运行

2. **管理面板无法访问**
   - 确保 `ADMIN_JWT_SECRET` 已设置
   - 检查 CORS 配置

3. **应用启动失败**
   - 检查所有必需的环境变量是否已设置
   - 查看 Railway 部署日志

### 查看日志

在 Railway 控制台中查看实时日志：
```bash
railway logs
```

## 安全注意事项

- 所有密钥都应该是随机生成的
- 不要在代码中硬编码敏感信息
- 定期更新依赖包
- 在生产环境中考虑启用 SSL

## 支持

- [Strapi 文档](https://docs.strapi.io/)
- [Railway 文档](https://docs.railway.app/)
- [GitHub Issues](https://github.com/your-username/your-repo/issues)
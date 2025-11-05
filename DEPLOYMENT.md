# 部署指南

本文档说明如何部署 Verse 项目到生产环境。

## 📋 目录

- [Web 应用部署](#web-应用部署)
- [微信小程序部署](#微信小程序部署)
- [数据库配置](#数据库配置)
- [环境变量配置](#环境变量配置)
- [Nginx 配置](#nginx-配置)
- [Docker 部署](#docker-部署)
- [常见问题](#常见问题)

## Web 应用部署

### 方式 1: 传统部署

#### 1. 构建项目

```bash
cd verse-api
npm install
npm run build
```

#### 2. 启动生产服务器

```bash
npm start
# 或使用 PM2
pm2 start ecosystem.config.js
```

#### 3. 配置 Nginx

参考 `nginx/nginx.conf` 配置文件，根据您的实际域名和证书路径进行配置。

### 方式 2: Docker 部署

#### 1. 构建 Docker 镜像

```bash
cd verse-api
docker build -t verse-api:latest .
```

#### 2. 运行容器

```bash
docker run -d \
  --name verse-api \
  -p 3200:3200 \
  --env-file .env \
  verse-api:latest
```

#### 3. 使用 Docker Compose

创建 `docker-compose.yml`:

```yaml
version: '3.8'
services:
  app:
    build: .
    ports:
      - "3200:3200"
    env_file:
      - .env
    restart: unless-stopped
```

运行：

```bash
docker-compose up -d
```

## 微信小程序部署

### 1. 配置项目

在微信开发者工具中：

1. 打开项目
2. 配置 `project.config.json` 中的 AppID
3. 配置服务器域名和业务域名

### 2. 上传代码

1. 在微信开发者工具中点击"上传"
2. 填写版本号和项目备注
3. 提交审核

### 3. 发布

审核通过后，在微信公众平台提交发布。

## 数据库配置

### MySQL 数据库设置

1. **创建数据库**

```sql
CREATE DATABASE `TangPoems` CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
```

2. **导入数据**

```bash
mysql -u root -p TangPoems < db/dump-nextJS-202401290617.sql
```

3. **创建用户（可选）**

```sql
CREATE USER 'app_user'@'localhost' IDENTIFIED BY 'your_password';
GRANT ALL PRIVILEGES ON TangPoems.* TO 'app_user'@'localhost';
FLUSH PRIVILEGES;
```

### 数据库连接配置

在 `.env` 文件中配置：

```env
DB_HOST=your_database_host
DB_USER=your_database_user
DB_PASSWORD=your_database_password
DB_DATABASE=TangPoems
DB_PORT=3306
```

## 环境变量配置

### 必需的环境变量

#### 数据库配置
- `DB_HOST`: 数据库主机地址
- `DB_USER`: 数据库用户名
- `DB_PASSWORD`: 数据库密码
- `DB_DATABASE`: 数据库名称
- `DB_PORT`: 数据库端口（可选，默认 3306）

#### 微信小程序配置
- `APPID_KEY`: 微信小程序 AppID
- `APP_SECRET`: 微信小程序 Secret

#### 腾讯云配置
- `TENCENT_CLOUD_SECRET_ID`: 腾讯云 SecretId
- `TENCENT_CLOUD_SECRET_KEY`: 腾讯云 SecretKey
- `TENCENT_CLOUD_BUCKET`: COS 存储桶名称
- `TENCENT_CLOUD_REGION`: COS 区域

#### 应用配置
- `PROXY_URL`: API 代理地址
- `IMAGE_HOSTNAME`: 图片域名

### 生产环境配置建议

1. **使用环境变量管理服务**
   - AWS Secrets Manager
   - Azure Key Vault
   - HashiCorp Vault

2. **不要将敏感信息提交到代码仓库**
   - 确保 `.env` 在 `.gitignore` 中
   - 使用 CI/CD 平台的环境变量功能

3. **定期轮换密钥**
   - 定期更新数据库密码
   - 定期更新 API 密钥

## Nginx 配置

### 基本配置

参考 `nginx/nginx.conf`，主要配置项：

1. **域名配置**
   ```nginx
   server_name www.your-domain.com your-domain.com;
   ```

2. **SSL 证书**
   ```nginx
   ssl_certificate /path/to/your/certificate.crt;
   ssl_certificate_key /path/to/your/private.key;
   ```

3. **反向代理**
   ```nginx
   location / {
       proxy_pass http://127.0.0.1:3200;
       proxy_set_header Host $host;
       proxy_set_header X-Real-IP $remote_addr;
   }
   ```

### SSL 证书配置

推荐使用 Let's Encrypt 免费证书：

```bash
# 安装 certbot
sudo apt-get install certbot python3-certbot-nginx

# 获取证书
sudo certbot --nginx -d your-domain.com -d www.your-domain.com
```

## Docker 部署

### Dockerfile

项目已包含 `Dockerfile`，可以直接使用：

```bash
docker build -t verse-api .
docker run -p 3200:3200 --env-file .env verse-api
```

### 使用 PM2

项目包含 `ecosystem.config.js` 配置文件：

```bash
# 安装 PM2
npm install -g pm2

# 启动应用
pm2 start ecosystem.config.js

# 查看状态
pm2 status

# 查看日志
pm2 logs
```

## 常见问题

### 1. 数据库连接失败

**问题**: 无法连接到数据库

**解决方案**:
- 检查数据库服务是否运行
- 检查防火墙设置
- 验证环境变量配置
- 检查数据库用户权限

### 2. 构建失败

**问题**: `npm run build` 失败

**解决方案**:
- 检查 Node.js 版本（需要 >= 18.0.0）
- 清除缓存：`rm -rf node_modules .next dist`
- 重新安装依赖：`npm install`
- 检查环境变量是否配置

### 3. 静态资源加载失败

**问题**: 图片或静态资源无法加载

**解决方案**:
- 检查 `IMAGE_HOSTNAME` 环境变量
- 检查 Nginx 配置中的静态文件路径
- 检查文件权限

### 4. 微信小程序配置问题

**问题**: 小程序无法连接服务器

**解决方案**:
- 检查服务器域名配置
- 检查业务域名配置
- 检查 SSL 证书是否有效
- 检查 API 地址是否正确

### 5. 性能优化建议

- 使用 CDN 加速静态资源
- 启用 Gzip 压缩
- 使用 Redis 缓存
- 数据库连接池优化
- 图片压缩和懒加载

## 监控和日志

### 日志管理

- 使用 PM2 日志：`pm2 logs`
- 使用 Docker 日志：`docker logs verse-api`
- 配置日志轮转

### 监控建议

- 服务器资源监控（CPU、内存、磁盘）
- 应用性能监控（APM）
- 错误追踪（Sentry 等）
- 数据库监控

## 备份和恢复

### 数据库备份

```bash
# 备份
mysqldump -u root -p TangPoems > backup.sql

# 恢复
mysql -u root -p TangPoems < backup.sql
```

### 定期备份

建议设置定时任务（cron）自动备份：

```bash
# 每天凌晨 2 点备份
0 2 * * * mysqldump -u root -p password TangPoems > /backup/db_$(date +\%Y\%m\%d).sql
```

## 安全建议

1. **使用 HTTPS**
   - 配置 SSL 证书
   - 强制 HTTPS 重定向

2. **防火墙配置**
   - 只开放必要端口
   - 限制数据库访问

3. **定期更新**
   - 更新依赖包
   - 更新系统补丁

4. **访问控制**
   - 使用强密码
   - 限制数据库用户权限
   - 使用 SSH 密钥认证

## 联系支持

如果遇到部署问题，请：

1. 查看项目文档
2. 搜索已有的 Issues
3. 创建新的 Issue 描述问题

---

**注意**: 生产环境部署前，请确保所有敏感信息已正确配置，并测试所有功能。


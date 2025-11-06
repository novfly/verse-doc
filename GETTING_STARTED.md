# 快速开始指南

本指南将帮助您快速上手 Verse 项目。

## 📋 目录

- [项目简介](#项目简介)
- [环境准备](#环境准备)
- [Web 应用快速开始](#web-应用快速开始)
- [微信小程序快速开始](#微信小程序快速开始)
- [Python 脚本使用](#python-脚本使用)
- [常见问题](#常见问题)

## 项目简介

Verse 是一个古诗词学习平台，包含：

- **Web 应用** (`verse-api`): 基于 Next.js 的全功能 Web 应用
- **微信小程序** (`verse-miniprogram`): 基于微信小程序原生框架的移动端应用
- **Python 脚本** (`verse-api/python`): 数据处理的辅助脚本

## 环境准备

### 必需软件

- **Node.js**: >= 18.0.0
- **npm**: >= 9.0.0
- **MySQL**: >= 5.7
- **Python**: >= 3.7 (仅用于 Python 脚本)

### 可选软件

- **Docker**: 用于容器化部署
- **PM2**: 用于进程管理
- **微信开发者工具**: 用于小程序开发

## Web 应用快速开始

### 1. 克隆项目

```bash
git clone https://github.com/novfly/verse-api.git
cd verse-api
```

### 2. 安装依赖

```bash
npm install
```

### 3. 配置环境变量

```bash
# 复制环境变量模板
cp env.example .env

# 编辑 .env 文件，填入您的配置
# 至少需要配置数据库连接信息
```

`.env` 文件示例：

```env
DB_HOST=localhost
DB_USER=root
DB_PASSWORD=your_password
DB_DATABASE=TangPoems
DB_PORT=3306

PROXY_URL=http://localhost:3200
IMAGE_HOSTNAME=localhost
```

### 4. 准备数据库

```bash
# 创建数据库
mysql -u root -p
CREATE DATABASE TangPoems CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;

# 导入数据（如果有 SQL 文件）
mysql -u root -p TangPoems < db/dump-nextJS-202401290617.sql
```

### 5. 启动开发服务器

```bash
npm run dev
```

访问 http://localhost:3200

### 6. 构建生产版本

```bash
npm run build
npm start
```

详细说明请参考 [verse-api/README.md](https://github.com/novfly/verse-api/blob/main/README.md)

## 微信小程序快速开始

### 1. 克隆项目

```bash
git clone https://github.com/novfly/verse-miniprogram.git
cd verse-miniprogram
```

### 2. 安装依赖

```bash
npm install
```

### 3. 配置

#### 方式 1: 使用配置文件（推荐）

```bash
# 1. 复制配置文件模板到项目根目录
cp config.example.js config.local.js

# 2. 编辑 config.local.js 文件，填入您的配置

# 3. 将配置文件复制到 miniprogram 目录下
cp config.local.js miniprogram/config.local.js
```

`config.local.js` 文件示例：

```javascript
module.exports = {
  WEBVIEW_DOMAIN: "https://your-domain.com",
  COS_DOMAIN: "https://your-bucket.cos.region.myqcloud.com",
  API_BASE_URL: "https://your-domain.com/api/",
  WECHAT_APPID: "your_wechat_appid",
  FINCLIP_APPID: "your_finclip_appid",
  CONTACT_EMAIL: "your-contact@example.com",
};
```

**⚠️ 重要：** 
- `miniprogram/config.local.js` 是必需的配置文件，必须创建后才能运行项目
- 代码会从 `miniprogram/config.local.js` 加载配置，如果不存在会报错并提示如何配置

#### 方式 2: 配置 JSON 文件（可选）

`project.config.json` 和 `fide.project.config.json` 中的 `appid` 需要单独配置：

##### 方式 2.1: 手动填写

编辑 `project.config.json`:
```json
{
  "appid": "your_wechat_appid"  // 替换为您的微信小程序 AppID
}
```

编辑 `fide.project.config.json`:
```json
{
  "appid": "your_finclip_appid"  // 替换为您的 FinClip AppID
}
```

**注意：** JSON 文件需要手动填写，因为 JSON 文件不能像 JavaScript 文件那样动态读取配置。

### 4. 在微信开发者工具中打开

1. 打开微信开发者工具
2. 选择"导入项目"
3. 选择项目目录
4. 输入 AppID（已在 project.config.json 中配置）

### 5. 配置服务器域名

在微信公众平台配置：

1. **服务器域名**: 配置您的 API 地址
2. **业务域名**: 配置您的 WebView 域名

详细说明请参考 [verse-miniprogram/README.md](https://github.com/novfly/verse-miniprogram/blob/main/README.md)

## Python 脚本使用

### 1. 安装依赖

```bash
cd verse-api/python
pip install -r requirements.txt
```

### 2. 配置环境变量

#### 方式 1: 使用 .env 文件（推荐）

确保 `verse-api/.env` 文件存在并包含数据库配置。

#### 方式 2: 直接设置环境变量

```bash
export DB_HOST=localhost
export DB_USER=root
export DB_PASSWORD=your_password
export DB_DATABASE=TangPoems
```

### 3. 运行脚本

```bash
# 批量更新诗词数据
python b_poetry_main.py

# 批量更新作者数据
python b_poetry_author_main.py

# 查询并转换数据
python query.py
```

详细说明请参考 [verse-api/python/README.md](https://github.com/novfly/verse-api/blob/main/python/README.md)

## 常见问题

### Q: 数据库连接失败

**A**: 检查以下几点：

1. 数据库服务是否运行
2. 环境变量是否正确配置
3. 数据库用户是否有权限
4. 防火墙是否阻止连接

### Q: 小程序无法连接服务器

**A**: 检查以下几点：

1. 微信公众平台是否配置了服务器域名
2. API 地址是否正确
3. SSL 证书是否有效
4. 服务器是否可访问

### Q: 构建失败

**A**: 检查以下几点：

1. Node.js 版本是否 >= 18.0.0
2. 依赖是否完整安装
3. 环境变量是否配置
4. 清除缓存后重试：`rm -rf node_modules .next dist && npm install`

### Q: 环境变量不生效

**A**: 检查以下几点：

1. `.env` 文件是否在正确位置
2. 变量名是否正确
3. 是否需要重启开发服务器
4. Next.js 需要重启才能加载新的环境变量

### Q: Python 脚本无法连接数据库

**A**: 检查以下几点：

1. 是否安装了 `python-dotenv`（如果使用 .env 文件）
2. 环境变量是否正确设置
3. 数据库服务是否运行
4. 网络连接是否正常

## 下一步

- 查看各项目的 [README.md](https://github.com/novfly/verse-api/blob/main/README.md)
- 查看 [部署指南](./DEPLOYMENT.md)
- 了解 [如何贡献](./CONTRIBUTING.md)

## 获取帮助

如果遇到问题：

1. 查看项目文档
2. 搜索已有的 Issues：
   - [verse-api Issues](https://github.com/novfly/verse-api/issues)
   - [verse-miniprogram Issues](https://github.com/novfly/verse-miniprogram/issues)
3. 创建新的 Issue 描述问题

---

**提示**: 首次运行前，请确保所有环境变量已正确配置，数据库已准备就绪。


# Verse 共享文档

本文件夹包含 Verse 项目中两个子项目（`verse-api` 和 `verse-miniprogram`）共享的文档。

## 📱 项目预览

### 微信小程序

<div align="center">
  <img src="./img/gh_3f325001159f_1280.jpg" alt="微信小程序 Demo" width="400" />
</div>

## 📄 共享文档

以下文档在两个项目中完全相同或高度相似，因此统一管理在此处：

- **[LICENSE](./LICENSE)** - Apache License 2.0 开源协议
- **[GETTING_STARTED.md](./GETTING_STARTED.md)** - 快速开始指南（包含 Web 应用、小程序、Python 脚本的完整教程）
- **[DEPLOYMENT.md](./DEPLOYMENT.md)** - 生产环境部署指南（包含两个项目的部署说明）
- **[CODE_OF_CONDUCT.md](./CODE_OF_CONDUCT.md)** - 社区行为准则
- **[CONTRIBUTING.md](./CONTRIBUTING.md)** - 贡献指南（通用版本）
- **[AUTHORS.md](./AUTHORS.md)** - 贡献者名单

## 📋 如何在项目中使用

### 方式 1：使用 GitHub URL 引用（推荐 ✅）

**这是当前推荐的方式，适用于两个项目分别提交到不同的 GitHub 仓库。**

在您的项目（`verse-api` 或 `verse-miniprogram`）的 README.md 或其他文档中，直接使用 GitHub URL 链接到共享文档。

**示例代码：**

```markdown
## 📄 开源协议

本项目采用 [Apache License 2.0](https://github.com/novfly/verse-doc/blob/main/LICENSE) 开源协议。

## 🤝 贡献指南

请参考 [贡献指南](https://github.com/novfly/verse-doc/blob/main/CONTRIBUTING.md)。

## 📚 其他共享文档

- [行为准则](https://github.com/novfly/verse-doc/blob/main/CODE_OF_CONDUCT.md)
- [部署指南](https://github.com/novfly/verse-doc/blob/main/DEPLOYMENT.md)
- [贡献者名单](https://github.com/novfly/verse-doc/blob/main/AUTHORS.md)
```

**说明：** 上面的代码块展示了需要复制到您项目 README.md 中的 Markdown 代码。代码块的作用是：
- 显示原始的 Markdown 语法，方便您复制
- 如果不用代码块包裹，这些链接会被渲染成可点击的格式，而不是展示代码本身

**优点：**
- ✅ 每个仓库保持独立，不需要复制文件
- ✅ 文档更新时，所有项目自动引用最新版本
- ✅ 符合 GitHub 仓库独立管理的最佳实践
- ✅ 在 GitHub 上可以直接点击链接查看文档

**当前状态：** `verse-api` 和 `verse-miniprogram` 项目已采用此方式。

### 方式 2：复制文件到各项目

**适用于：需要每个仓库都有完整的文档副本（例如某些组织要求）**

如果您需要每个项目仓库都包含这些文档的副本，可以将文档复制到各项目中：

```bash
# 复制到 verse-api
cp verse-doc/LICENSE verse-api/
cp verse-doc/CODE_OF_CONDUCT.md verse-api/
cp verse-doc/CONTRIBUTING.md verse-api/
cp verse-doc/AUTHORS.md verse-api/
cp verse-doc/DEPLOYMENT.md verse-api/

# 复制到 verse-miniprogram
cp verse-doc/LICENSE verse-miniprogram/
cp verse-doc/CODE_OF_CONDUCT.md verse-miniprogram/
cp verse-doc/CONTRIBUTING.md verse-miniprogram/
cp verse-doc/AUTHORS.md verse-miniprogram/
cp verse-doc/DEPLOYMENT.md verse-miniprogram/
```

**注意：** 
- 如果使用此方式，更新文档时需要手动同步到所有项目
- 确保保持各项目中的文档版本一致

### 方式 3：符号链接（仅限本地开发）

**⚠️ 注意：GitHub 不支持符号链接，此方式仅适用于本地开发环境**

在本地开发环境中，可以使用符号链接来引用共享文档：

```bash
# 在 verse-api 项目中创建符号链接
cd verse-api
ln -s ../verse-doc/LICENSE LICENSE
ln -s ../verse-doc/CODE_OF_CONDUCT.md CODE_OF_CONDUCT.md
ln -s ../verse-doc/CONTRIBUTING.md CONTRIBUTING.md
ln -s ../verse-doc/AUTHORS.md AUTHORS.md
ln -s ../verse-doc/DEPLOYMENT.md DEPLOYMENT.md

# 在 verse-miniprogram 项目中创建符号链接
cd verse-miniprogram
ln -s ../verse-doc/LICENSE LICENSE
ln -s ../verse-doc/CODE_OF_CONDUCT.md CODE_OF_CONDUCT.md
ln -s ../verse-doc/CONTRIBUTING.md CONTRIBUTING.md
ln -s ../verse-doc/AUTHORS.md AUTHORS.md
ln -s ../verse-doc/DEPLOYMENT.md DEPLOYMENT.md
```

**说明：**
- `ln -s` 命令创建符号链接（类似 Windows 的快捷方式）
- `../verse-doc/LICENSE` 是源文件路径
- `LICENSE` 是在当前项目中创建的链接文件
- 这样在本地开发时，可以直接访问文档，但提交到 GitHub 时符号链接不会工作

## 📝 项目特定文档

以下文档包含项目特定内容，保留在各项目目录中：

- `README.md` - 项目说明和快速开始
- `SECURITY.md` - 项目特定的安全配置说明
- `CHANGELOG.md` - 项目特定的变更历史
- `FAQ.md` - 项目特定的常见问题
- `BUILD_SECURITY.md` - 构建安全说明（仅 verse-api）

## 🔄 更新文档

当需要更新共享文档时：

1. 修改 `verse-doc/` 中的文档
2. 如果使用**方式 2（复制文件）**，需要手动同步到所有项目
3. 如果使用**方式 1（GitHub URL）**，所有项目会自动引用最新版本

## 📚 文档结构

```
verse-doc/
├── LICENSE              # Apache 2.0 许可证
├── GETTING_STARTED.md   # 快速开始指南（包含所有子项目）
├── DEPLOYMENT.md        # 部署指南（包含所有子项目）
├── CODE_OF_CONDUCT.md   # 行为准则
├── CONTRIBUTING.md      # 贡献指南（通用）
├── AUTHORS.md           # 贡献者名单
└── README.md            # 本文件
```

---

**总结：** 对于 GitHub 开源项目，推荐使用**方式 1（GitHub URL 引用）**，这是最简单且最符合 GitHub 仓库管理的方式。

# Verse 共享文档

本文件夹包含 Verse 项目中两个子项目（`verse-api` 和 `verse-miniprogram`）共享的文档。

## 📄 共享文档

以下文档在两个项目中完全相同或高度相似，因此统一管理在此处：

- **[LICENSE](./LICENSE)** - Apache License 2.0 开源协议
- **[CODE_OF_CONDUCT.md](./CODE_OF_CONDUCT.md)** - 社区行为准则
- **[CONTRIBUTING.md](./CONTRIBUTING.md)** - 贡献指南（通用版本）
- **[AUTHORS.md](./AUTHORS.md)** - 贡献者名单
- **[DEPLOYMENT.md](./DEPLOYMENT.md)** - 生产环境部署指南（包含两个项目的部署说明）

## 📋 使用说明

### 方式 1：符号链接（推荐）

在项目中使用符号链接指向共享文档：

```bash
# 在 verse-api 项目中
cd verse-api
ln -s ../verse-doc/LICENSE LICENSE
ln -s ../verse-doc/CODE_OF_CONDUCT.md CODE_OF_CONDUCT.md
ln -s ../verse-doc/CONTRIBUTING.md CONTRIBUTING.md
ln -s ../verse-doc/AUTHORS.md AUTHORS.md
ln -s ../verse-doc/DEPLOYMENT.md DEPLOYMENT.md

# 在 verse-miniprogram 项目中
cd verse-miniprogram
ln -s ../verse-doc/LICENSE LICENSE
ln -s ../verse-doc/CODE_OF_CONDUCT.md CODE_OF_CONDUCT.md
ln -s ../verse-doc/CONTRIBUTING.md CONTRIBUTING.md
ln -s ../verse-doc/AUTHORS.md AUTHORS.md
ln -s ../verse-doc/DEPLOYMENT.md DEPLOYMENT.md
```

### 方式 2：直接引用（推荐用于 GitHub 仓库）

在项目的 README.md 中使用 GitHub URL 引用共享文档：

```markdown
## 📄 开源协议

本项目采用 [Apache License 2.0](https://github.com/novfly/verse-doc/blob/main/LICENSE) 开源协议。

## 🤝 贡献指南

请参考 [共享贡献指南](https://github.com/novfly/verse-doc/blob/main/CONTRIBUTING.md)。
```

### 方式 3：复制到各项目（当前方案）

如果需要独立提交到不同的 GitHub 仓库，可以将这些文档复制到各项目中。在更新时，请确保两个项目的文档保持一致。

## 📝 项目特定文档

以下文档包含项目特定内容，保留在各项目目录中：

- `README.md` - 项目说明和快速开始
- `GETTING_STARTED.md` - 项目特定的快速开始指南
- `SECURITY.md` - 项目特定的安全配置说明
- `CHANGELOG.md` - 项目特定的变更历史
- `FAQ.md` - 项目特定的常见问题
- `BUILD_SECURITY.md` - 构建安全说明（仅 verse-api）

## 🔄 更新文档

当需要更新共享文档时：

1. 修改 `verse-doc/` 中的文档
2. 如果使用复制方式，同步到两个项目
3. 确保两个项目的文档保持一致

## 📚 文档结构

```
verse-doc/
├── LICENSE              # Apache 2.0 许可证
├── CODE_OF_CONDUCT.md   # 行为准则
├── CONTRIBUTING.md      # 贡献指南（通用）
├── AUTHORS.md           # 贡献者名单
├── DEPLOYMENT.md        # 部署指南
└── README.md            # 本文件
```

---

**注意**: 如果两个项目分别提交到不同的 GitHub 仓库，建议将共享文档复制到各项目中，以确保每个仓库的完整性。

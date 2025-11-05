# 贡献指南

感谢您对 Verse 项目的关注！我们欢迎所有形式的贡献。

## 📋 目录

- [行为准则](#行为准则)
- [如何贡献](#如何贡献)
- [开发环境设置](#开发环境设置)
- [代码规范](#代码规范)
- [提交规范](#提交规范)
- [Pull Request 流程](#pull-request-流程)
- [报告问题](#报告问题)
- [功能建议](#功能建议)

## 行为准则

参与本项目时，请遵守以下行为准则：

- 尊重所有贡献者
- 接受建设性的批评
- 关注对社区最有利的事情
- 对其他社区成员表示同理心

详细的行为准则请参考 [CODE_OF_CONDUCT.md](./CODE_OF_CONDUCT.md)。

## 如何贡献

### 报告 Bug

如果您发现了 bug，请：

1. 检查对应项目的 Issues 中是否已有相关问题
2. 如果没有，请创建新的 Issue，包含：
   - 清晰的标题和描述
   - 复现步骤
   - 预期行为
   - 实际行为
   - 环境信息（操作系统、Node.js 版本等）
   - 截图（如果适用）

### 提出功能建议

如果您有功能建议，请：

1. 检查是否已有相关 Issue
2. 创建新的 Issue，描述：
   - 功能的使用场景
   - 为什么需要这个功能
   - 可能的实现方式（可选）

### 提交代码

1. Fork 对应项目
2. 创建特性分支 (`git checkout -b feature/AmazingFeature`)
3. 提交更改 (`git commit -m 'Add some AmazingFeature'`)
4. 推送到分支 (`git push origin feature/AmazingFeature`)
5. 开启 Pull Request

## 开发环境设置

### Web 应用 (verse-api)

```bash
# 1. Fork 并克隆项目
git clone https://github.com/novfly/verse-api.git
cd verse-api

# 2. 安装依赖
npm install

# 3. 配置环境变量
cp env.example .env.local
# 编辑 .env.local 文件，填入配置信息

# 4. 启动开发服务器
npm run dev
```

### 微信小程序 (verse-miniprogram)

```bash
# 1. Fork 并克隆项目
git clone https://github.com/novfly/verse-miniprogram.git
cd verse-miniprogram

# 2. 安装依赖
npm install

# 3. 配置项目
cp config.example.js config.local.js
# 编辑 config.local.js 文件，填入配置信息

# 4. 在微信开发者工具中打开项目
```

详细的安装和配置说明请参考各项目的 README.md。

## 代码规范

### TypeScript/JavaScript

- 使用 ESLint 检查代码规范
- 提交前运行 `npm run lint`（如果项目支持）
- 遵循项目现有的代码风格
- 使用有意义的变量和函数名
- 添加必要的注释

### 代码格式

- 使用 2 个空格缩进
- 使用单引号（除非需要双引号）
- 在语句末尾添加分号
- 使用尾随逗号（trailing commas）

### 文件命名

- 组件文件使用 PascalCase：`UserProfile.tsx`
- 工具文件使用 camelCase：`apiUtils.ts`
- 常量文件使用 UPPER_SNAKE_CASE：`API_CONSTANTS.ts`

## 提交规范

### Commit Message 格式

我们使用约定式提交（Conventional Commits）格式：

```
<type>(<scope>): <subject>

<body>

<footer>
```

### Type 类型

- `feat`: 新功能
- `fix`: 修复 bug
- `docs`: 文档更新
- `style`: 代码格式调整（不影响功能）
- `refactor`: 代码重构
- `perf`: 性能优化
- `test`: 测试相关
- `chore`: 构建过程或辅助工具的变动

### 示例

```
feat(api): 添加用户登录接口

- 实现用户登录功能
- 添加 JWT token 生成
- 添加错误处理

Closes #123
```

### 提交前检查清单

- [ ] 代码已通过 ESLint 检查
- [ ] 已添加必要的注释
- [ ] 已更新相关文档
- [ ] 提交信息清晰明确
- [ ] 没有包含敏感信息（密码、密钥等）

## Pull Request 流程

### 创建 PR 前

1. 确保代码已通过所有检查
2. 确保所有测试通过
3. 更新相关文档
4. 确保没有敏感信息泄露

### PR 描述模板

```markdown
## 变更描述
简要描述本次 PR 的变更内容

## 变更类型
- [ ] Bug 修复
- [ ] 新功能
- [ ] 文档更新
- [ ] 代码重构
- [ ] 性能优化
- [ ] 其他

## 测试
描述如何测试这些变更

## 截图（如果适用）
添加相关截图

## 相关 Issue
关联的 Issue 编号（如 #123）
```

### PR 审查

- 所有 PR 都需要至少一位维护者审查
- 审查者可能会要求修改
- 请及时响应审查意见

## 报告问题

### Bug 报告模板

```markdown
**描述 Bug**
清晰简洁地描述 bug

**复现步骤**
1. 执行 '...'
2. 点击 '...'
3. 看到错误

**预期行为**
描述您期望发生什么

**实际行为**
描述实际发生了什么

**截图**
如果适用，添加截图

**环境信息**
- OS: [e.g. macOS 14.0]
- Node.js 版本: [e.g. 18.0.0]
- 浏览器: [e.g. Chrome 120] (如果是前端问题)

**额外信息**
其他相关信息
```

## 功能建议

### 功能请求模板

```markdown
**功能描述**
清晰简洁地描述您想要的功能

**使用场景**
描述这个功能的使用场景

**可能的实现方式**
如果有想法，描述可能的实现方式

**替代方案**
描述您考虑过的替代方案

**额外信息**
其他相关信息
```

## 开发指南

### 添加新功能

1. 创建功能分支
2. 实现功能
3. 添加测试（如果适用）
4. 更新文档
5. 提交 PR

### 修复 Bug

1. 创建修复分支
2. 编写测试用例（如果可能）
3. 修复 bug
4. 确保测试通过
5. 提交 PR

### 更新文档

文档更新同样欢迎！包括：
- README 文件
- 代码注释
- API 文档
- 使用教程

## 获取帮助

如果您在贡献过程中遇到问题：

1. 查看项目文档
2. 搜索已有的 Issues
3. 创建新的 Issue 询问
4. 联系项目维护者

## 致谢

感谢所有为这个项目做出贡献的开发者！您的贡献让这个项目变得更好。

---

**注意**: 提交代码即表示您同意将您的贡献在 Apache License 2.0 下授权。


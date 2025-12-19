# ClaudeCode插件开发模板

> **作者**：大熊掌门
> **版本**：1.0.0
> **课程**：ClaudeCode纯干货教程第7课

## 🚀 快速开始

这是一个完整的ClaudeCode插件开发模板，基于2025年10月推出的ClaudeCode插件系统。

### 环境要求

- ClaudeCode 2.0+
- Git
- GitHub账号（用于分发）

### 安装和运行

```bash
# 1. 克隆或下载此模板
git clone https://github.com/username/claudecode-plugin-template.git my-plugin
cd my-plugin

# 2. 自定义插件配置
编辑 .claude-plugin/plugin.json 文件

# 3. 添加你的命令和agents
编辑 commands/ 和 agents/ 目录下的文件

# 4. 发布到GitHub
git init
git add .
git commit -m "Initial plugin"
git remote add origin https://github.com/username/my-plugin.git
git push -u origin main

# 5. 创建版本标签
git tag -a v1.0.0 -m "First release"
git push origin v1.0.0
```

## 📁 项目结构

```
my-plugin/
├── .claude-plugin/           # 元数据目录
│   └── plugin.json           # 必需：插件清单文件
├── commands/                 # Slash命令定义
│   ├── hello.md              # 示例：Hello命令
│   ├── deploy.md             # 示例：部署命令
│   └── status.md             # 示例：状态查询命令
├── agents/                   # 专业代理定义
│   ├── code-reviewer.md      # 示例：代码审查代理
│   └── task-manager.md       # 示例：任务管理代理
├── hooks/                    # Hook配置
│   └── hooks.json            # Git hooks配置
├── scripts/                  # 实用脚本
│   ├── pre-commit.sh         # Pre-commit脚本
│   └── deploy.sh             # 部署脚本
├── .mcp.json                 # MCP服务器配置
├── LICENSE                   # 许可证文件
├── CHANGELOG.md              # 版本历史
└── README.md                 # 说明文档
```

## 🛠️ 功能特性

### 1. Slash Commands（斜杠命令）

模板包含三个示例命令：

- `hello` - 显示个性化问候消息
- `deploy` - 部署应用程序
- `status` - 查看项目状态

**使用方法**：`/hello [name]`, `/deploy [environment]`, `/status`

### 2. Specialized Agents（专业代理）

模板包含两个示例代理：

- **Code Reviewer** - 代码质量和安全审查
- **Task Manager** - 项目任务管理和分析

### 3. MCP Servers集成

支持以下外部服务集成：

- GitHub API
- 数据库连接
- API服务
- 文件系统

### 4. Hooks（钩子）

预配置的自动化钩子：

- Pre-commit - 代码提交前检查
- Post-deploy - 部署后验证

## 📝 开发指南

### 添加新命令

1. 在`commands/`目录创建新的`.md`文件：

```markdown
---
description: 你的命令描述
argument-hint: [参数说明]
---

# /your-command

## Purpose
描述命令的目的和用途

## Contract
**Inputs:**
- `$1` — 参数1说明
- `$2` — 参数2说明

**Outputs:** 输出说明

## Instructions
1. 步骤1
2. 步骤2
3. 步骤3
```

2. 在`plugin.json`中注册命令：

```json
{
    "components": {
        "commands": ["your-command"]
    }
}
```

### 添加新Agent

1. 在`agents/`目录创建新的`.md`文件：

```markdown
---
name: Your Agent Name
description: 代理功能描述
tools: ["tool1", "tool2"]
---

You are a specialized agent for...
Describe the agent's capabilities and instructions.
```

2. 在`plugin.json`中注册agent：

```json
{
    "components": {
        "agents": ["your-agent"]
    }
}
```

### 配置MCP服务器

编辑`.mcp.json`文件：

```json
{
    "mcpServers": {
        "your-service": {
            "command": "node",
            "args": ["./your-mcp-server.js"],
            "env": {
                "API_KEY": "${YOUR_API_KEY}",
                "BASE_URL": "https://api.example.com"
            }
        }
    }
}
```

### 添加Hooks

编辑`hooks/hooks.json`：

```json
{
    "pre-commit": {
        "script": "./scripts/pre-commit.sh",
        "description": "Run tests and linting before commit"
    },
    "post-deploy": {
        "script": "./scripts/post-deploy.sh",
        "description": "Verify deployment success"
    }
}
```

## 🧪 测试

```bash
# 本地测试插件配置
cat .claude-plugin/plugin.json | jq . > /dev/null && echo "JSON配置正确"

# 测试命令文件格式
head -20 ./commands/hello.md | grep -E "^(---|description:)" && echo "命令格式正确"

# 验证目录结构
ls -la .claude-plugin/ commands/ agents/ hooks/ && echo "目录结构正确"
```

## 📦 发布和分发

### GitHub发布流程

1. **推送到GitHub仓库**：
```bash
git add .
git commit -m "Release v1.0.0"
git tag -a v1.0.0 -m "Version 1.0.0"
git push origin main --tags
```

2. **用户安装插件**：
```bash
# 添加市场
/plugin marketplace add username/username

# 安装插件
/plugin install my-plugin@username
```

### 版本管理

使用Git标签管理版本：
- `v1.0.0` - 初始版本
- `v1.1.0` - 新功能版本
- `v1.0.1` - 修复版本

## 🔧 自定义开发

### 修改插件信息

编辑`.claude-plugin/plugin.json`中的以下字段：

- `name` - 插件唯一标识
- `displayName` - 显示名称
- `description` - 插件描述
- `version` - 版本号
- `author` - 作者信息
- `repository` - GitHub仓库地址

### 添加依赖

在`plugin.json`中声明依赖：

```json
{
    "dependencies": {
        "plugins": ["base-plugin"],
        "tools": ["docker", "kubectl", "git"]
    }
}
```

### 配置默认设置

```json
{
    "configuration": {
        "defaultSettings": {
            "deployEnvironment": "staging",
            "timeout": 300,
            "enableNotifications": true
        }
    }
}
```

## 📚 学习资源

- [ClaudeCode插件官方文档](https://github.com/anthropics/claude-code/blob/main/plugins/README.md)
- [MCP协议规范](https://modelcontextprotocol.io)
- [插件示例集合](https://github.com/anthropics/claude-code/tree/main/plugins/examples)
- [社区插件市场](https://github.com/topics/claudecode-plugin)

## 🤝 贡献

欢迎提交Issue和Pull Request来改进这个模板！

### 贡献指南

1. Fork 这个仓库
2. 创建你的功能分支 (`git checkout -b feature/AmazingFeature`)
3. 提交你的更改 (`git commit -m 'Add some AmazingFeature'`)
4. 推送到分支 (`git push origin feature/AmazingFeature`)
5. 打开一个 Pull Request

## 📄 许可证

MIT License

## 🎯 最佳实践

### 命名规范

- **插件名称**：使用kebab-case，如`my-awesome-plugin`
- **命令名称**：使用简洁的动词，如`deploy`, `test`, `review`
- **Agent名称**：使用描述性名称，如`security-reviewer`, `performance-analyzer`

### 文档规范

- 每个命令都要有清晰的用途说明
- 参数说明要详细
- 提供使用示例

### 安全考虑

- 不要在插件中硬编码敏感信息
- 使用环境变量存储API密钥
- 验证用户输入

---

> **提示**：这个模板是ClaudeCode纯干货教程第7课的学习材料，更多教程内容请关注"大熊掌门"。

> **GitHub仓库**：https://github.com/MaesHughes/wuxing-blog-comments
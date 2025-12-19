# MCP服务器配置手册

> **课程**：ClaudeCode纯干货教程第7课 - Plugins插件生态
> **用途**：提供常用MCP服务器的详细配置示例

## 🔗 MCP配置基础

### .mcp.json 配置文件结构

```json
{
    "mcpServers": {
        "server-name": {
            "command": "可执行命令",
            "args": ["参数1", "参数2"],
            "env": {
                "环境变量": "值"
            }
        }
    }
}
```

### 环境变量使用规范

- 使用`${VARIABLE_NAME}`格式引用环境变量
- 敏感信息（API密钥、密码）必须使用环境变量
- 建议在项目根目录创建`.env`文件管理环境变量

## 🏢 开发服务集成

### 1. GitHub集成配置

```json
{
    "mcpServers": {
        "github": {
            "command": "npx",
            "args": ["-y", "@modelcontextprotocol/server-github"],
            "env": {
                "GITHUB_PERSONAL_ACCESS_TOKEN": "${GITHUB_TOKEN}"
            }
        }
    }
}
```

**所需环境变量**：
```bash
export GITHUB_TOKEN="ghp_xxxxxxxxxxxxxxxxxxxx"
```

### 2. 数据库集成

#### PostgreSQL配置
```json
{
    "mcpServers": {
        "postgres": {
            "command": "npx",
            "args": ["-y", "@modelcontextprotocol/server-postgres"],
            "env": {
                "DATABASE_URL": "${DATABASE_URL}"
            }
        }
    }
}
```

#### MySQL配置
```json
{
    "mcpServers": {
        "mysql": {
            "command": "npx",
            "args": ["-y", "@modelcontextprotocol/server-mysql"],
            "env": {
                "MYSQL_HOST": "${MYSQL_HOST}",
                "MYSQL_USER": "${MYSQL_USER}",
                "MYSQL_PASSWORD": "${MYSQL_PASSWORD}",
                "MYSQL_DATABASE": "${MYSQL_DATABASE}"
            }
        }
    }
}
```

### 3. 云服务集成

#### AWS集成配置
```json
{
    "mcpServers": {
        "aws-s3": {
            "command": "npx",
            "args": ["-y", "@modelcontextprotocol/server-aws-s3"],
            "env": {
                "AWS_ACCESS_KEY_ID": "${AWS_ACCESS_KEY_ID}",
                "AWS_SECRET_ACCESS_KEY": "${AWS_SECRET_ACCESS_KEY}",
                "AWS_REGION": "${AWS_REGION}",
                "S3_BUCKET": "${S3_BUCKET_NAME}"
            }
        }
    }
}
```

## 🔧 测试与验证

```bash
# 测试所有MCP服务器
claudecode mcp test --all

# 查看MCP服务器状态
claudecode mcp status
```

---

> **注意**：在实际使用前，请确保所有环境变量都已正确设置。
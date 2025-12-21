# Hook系统配置模板集合

> **用途**：ClaudeCode Hook系统的实用配置模板
> **版本**：2025年12月
> **作者**：大熊掌门

## 📋 目录
1. [基础Hook配置](#1-基础hook配置)
2. [开发工作流Hook](#2-开发工作流hook)
3. [质量保证Hook](#3-质量保证hook)
4. [高级控制流Hook](#4-高级控制流hook)
5. [项目特定Hook](#5-项目特定hook)
6. [Hook调试技巧](#6-hook调试技巧)

---

## 1. 基础Hook配置

### 1.1 最小配置
```json
{
  "hooks": {
    "bash": {
      "command": "echo 'Command: {{command}}' >> ~/.claude/logs/bash.log"
    }
  }
}
```

### 1.2 文件操作Hook
```json
{
  "hooks": {
    "edit": {
      "command": "echo 'Edited: {{filename}} at $(date)' >> ~/.claude/logs/edits.log"
    },
    "write": {
      "command": "echo 'Created: {{filename}}' >> ~/.claude/logs/creates.log"
    }
  }
}
```

### 1.3 通知Hook
```json
{
  "hooks": {
    "post-tool-use": {
      "command": "notify-send 'Claude Code' 'Tool {{toolName}} completed'"
    }
  }
}
```

---

## 2. 开发工作流Hook

### 2.1 自动备份Hook
```json
{
  "hooks": {
    "pre-edit": {
      "command": "cp {{filename}} {{filename}}.backup.$(date +%s)"
    }
  }
}
```

### 2.2 Git自动提交Hook
```json
{
  "hooks": {
    "post-write": {
      "command": "git add {{filename}} && git commit -m 'Auto-commit: Updated {{filename}}'"
    }
  }
}
```

### 2.3 依赖管理Hook
```json
{
  "hooks": {
    "write": {
      "command": "if [[ '{{filename}}' == package.json ]]; then npm install; fi"
    }
  }
}
```

---

## 3. 质量保证Hook

### 3.1 代码格式化Hook
```json
{
  "hooks": {
    "edit": {
      "command": "case '{{filename}}' in *.js) npx prettier --write {{filename}} ;; *.py) black {{filename}} ;; *.go) go fmt {{filename}} ;; esac"
    }
  }
}
```

### 3.2 代码检查Hook
```json
{
  "hooks": {
    "post-edit": {
      "command": "case '{{filename}}' in *.js) npx eslint {{filename}} ;; *.py) flake8 {{filename}} ;; esac"
    }
  }
}
```

### 3.3 测试执行Hook
```json
{
  "hooks": {
    "post-write": {
      "command": "if [[ '{{filename}}' == *test* ]] || [[ '{{filename}}' == *.test.* ]]; then npm test -- --testPathPattern={{filename}}; fi"
    }
  }
}
```

---

## 4. 高级控制流Hook

### 4.1 安全检查Hook
```json
{
  "hooks": {
    "write": {
      "command": "check-security.sh {{filename}}",
      "output": "json"
    }
  }
}
```

`check-security.sh` 脚本：
```bash
#!/bin/bash
filename=$1

# 检查敏感信息
if grep -q "password\|secret\|token\|key" "$filename"; then
    echo '{"action": "block", "message": "文件包含可能的敏感信息"}'
    exit 1
fi

echo '{"action": "continue", "message": "安全检查通过"}'
```

### 4.2 批准Hook
```json
{
  "hooks": {
    "pre-tool-use": {
      "command": "ask-approval.sh {{toolName}}",
      "output": "json"
    }
  }
}
```

### 4.3 条件执行Hook
```json
{
  "hooks": {
    "edit": {
      "command": "if [[ '{{filename}}' == production/* ]]; then echo '{\"action\": \"approve\", \"message\": \"即将修改生产文件\"}'; else echo '{\"action\": \"continue\"}'; fi",
      "output": "json"
    }
  }
}
```

---

## 5. 项目特定Hook

### 5.1 React项目Hook
```json
{
  "hooks": {
    "post-edit": {
      "command": "if [[ '{{filename}}' == *.jsx ]] || [[ '{{filename}}' == *.tsx ]]; then npm run lint:fix; fi"
    }
  }
}
```

### 5.2 Python项目Hook
```json
{
  "hooks": {
    "write": {
      "command": "if [[ '{{filename}}' == requirements.txt ]]; then pip install -r {{filename}}; fi"
    }
  }
}
```

### 5.3 Go项目Hook
```json
{
  "hooks": {
    "post-write": {
      "command": "if [[ '{{filename}}' == go.mod ]]; then go mod tidy; fi"
    }
  }
}
```

---

## 6. Hook调试技巧

### 6.1 调试模式Hook
```json
{
  "hooks": {
    "bash": {
      "command": "echo '[DEBUG] Command: {{command}}' >> ~/.claude/debug.log && {{command}}"
    }
  }
}
```

### 6.2 性能监控Hook
```json
{
  "hooks": {
    "pre-tool-use": {
      "command": "echo '$(date) - Starting: {{toolName}}' >> ~/.claude/performance.log"
    },
    "post-tool-use": {
      "command": "echo '$(date) - Completed: {{toolName}}' >> ~/.claude/performance.log"
    }
  }
}
```

### 6.3 错误追踪Hook
```json
{
  "hooks": {
    "bash": {
      "command": "{{command}} 2>&1 | tee -a ~/.claude/error.log"
    }
  }
}
```

---

## 🔧 Hook管理脚本

### 启用Hook配置
```bash
#!/bin/bash
# enable-hooks.sh
CONFIG_DIR="$HOME/.claude"
BACKUP_DIR="$CONFIG_DIR/backups/$(date +%s)"

# 备份当前配置
mkdir -p "$BACKUP_DIR"
cp "$CONFIG_DIR/settings.json" "$BACKUP_DIR/" 2>/dev/null

# 应用新的Hook配置
cp settings.json "$CONFIG_DIR/"

echo "Hook配置已启用"
echo "备份位置: $BACKUP_DIR"
```

### 禁用所有Hook
```bash
#!/bin/bash
# disable-hooks.sh
CONFIG_DIR="$HOME/.claude"

# 创建无Hook的配置
echo '{}' > "$CONFIG_DIR/settings.json"

echo "所有Hook已禁用"
```

### 查看Hook状态
```bash
#!/bin/bash
# hook-status.sh
CONFIG_FILE="$HOME/.claude/settings.json"

if grep -q '"hooks"' "$CONFIG_FILE"; then
    echo "✅ Hook系统已启用"
    echo "当前Hook配置："
    jq '.hooks' "$CONFIG_FILE"
else
    echo "❌ Hook系统未启用"
fi
```

---

## 📝 最佳实践

### 1. Hook命名规范
- 使用描述性的名称
- 保持简短但清晰
- 避免特殊字符

### 2. 错误处理
```json
{
  "hooks": {
    "edit": {
      "command": "format-code.sh {{filename}} || echo '格式化失败，请手动检查'"
    }
  }
}
```

### 3. 性能考虑
- 避免阻塞主要操作
- 使用异步操作处理耗时任务
- 合理使用缓存

### 4. 安全性
- 不在Hook中硬编码敏感信息
- 验证输入参数
- 使用最小权限原则

---

## 🚀 高级技巧

### 1. 动态Hook加载
```json
{
  "hooks": {
    "bash": {
      "command": "load-project-hooks.sh"
    }
  }
}
```

### 2. 环境相关Hook
```json
{
  "hooks": {
    "write": {
      "command": "if [ '$NODE_ENV' = 'production' ]; then production-hook.sh {{filename}}; else development-hook.sh {{filename}}; fi"
    }
  }
}
```

### 3. Hook链
```json
{
  "hooks": {
    "pre-edit": {
      "command": "hook1.sh && hook2.sh && hook3.sh"
    }
  }
}
```

---

## ⚠️ 注意事项

1. **备份重要**：修改Hook配置前总是备份
2. **测试先行**：在测试环境中验证Hook
3. **文档记录**：为自定义Hook编写文档
4. **版本控制**：将Hook配置纳入版本控制
5. **定期审查**：定期检查和更新Hook配置

---

**立即开始使用这些模板，让Hook系统为你自动处理重复任务！**
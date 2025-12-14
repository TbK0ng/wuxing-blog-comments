# ClaudeCode 教程资源

![ClaudeCode](https://img.shields.io/badge/ClaudeCode-AI%20Assistant-blue)
![Author](https://img.shields.io/badge/Author-大熊掌门-green)
![Platform](https://img.shields.io/badge/Platform-Windows%20%7C%20macOS%20%7C%20Linux-lightgrey)

> 📚 **零基础快速掌握ClaudeCode，30分钟上手AI编程助手**

## 📖 项目简介

本项目是《ClaudeCode纯干货教程》的配套资源库，包含完整的学习材料、实战脚本和配置模板。通过系统化的教程，帮助开发者快速掌握ClaudeCode的使用技巧，提升编程效率。

## 🎯 学习目标

- ✅ 30分钟快速上手ClaudeCode
- ✅ 掌握核心命令与高效操作
- ✅ 学会配置个性化开发环境
- ✅ 解决常见问题与故障排除
- ✅ 实战项目演练

## 📚 课程目录

### 第1课：30分钟快速上手ClaudeCode 📂
[点击进入](第1课-30分钟快速上手ClaudeCode/)

- **安装脚本**：一键安装ClaudeCode（Windows/macOS/Linux）
- **配置模板**：多种场景配置文件（基础/性能/安全/前端/后端/团队）
- **问题解决**：常见错误诊断与修复方案

### 课程预告（即将更新）
- 第2课：核心命令与高效操作
- 第3课：高级配置与插件开发
- 第4课：实战项目：AI辅助开发
- 第5课：团队协作最佳实践

## 🚀 快速开始

### 1. 环境要求
- Node.js 18.0 或更高版本
- 至少 2GB 可用内存
- 稳定的网络连接

### 2. 一键安装
```bash
# Windows
.\第1课-30分钟快速上手ClaudeCode\scripts\install.bat

# macOS/Linux
chmod +x 第1课-30分钟快速上手ClaudeCode/scripts/install.sh
./第1课-30分钟快速上手ClaudeCode/scripts/install.sh
```

### 3. 配置API密钥
```bash
export ANTHROPIC_API_KEY="your-api-key-here"
```

### 4. 验证安装
```bash
claude --version
claude "你好，ClaudeCode！"
```

## 📁 项目结构

```
wuxingcodes-claudecode2025/
├── README.md                          # 项目说明（本文件）
├── 第1课-30分钟快速上手ClaudeCode/     # 第一课资源
│   ├── README.md                      # 课程说明
│   ├── 01-安装脚本.md                 # 安装指南
│   ├── 02-配置文件模板.md             # 配置指南
│   ├── 03-常见问题解决方案.md         # 故障排除
│   ├── scripts/                       # 所有脚本
│   │   ├── install.bat/.sh           # 安装脚本
│   │   ├── diagnose-*.bat/.sh        # 诊断工具
│   │   ├── fix-*.bat/.sh/.ps1        # 问题修复
│   │   └── cleanup-*.bat/.sh         # 清理脚本
│   └── configs/                       # 配置文件
│       ├── config-*.json             # 各种配置
│       ├── .env.example              # 环境变量模板
│       └── vscode-settings.json      # VS Code设置
└── 更新日志.md                        # 版本更新记录
```

## 💡 使用技巧

### 配置推荐
```bash
# 复制性能优化配置
cp 第1课-30分钟快速上手ClaudeCode/configs/config-performance.json ~/.claude/config.json

# 前端开发者专用配置
cp 第1课-30分钟快速上手ClaudeCode/configs/config-frontend.json ~/.claude/config.json
```

### 常用命令
```bash
# 创建新项目
claude init

# 快速诊断问题
./第1课-30分钟快速上手ClaudeCode/scripts/diagnose-unix.sh

# 清理并重装
./第1课-30分钟快速上手ClaudeCode/scripts/cleanup-unix.sh
```

## 🔗 相关链接

### 官方资源
- [ClaudeCode 官方文档](https://docs.anthropic.com/claude-code)
- [ClaudeCode GitHub 仓库](https://github.com/anthropics/claude-code)
- [Anthropic 官网](https://www.anthropic.com)

### 学习资源
- **🌟 作者博客**: [https://blog.wuxingcodes.com/](https://blog.wuxingcodes.com/)
  - 定期分享AI编程技巧
  - ClaudeCode实战案例
  - 最新技术动态解读
- [社区论坛](https://community.anthropic.com)
- [视频教程](https://www.youtube.com/results?search_query=claude+code+tutorial)

## 🤝 贡献指南

欢迎提交 Issue 和 Pull Request！

1. Fork 本仓库
2. 创建特性分支 (`git checkout -b feature/AmazingFeature`)
3. 提交更改 (`git commit -m 'Add some AmazingFeature'`)
4. 推送到分支 (`git push origin feature/AmazingFeature`)
5. 开启 Pull Request

## 📄 许可证

本项目采用 MIT 许可证 - 查看 [LICENSE](LICENSE) 文件了解详情

## 👨‍💻 作者

**大熊掌门** | 全平台搜索"大熊掌门"

- 📧 [邮箱联系](mailto:contact@wuxingcodes.com)
- 🐙 [GitHub](https://github.com/YourGitHub)
- 🐦 [Twitter](https://twitter.com/YourTwitter)
- 📝 [技术博客](https://blog.wuxingcodes.com/)

## ⭐ 支持项目

如果这个项目对你有帮助，请给它一个 ⭐ Star！

---

<div align="center">
  <p>💚 感谢使用 ClaudeCode 教程 💚</p>
  <p>Made with ❤️ by 大熊掌门</p>
</div>
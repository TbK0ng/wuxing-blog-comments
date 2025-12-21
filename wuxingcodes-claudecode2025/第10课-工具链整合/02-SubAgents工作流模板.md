# SubAgents工作流模板

> **用途**：ClaudeCode SubAgents工作流设计模板集合
> **版本**：2025年12月
> **作者**：大熊掌门

## 📋 目录
1. [基础工作流模板](#1-基础工作流模板)
2. [并行处理模板](#2-并行处理模板)
3. [高级协作模式](#3-高级协作模式)
4. [行业特定模板](#4-行业特定模板)
5. [动态工作流生成](#5-动态工作流生成)

---

## 1. 基础工作流模板

### 1.1 需求分析流程

```yaml
# workflows/requirements-analysis.yaml
name: requirements-analysis
description: 从想法到需求的完整分析流程

agents:
  product-owner:
    role: 产品负责人
    capabilities:
      - 需求收集
      - 用户故事编写
      - 优先级排序

  business-analyst:
    role: 业务分析师
    capabilities:
      - 业务流程分析
      - 需求文档编写
      - 用例设计

stages:
  - stage: idea-collection
    agent: product-owner
    tasks:
      - 收集用户反馈
      - 分析业务需求
      - 初步可行性评估
    output: ideas.json

  - stage: requirement-definition
    agent: business-analyst
    depends_on: idea-collection
    tasks:
      - 编写需求文档
      - 创建用户故事
      - 定义验收标准
    output: requirements.md

  - stage: prioritization
    agent: product-owner
    depends_on: requirement-definition
    tasks:
      - 评估业务价值
      - 技术难度分析
      - 优先级排序
    output: backlog.json
```

### 1.2 代码审查流程

```yaml
# workflows/code-review.yaml
name: code-review
description: 全面的代码审查流程

agents:
  code-reviewer:
    role: 代码审查专家
    capabilities:
      - 代码质量检查
      - 安全审计
      - 性能分析

  security-specialist:
    role: 安全专家
    capabilities:
      - 漏洞扫描
      - 安全最佳实践
      - 合规性检查

stages:
  - stage: initial-review
    agent: code-reviewer
    tasks:
      - 代码规范检查
      - 逻辑正确性验证
      - 性能评估
    output: review-comments.md

  - stage: security-review
    agent: security-specialist
    parallel: true
    tasks:
      - 安全漏洞扫描
      - 依赖安全检查
      - 敏感信息检测
    output: security-report.md

  - stage: final-approval
    agent: code-reviewer
    depends_on: [initial-review, security-review]
    tasks:
      - 综合评估
      - 生成报告
      - 批准决策
    output: final-review.json
```

### 1.3 部署流程

```yaml
# workflows/deployment.yaml
name: deployment
description: 应用部署流程

agents:
  devops-engineer:
    role: DevOps工程师
    capabilities:
      - CI/CD管道
      - 容器化
      - 监控配置

  qa-engineer:
    role: QA工程师
    capabilities:
      - 测试执行
      - 环境验证
      - 回归测试

stages:
  - stage: preparation
    agent: devops-engineer
    tasks:
      - 构建应用
      - 准备部署环境
      - 配置监控
    output: deployment-ready/

  - stage: testing
    agent: qa-engineer
    depends_on: preparation
    tasks:
      - 冒烟测试
      - 集成测试
      - 性能测试
    output: test-results/

  - stage: deployment
    agent: devops-engineer
    depends_on: testing
    tasks:
      - 执行部署
      - 验证部署
      - 监控启动
    output: deployment-status.json
```

---

## 2. 并行处理模板

### 2.1 前后端并行开发

```yaml
# workflows/parallel-frontend-backend.yaml
name: parallel-development
description: 前后端并行开发工作流

agents:
  frontend-developer:
    role: 前端开发
    capabilities:
      - UI开发
      - 组件实现
      - 响应式设计

  backend-developer:
    role: 后端开发
    capabilities:
      - API开发
      - 数据库设计
      - 业务逻辑

  integration-specialist:
    role: 集成专家
    capabilities:
      - 接口联调
      - 端到端测试
      - 问题诊断

stages:
  - stage: api-design
    agent: backend-developer
    tasks:
      - 设计API接口
      - 创建OpenAPI文档
    output: api-spec.yaml

  - stage: parallel-development
    parallel: true
    branches:
      - branch: frontend
        agent: frontend-developer
        tasks:
          - 开发UI组件
          - 实现业务逻辑
        input: api-spec.yaml
        output: frontend/

      - branch: backend
        agent: backend-developer
        tasks:
          - 实现API接口
          - 开发数据模型
        input: api-spec.yaml
        output: backend/

  - stage: integration
    agent: integration-specialist
    depends_on: parallel-development
    tasks:
      - 前后端联调
      - 修复集成问题
      - 端到端测试
    input: [frontend/, backend/]
    output: integrated-app/
```

### 2.2 多功能并行处理

```yaml
# workflows/multi-feature.yaml
name: multi-feature-development
description: 多功能特性并行开发

agents:
  feature-leads:
    - name: feature-a-lead
      role: 特性A负责人
    - name: feature-b-lead
      role: 特性B负责人
    - name: feature-c-lead
      role: 特性C负责人

stages:
  - stage: parallel-features
    parallel: true
    branches:
      - branch: feature-a
        agent: feature-a-lead
        tasks:
          - 需求分析
          - 设计实现
          - 单元测试

      - branch: feature-b
        agent: feature-b-lead
        tasks:
          - 原型设计
          - 功能开发
          - 集成测试

      - branch: feature-c
        agent: feature-c-lead
        tasks:
          - 技术调研
          - POC实现
          - 评估报告

  - stage: feature-merge
    agent: integration-specialist
    depends_on: parallel-features
    tasks:
      - 合并功能分支
      - 冲突解决
      - 整体测试
```

---

## 3. 高级协作模式

### 3.1 瀑布式开发

```yaml
# workflows/agile-sprint.yaml
name: agile-sprint
description: 瀑布式开发冲刺

agents:
  scrum-master:
    role: Scrum Master
    capabilities:
      - 冲刺计划
      - 进度跟踪
      - 障碍移除

  development-team:
    - name: dev-1
      role: 全栈开发者
    - name: dev-2
      role: 后端开发者
    - name: dev-3
      role: 前端开发者

  qa-team:
    - name: qa-1
      role: 测试工程师
    - name: qa-2
      role: 自动化测试

stages:
  - stage: sprint-planning
    agent: scrum-master
    tasks:
      - 分解用户故事
      - 估算工作量
      - 制定冲刺计划
    output: sprint-plan.json

  - stage: sprint-execution
    parallel: true
    duration: "2 weeks"
    branches:
      - branch: development
        agents: development-team
        tasks:
          - 功能开发
          - 代码实现
          - 单元测试
        daily-sync: true

      - branch: testing
        agents: qa-team
        tasks:
          - 测试用例编写
          - 自动化测试
          - Bug验证

  - stage: sprint-review
    agent: scrum-master
    depends_on: sprint-execution
    tasks:
      - 演示功能
      - 收集反馈
      - 冲刺回顾
    output: sprint-review.md
```

### 3.2 DevOps流水线

```yaml
# workflows/devops-pipeline.yaml
name: devops-pipeline
description: DevOps CI/CD流水线

agents:
  build-engineer:
    role: 构建工程师
    capabilities:
      - 代码编译
      - 依赖管理
      - 静态分析

  test-engineer:
    role: 测试工程师
    capabilities:
      - 自动化测试
      - 性能测试
      - 安全测试

  deploy-engineer:
    role: 部署工程师
    capabilities:
      - 环境管理
      - 发布管理
      - 监控配置

stages:
  - stage: build
    agent: build-engineer
    trigger: [push, pull_request]
    tasks:
      - 代码检出
      - 依赖安装
      - 构建应用
      - 静态分析
    output: build-artifacts/

  - stage: test
    agent: test-engineer
    depends_on: build
    parallel: true
    branches:
      - branch: unit-tests
        tasks: [单元测试, 覆盖率检查]
      - branch: integration-tests
        tasks: [集成测试, API测试]
      - branch: security-tests
        tasks: [安全扫描, 漏洞检测]

  - stage: deploy
    agent: deploy-engineer
    depends_on: test
    environment: staging
    tasks:
      - 环境准备
      - 应用部署
      - 健康检查
      - 监控配置
```

---

## 4. 行业特定模板

### 4.1 电商开发

```yaml
# workflows/e-commerce.yaml
name: e-commerce-development
description: 电商平台开发工作流

agents:
  product-manager:
    role: 产品经理
    capabilities:
      - 商品管理
      - 订单流程
      - 支付集成

  ux-designer:
    role: UX设计师
    capabilities:
      - 用户界面设计
      - 购物流程优化
      - 移动端适配

stages:
  - stage: feature-design
    agents: [product-manager, ux-designer]
    tasks:
      - 功能规划
      - 原型设计
      - 用户体验优化

  - stage: implementation
    parallel: true
    branches:
      - branch: catalog
        tasks: [商品展示, 搜索功能, 分类管理]
      - branch: cart-checkout
        tasks: [购物车, 结算流程, 订单管理]
      - branch: payment
        tasks: [支付集成, 安全防护, 退款处理]
```

### 4.2 金融科技

```yaml
# workflows/fintech.yaml
name: fintech-development
description: 金融科技应用开发

agents:
  security-specialist:
    role: 安全专家
    capabilities:
      - 合规检查
      - 风险评估
      - 审计追踪

  qa-engineer:
    role: QA工程师
    capabilities:
      - 压力测试
      - 安全测试
      - 合规验证

stages:
  - stage: security-review
    agent: security-specialist
    tasks:
      - 安全需求分析
      - 威胁建模
      - 安全架构设计

  - stage: implementation
    agent: developer
    depends_on: security-review
    tasks:
      - 安全编码
      - 加密实现
      - 审计日志

  - stage: compliance-testing
    agent: qa-engineer
    depends_on: implementation
    tasks:
      - PCI DSS测试
      - 渗透测试
      - 合规验证
```

---

## 5. 动态工作流生成

### 5.1 基于复杂度的动态调整

```python
# dynamic_workflow_generator.py
import yaml

class DynamicWorkflowGenerator:
    def __init__(self):
        self.templates = {
            'simple': {
                'stages': ['development', 'basic-testing', 'deployment']
            },
            'medium': {
                'stages': ['design', 'development', 'integration-testing', 'deployment']
            },
            'complex': {
                'stages': ['requirements', 'design', 'development',
                          'comprehensive-testing', 'security-review', 'deployment']
            }
        }

    def generate_workflow(self, project_analysis):
        complexity = project_analysis['complexity']
        risk_level = project_analysis['risk']
        team_size = project_analysis['team_size']

        base_template = self.templates[complexity]
        workflow = self._customize_workflow(base_template, project_analysis)

        return workflow

    def _customize_workflow(self, template, analysis):
        workflow = template.copy()

        # 添加安全审查（如果是高风险项目）
        if analysis['risk'] == 'high':
            workflow['stages'].append('security-audit')

        # 添加性能测试（如果是大项目）
        if analysis['expected_users'] > 10000:
            workflow['stages'].append('performance-testing')

        return workflow
```

### 5.2 基于团队的动态分配

```yaml
# workflows/dynamic-team-allocation.yaml
name: dynamic-team-allocation
description: 根据团队技能动态分配工作

rules:
  team_skill_match:
    react-project: ["frontend-specialist", "react-expert"]
    node-api: ["backend-developer", "api-designer"]
    ml-project: ["data-scientist", "ml-engineer"]
    mobile-app: ["mobile-developer", "ui-ux-designer"]

  workload_balancing:
    max_tasks_per_agent: 3
    parallel_threshold: 5

dynamic_allocation:
  algorithm: "skill-match-first"
  fallback: "round-robin"
```

### 5.3 实时工作流调整

```python
# adaptive_workflow.py
class AdaptiveWorkflow:
    def __init__(self):
        self.current_state = {}
        self.adjustment_rules = []

    def monitor_and_adjust(self, workflow, metrics):
        adjustments = []

        # 如果任务耗时过长，增加并行度
        if metrics['avg_task_time'] > self.thresholds['task_time']:
            adjustments.append({
                'action': 'increase_parallelism',
                'value': 2
            })

        # 如果错误率过高，增加审查步骤
        if metrics['error_rate'] > self.thresholds['error_rate']:
            adjustments.append({
                'action': 'add_review_stage',
                'stage': 'additional-code-review'
            })

        return self.apply_adjustments(workflow, adjustments)
```

---

## 🔧 使用指南

### 1. 工作流启动

```bash
# 启动预定义工作流
claude-code workflow start requirements-analysis

# 启动自定义工作流
claude-code workflow start --config my-workflow.yaml

# 监控工作流执行
claude-code workflow monitor --name requirements-analysis
```

### 2. 工作流管理

```bash
# 列出所有工作流
claude-code workflow list

# 查看工作流详情
claude-code workflow show requirements-analysis

# 暂停工作流
claude-code workflow pause requirements-analysis

# 恢复工作流
claude-code workflow resume requirements-analysis
```

### 3. 工作流调试

```bash
# 启用调试模式
claude-code workflow start --debug requirements-analysis

# 查看工作流日志
claude-code workflow logs --name requirements-analysis

# 分析工作流性能
claude-code workflow analyze --name requirements-analysis
```

---

## 💡 最佳实践

1. **工作流版本控制**：将工作流配置纳入版本控制
2. **模块化设计**：将复杂工作流分解为可复用模块
3. **错误处理**：为每个阶段定义错误处理策略
4. **监控指标**：设置关键性能指标进行监控
5. **持续优化**：基于使用数据持续改进工作流

---

**立即使用这些模板，构建高效的SubAgents协作工作流！**
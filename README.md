# 🔄 AICW - AI批判式协作工作流

> **让AI审查AI，你只管提需求**

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Version](https://img.shields.io/badge/version-4.3.1-blue.svg)]()

---

## 🎯 这是什么？

AICW (AI Critic Collaboration Workflow) 是一套**让多个AI互相审查**的工作流。

**核心理念**：不追求完美，只追求MVP（最小可行产品）。

- **只拦P0**（致命问题），其他的登记下来，先跑起来再说
- **两轮审查**，强制停机，拒绝无限循环
- **执行AI有权拒绝**不合理的优化建议

---

## ⚡ 快速开始（3步）

### Step 1：复制 Executor Prompt

把 [prompts/executor_prompt.md](./prompts/executor_prompt.md) 的内容设置为执行AI的System Prompt（Claude/GPT均可）

### Step 2：复制 Critic Prompt

把 [prompts/critic_prompt.md](./prompts/critic_prompt.md) 的内容设置为审查AI的System Prompt

### Step 3：开始工作流

```
你(需求) → Executor(P1初稿) → Critic(C1全量扫描) 
         → Executor(决策表+P2终稿) → Critic(C2放行) → 🚀开干
```

---

## 🧠 核心规则

### P0判定尺（只有这3种情况才算P0）

| 类型 | 定义 | 示例 |
|------|------|------|
| **无法开始** | 第1步动作无法执行 | 缺关键输入/权限/资源 |
| **无法验收** | 没有成/败标准 | 改完也不知道对不对 |
| **红线风险** | 一执行就可能造成不可接受损失 | 安全/合规/资金暴露 |

### Stop Rule（硬性停机）

满足任一条件，工作流**必须终止**：

1. **P0清零**：审查者找不到任何P0
2. **轮次耗尽**：到达第2轮（C2）结尾

> ⚠️ 除非存在P0，否则**强制PASS**。残留P1/P2 **严禁**作为打回理由。

---

## 📁 仓库结构

```
AICW-Workflow/
├── README.md                           # 你正在看的文件
├── prompts/
│   ├── executor_prompt.md              # 执行AI的System Prompt
│   ├── critic_prompt.md                # 审查AI的System Prompt
│   └── workflow_overview.md            # 工作流总览
├── examples/
│   └── case_knowledge_base.md          # 实战案例：3天搭建投资研究知识库
├── CHANGELOG.md                        # 版本更新记录
└── LICENSE                             # MIT License
```

---

## 📖 实战案例

使用这套工作流，我在**2天内产出112个研究文件**，相当于过去一个月的量。

| 研究项目 | 文件数 | 耗时 |
|----------|--------|------|
| 塔勒布期权思维 | 44个 | 1天 |
| 索罗斯反身性 | 68个 | 半天 |

详细案例请看：[examples/case_knowledge_base.md](./examples/case_knowledge_base.md)

---

## 🔧 适用场景

- ✅ 代码开发与审查
- ✅ 项目规划
- ✅ 研究报告产出
- ✅ 市场分析
- ✅ 任何需要"产出+检查"的场景

---

## 📝 版本历史

| 版本 | 日期 | 主要变更 |
|------|------|----------|
| V4.3.1 | 2026-01-09 | 增加P0判定尺、Stop Rule硬性停机 |
| V4.0 | 2026-01-01 | 引入两轮审查机制 |
| V3.0 | 2025-12-15 | 增加遗留风险承诺书 |

---

## 🤝 贡献

欢迎提Issue或PR！

如果这个工作流对你有帮助，请给个 ⭐ Star，让更多人看到。

---

## 📜 License

MIT License - 随便用，注明出处即可。

---

## 👤 关于作者

- 公众号：Do a bit
- 这套工作流的灵感来自 Boris Cherny（Claude Code之父）的分享

# 🔄 AICW - AI Critic Collaboration Workflow

> **Let AI review AI, you just set the requirements.**
>
> **让AI审查AI，你只管提需求。**

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Version](https://img.shields.io/badge/version-4.3.1-blue.svg)]()

---

## 🎯 What is this? | 这是什么？

AICW (AI Critic Collaboration Workflow) is a workflow that enables **multiple AIs to review each other's work**.

AICW（AI批判式协作工作流）是一套**让多个AI互相审查**的工作流。

**Core Philosophy | 核心理念**: Don't pursue perfection, pursue MVP. | 不追求完美，只追求MVP。

- **Only block P0** (fatal issues), log everything else and start executing | **只拦P0**（致命问题），其他的登记下来，先跑起来再说
- **Two-round review**, forced termination, no infinite loops | **两轮审查**，强制停机，拒绝无限循环
- **Executor AI can reject** unreasonable suggestions | **执行AI有权拒绝**不合理的优化建议

---

## 📦 Two Usage Modes | 两种使用方式

### Mode 1: Multi-Model Collaboration ⭐ | 多模型协作（推荐）

**For | 适用于**: Claude (Executor) + GPT (Critic) or any AI combination

This is the author's actual approach. | 这是作者实际在用的方式。

```
Antigravity (Claude)              GPT
      ↓                            ↓
executor_prompt.md            critic_prompt.md
      ↓                            ↓
   Output Plan    ───copy───→   Output Review
   输出方案卡      ───复制───→   输出审查卡
```

### Mode 2: Claude Code Skill | 单模型版

Place `skills/SKILL.md` in your project's `skills/` directory.

把 `skills/SKILL.md` 放到项目的 `skills/` 目录下即可。

---

## 🧠 Core Rules | 核心规则

### P0 Criteria | P0判定尺

| Type 类型 | Definition 定义 | Example 示例 |
|-----------|-----------------|--------------|
| **Cannot Start 无法开始** | Step 1 cannot execute 第1步无法执行 | Missing input 缺输入 |
| **Cannot Verify 无法验收** | No success/fail criteria 没有成败标准 | Can't tell if done 不知道对不对 |
| **Red Line Risk 红线风险** | Unacceptable loss 不可接受损失 | Security/compliance 安全合规 |

### Stop Rule | 硬性停机

Workflow **must terminate** when | 满足任一条件，工作流**必须终止**：

1. **P0 = 0**: No P0 issues found | 审查者找不到任何P0
2. **Round limit**: Reached Round 2 (C2) | 到达第2轮结尾

> ⚠️ Unless P0 exists, **force PASS**. | 除非存在P0，否则**强制PASS**。

---

## 📁 Repository Structure | 仓库结构

```
AICW-Workflow/
├── README.md                    # Bilingual 双语文档
├── prompts/                     # ⭐ Multi-model 多模型版
│   ├── executor_prompt.md       # For Claude 给Claude
│   ├── critic_prompt.md         # For GPT 给GPT
│   └── workflow_overview.md
├── skills/                      # Single-model 单模型版
│   └── SKILL.md
├── examples/
│   └── case_knowledge_base.md   # Case study 实战案例
└── assets/
    └── wechat_qrcode.jpg
```

---

## 📖 Case Study | 实战案例

Using this workflow, I produced **112 research files in 2 days** — equivalent to a month's work.

使用这套工作流，我在**2天内产出112个研究文件**，相当于过去一个月的量。

| Project 项目 | Files 文件数 | Time 耗时 |
|--------------|--------------|-----------|
| Taleb Options 塔勒布期权 | 44 | 1 day |
| Soros Reflexivity 索罗斯反身性 | 68 | 0.5 day |

---

## 🔧 Use Cases | 适用场景

- ✅ Code development & review | 代码开发与审查
- ✅ Project planning | 项目规划
- ✅ Research reports | 研究报告
- ✅ Market analysis | 市场分析
- ✅ Any "output + review" scenario | 任何需要"产出+检查"的场景

---

## ❓ FAQ

### Q: Why multi-model over single-model? | 为什么推荐多模型？

**A**: Having one AI review its own output creates blind spots. Different AIs find more issues.

让一个AI审查自己的输出，容易有盲区。用不同的AI互相审查，能发现更多问题。

### Q: What is Antigravity? | Antigravity是什么？

**A**: A VSCode plugin / standalone app that provides free Claude Code access.

一个VSCode插件/独立App，可以免费使用Claude Code。

---

## 📜 License

MIT License

---

## 👤 Author | 关于作者

- WeChat 公众号: **多少做点 do a bit**
- Inspired by Boris Cherny (Claude Code creator)

<img src="./assets/wechat_qrcode.jpg" width="200" alt="WeChat QR Code">

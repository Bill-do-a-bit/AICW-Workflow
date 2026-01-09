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

## 📦 两种使用方式

### 方式1：多模型协作（推荐⭐）

适用于：**Claude执行 + GPT审查** 或任意AI组合

这是作者实际在用的方式。利用不同AI的优势：

- **Claude/Antigravity**：执行力强，代码生成稳定
- **GPT**：逻辑推理强，审查更严格

```
Antigravity (Claude)              GPT
      ↓                            ↓
executor_prompt.md            critic_prompt.md
      ↓                            ↓
    输出方案卡    ───复制───→    输出审查卡
      ↓                            ↓
    修改方案      ←──复制────   指出P0问题
```

**使用步骤**：

1. 在 Claude/Antigravity 中设置 `prompts/executor_prompt.md` 作为System Prompt
2. 在 GPT 中设置 `prompts/critic_prompt.md` 作为System Prompt
3. 手动在两个AI之间传递方案和审查意见

---

### 方式2：Claude Code Skill（单模型）

适用于：想在**单个Claude会话**内完成全部流程

把 `skills/SKILL.md` 放到项目的 `skills/` 目录下，Claude会自动识别。

```
your-project/
└── skills/
    └── SKILL.md    # 复制这个文件
```

**触发方式**：直接说"帮我用AICW规划一个任务"

> ⚠️ 注意：单模型方式的审查效果可能不如多模型协作，因为同一个AI审查自己的输出容易有盲区。

---

## ⚡ 快速开始（多模型协作版）

### Step 1：设置执行AI（Claude/Antigravity）

复制 `prompts/executor_prompt.md` 的内容，在对话开头发送给Claude。

### Step 2：设置审查AI（GPT）

复制 `prompts/critic_prompt.md` 的内容，在新GPT对话中设置为System Prompt。

### Step 3：开始工作流

```
1) 你向Claude提需求
2) Claude输出 [P1] 方案卡
3) 复制方案卡给GPT，说"Round=C1，请审查"
4) GPT输出 [C1] 审查卡
5) 复制审查意见给Claude，Claude输出决策表 + [P2] 最终稿
6) 复制给GPT，说"Round=C2，请审查"
7) GPT判定 PASS → 🚀开干
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
├── prompts/                            # ⭐ 多模型协作版（推荐）
│   ├── executor_prompt.md              # 执行AI的Prompt（给Claude）
│   ├── critic_prompt.md                # 审查AI的Prompt（给GPT）
│   └── workflow_overview.md            # 工作流总览
├── skills/                             # 单模型版
│   └── SKILL.md                        # Claude Code Skill
├── examples/
│   └── case_knowledge_base.md          # 实战案例
├── CHANGELOG.md
└── LICENSE
```

---

## 📖 实战案例

使用这套工作流（Claude执行 + GPT审查），我在**2天内产出112个研究文件**，相当于过去一个月的量。

| 研究项目 | 文件数 | 耗时 |
|----------|--------|------|
| 塔勒布期权思维 | 44个 | 1天 |
| 索罗斯反身性 | 68个 | 半天 |

**关键价值**：GPT审查时发现了我遗漏的"时间线"模块（判定为P0），逼着Claude补上了——这是我自己检查不会发现的。

详细案例请看：[examples/case_knowledge_base.md](./examples/case_knowledge_base.md)

---

## 🔧 适用场景

- ✅ 代码开发与审查
- ✅ 项目规划
- ✅ 研究报告产出
- ✅ 市场分析
- ✅ 任何需要"产出+检查"的场景

---

## ❓ FAQ

### Q: 为什么推荐多模型协作而不是单模型？

**A**: 让一个AI审查自己的输出，容易有盲区。用不同的AI互相审查，能发现更多问题。就像代码审查不应该让作者自己审一样。

### Q: 可以用其他AI组合吗？

**A**: 可以。比如：

- Gemini（执行）+ Claude（审查）
- Claude（执行）+ Claude（审查，不同对话）
- 任意组合都行，核心是**两个独立的AI视角**

### Q: Antigravity是什么？

**A**: Antigravity是一个VSCode插件/独立App，可以免费使用Claude Code。只需登录Google账号即可。

---

## 📝 版本历史

| 版本 | 日期 | 主要变更 |
|------|------|----------|
| V4.3.1 | 2026-01-09 | 明确多模型协作为推荐方式、增加P0判定尺 |
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

- 公众号：**多少做点 do a bit**
- 这套工作流的灵感来自 Boris Cherny（Claude Code之父）的分享

<img src="./assets/wechat_qrcode.jpg" width="200" alt="微信公众号二维码">

# 🔄 AICW - AI Critic Collaboration Workflow

> **Let AI review AI, you just set the requirements.**
>
> **让AI审查AI，你只管提需求。**

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Version](https://img.shields.io/badge/version-4.3.1-blue.svg)]()
[![中文文档](https://img.shields.io/badge/文档-中文版-red.svg)](./README_CN.md)

---

## 🎯 What is this?

AICW (AI Critic Collaboration Workflow) is a workflow that enables **multiple AIs to review each other's work**.

**Core Philosophy**: Don't pursue perfection, pursue MVP (Minimum Viable Product).

- **Only block P0** (fatal issues), log everything else and start executing
- **Two-round review**, forced termination, no infinite loops
- **Executor AI can reject** unreasonable optimization suggestions

---

## 📦 Two Usage Modes

### Mode 1: Multi-Model Collaboration (Recommended ⭐)

**For: Claude (Executor) + GPT (Critic)** or any AI combination

This is the author's actual approach. Leverage different AI strengths:

- **Claude/Antigravity**: Strong execution, stable code generation
- **GPT**: Strong logical reasoning, stricter review

```
Antigravity (Claude)              GPT
      ↓                            ↓
executor_prompt.md            critic_prompt.md
      ↓                            ↓
   Output Plan    ───copy───→   Output Review
      ↓                            ↓
   Revise Plan    ←──copy────   Flag P0 Issues
```

---

### Mode 2: Claude Code Skill (Single Model)

**For: Complete entire workflow within a single Claude session**

Place `skills/SKILL.md` in your project's `skills/` directory.

```
your-project/
└── skills/
    └── SKILL.md
```

> ⚠️ Note: Single-model review may be less effective than multi-model collaboration.

---

## 🧠 Core Rules

### P0 Criteria (Only these 3 cases qualify as P0)

| Type | Definition | Example |
|------|------------|---------|
| **Cannot Start** | Step 1 cannot execute | Missing input/permission/resource |
| **Cannot Verify** | No success/fail criteria | Can't tell if it's done right |
| **Red Line Risk** | Execution causes unacceptable loss | Security/compliance/financial exposure |

### Stop Rule (Hard Termination)

Workflow **must terminate** when either condition is met:

1. **P0 = 0**: Reviewer finds no P0 issues
2. **Round limit**: Reached end of Round 2 (C2)

> ⚠️ Unless P0 exists, **force PASS**. Remaining P1/P2 **cannot** be used as rejection reasons.

---

## 📁 Repository Structure

```
AICW-Workflow/
├── README.md                           # English (you are here)
├── README_CN.md                        # 中文版
├── prompts/                            # ⭐ Multi-model version (Recommended)
│   ├── executor_prompt.md              # Executor AI Prompt (for Claude)
│   ├── critic_prompt.md                # Critic AI Prompt (for GPT)
│   └── workflow_overview.md            # Workflow overview
├── skills/                             # Single-model version
│   └── SKILL.md                        # Claude Code Skill
├── examples/
│   └── case_knowledge_base.md          # Case study
├── CHANGELOG.md
└── LICENSE
```

---

## 📖 Case Study

Using this workflow (Claude executor + GPT reviewer), I produced **112 research files in 2 days** — equivalent to a month's work.

| Research Project | Files | Time |
|------------------|-------|------|
| Taleb Options Thinking | 44 | 1 day |
| Soros Reflexivity | 68 | 0.5 day |

**Key Value**: GPT review discovered a missing "Timeline" module (flagged as P0), forcing Claude to add it — something I wouldn't have caught myself.

---

## 🔧 Use Cases

- ✅ Code development & review
- ✅ Project planning
- ✅ Research report generation
- ✅ Market analysis
- ✅ Any scenario requiring "output + review"

---

## ❓ FAQ

### Q: Why recommend multi-model over single-model?

**A**: Having one AI review its own output creates blind spots. Different AIs reviewing each other find more issues. Like code review shouldn't be done by the author.

### Q: Can I use other AI combinations?

**A**: Yes. For example:

- Gemini (executor) + Claude (reviewer)
- Claude (executor) + Claude (reviewer, different session)
- Any combination works — the key is **two independent AI perspectives**

### Q: What is Antigravity?

**A**: Antigravity is a VSCode plugin / standalone app that provides free Claude Code access. Just log in with a Google account.

---

## 📝 Version History

| Version | Date | Changes |
|---------|------|---------|
| V4.3.1 | 2026-01-09 | Multi-model as recommended approach, P0 criteria |
| V4.0 | 2026-01-01 | Two-round review mechanism |
| V3.0 | 2025-12-15 | Risk commitment form |

---

## 🤝 Contributing

Issues and PRs welcome!

If this workflow helps you, please give it a ⭐ Star.

---

## 📜 License

MIT License

---

## 👤 Author

- WeChat Public Account: **多少做点 do a bit**
- Inspired by Boris Cherny (Claude Code creator)

<img src="./assets/wechat_qrcode.jpg" width="200" alt="WeChat QR Code">

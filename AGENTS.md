# AGENTS.md

本文件为 AI 代理协作指引。详细文档请参阅 [README.md](./README.md)。

## 项目概述

Paper Master 是一个 AI 驱动的结课论文创作系统，通过 **5+2 角色协作**（5 核心 + 2 选用）将论文要求转化为高质量输出。

## 角色与流程速查

### 核心角色

| 角色 | 文件 | 职责 |
|------|------|------|
| **Format_Analyst** | `roles/Format_Analyst.md` | 分析格式要求，输出格式规范 |
| **Research_Collector** | `roles/Research_Collector.md` | 网络查询资料，整理参考文献 |
| **Outline_Architect** | `roles/Outline_Architect.md` | 创建论文大纲结构 |
| **Content_Writer** | `roles/Content_Writer.md` | 分部分撰写论文内容 |
| **HTML_Formatter** | `roles/HTML_Formatter.md` | 生成 Word 兼容 HTML |

### 选用角色（按需调用）

| 角色 | 文件 | 职责 | 触发条件 |
|------|------|------|----------|
| **Code_Implementer** | `roles/Code_Implementer.md` | 编写 Python 代码 | 论文含算法/实验需求 |
| **Figure_Designer** | `roles/Figure_Designer.md` | 生成顶会风格配图 | 用户要求配图 |

### 工作流程

```
Format_Analyst
    ↓
Research_Collector
    ↓
Outline_Architect
    ↓
Content_Writer ←→ Code_Implementer (按需)
    ↓          ←→ Figure_Designer (按需)
HTML_Formatter
```

---

## 角色切换协议（强制执行）

### 1. 强制阅读角色定义

**在执行任何阶段之前，必须先使用 `view_file` 工具阅读对应的角色定义文件。**

| 阶段 | 必须阅读的文件 | 触发条件 |
|------|---------------|----------|
| 格式分析 | `roles/Format_Analyst.md` | 用户提出新的论文需求 |
| 资料查询 | `roles/Research_Collector.md` | 格式规范完成后 |
| 大纲创建 | `roles/Outline_Architect.md` | 资料汇编完成后 |
| 代码实现 | `roles/Code_Implementer.md` | 格式规范标注需要代码（选用） |
| 内容撰写 | `roles/Content_Writer.md` | 大纲确认后 |
| 图片生成 | `roles/Figure_Designer.md` | 格式规范标注需要配图（选用） |
| HTML 生成 | `roles/HTML_Formatter.md` | 所有部分内容完成后 |

> ⚠️ **禁止跳过**：不得在未阅读角色定义文件的情况下直接执行该角色的任务。

### 2. 显式角色切换标记

切换角色时，**必须输出以下格式的标记**：

```markdown
---
## 【角色切换：[角色名称]】

📖 **阅读角色定义**: `roles/[角色文件名].md`
📋 **当前任务**: [简述本阶段要完成的任务]
---
```

### 3. 阶段检查点

每个阶段完成后，**必须输出检查清单确认**：

```markdown
## ✅ [角色名] 阶段完成

- [x] 已完成的任务项
- [ ] **下一步**: [下一个角色]
```

---

## 关键规则（必须遵守）

### 1. 格式分析师初次确认（强制）

在任何内容分析之前，**必须先完成以下确认**：

1. **论文类型** - 结课论文 / 实验报告 / 课程设计等
2. **格式模板** - 用户指定的模板文件路径
3. **字数要求** - 总字数及各部分分配
4. **参考文献格式** - 默认 GB/T 7714
5. **特殊要求** - 图表、公式等
6. **代码实现** - 是否需要（触发 Code_Implementer）
7. **配图需求** - 是否需要（触发 Figure_Designer）

### 2. 内容撰写规则

- **逐部分撰写**：每次只写一个章节
- **单独保存**：每个部分保存为独立 MD 文件
- **学术风格**：使用正式学术语言，避免口语化
- **合理引用**：整合参考资料，标注引用

### 3. HTML 输出规范

- **字体**：正文宋体，标题黑体
- **字号**：正文小四/12pt，标题按层级递增
- **行距**：1.5倍
- **段首**：缩进 2em
- **兼容性**：确保 Word 可正确识别样式

---

## 项目目录结构

```
project/
├── 格式规范.md           # Format_Analyst 输出
├── 资料汇编.md           # Research_Collector 输出
├── 参考文献.md           # Research_Collector 输出
├── 论文大纲.md           # Outline_Architect 输出
├── content/              # Content_Writer 输出
│   ├── 00_摘要.md
│   ├── 01_引言.md
│   └── ...
├── code/                 # Code_Implementer 输出（选用）
│   ├── main.py
│   └── README.md
├── figures/              # Figure_Designer 输出（选用）
│   ├── fig1_framework.png
│   └── README.md
└── output/               # HTML_Formatter 输出
    └── 论文.html
```

---

## 常用命令

```bash
# 初始化项目
python tools/project_manager.py init <项目名称>

# 验证项目
python tools/project_manager.py validate <项目路径>
```

---

## 重要资源

| 资源 | 路径 |
|------|------|
| 用户模板 | `templates/user/` |
| HTML 模板 | `templates/html/` |
| 工作流指南 | `docs/workflow_guide.md` |
| HTML 转 Word | `docs/html_to_word_guide.md` |
| 顶会风格 Prompt | `顶会风格描述prompt.md` |

---

## AI 代理重要提示

### 核心原则

- 本项目定义 AI 角色协作机制
- 质量取决于对格式规范的严格执行
- **角色切换协议是强制要求，不可跳过**

### 流程要点

- 格式分析师的「初次确认」是**强制要求**
- 内容撰写必须**逐部分**进行
- HTML 输出必须保证 **Word 兼容性**
- 参考文献默认使用 **GB/T 7714** 格式

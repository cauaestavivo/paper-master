# Paper Master - AI 辅助结课论文创作框架

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

一个基于 AI 的智能论文创作系统，通过多角色协作，将论文要求转化为高质量的学术论文，**输出 Word 兼容的 HTML 格式**。

---

## 🚀 快速开始

### 三步开始

```
1️⃣ 准备论文要求
   使用 Mineru 将论文要求文档转换为 MD 格式，放入 templates/user/ 目录

2️⃣ 打开 AI 编辑器
   使用 Antigravity/Cursor/Copilot 打开本项目

3️⃣ 开始对话
   告诉 AI："我需要写一篇关于 XX 的结课论文，格式要求在 templates/user/ 中"
```

### 使用示例

```
用户：我需要写一篇关于"大数据在应急管理中的应用"的结课论文，字数要求3000字

AI（Format_Analyst）：好的，请确认以下信息...
   1. 论文类型：[建议] 结课论文
   2. 格式模板：[请指定] templates/user/ 中的模板文件
   3. 字数要求：3000字
   4. 参考文献格式：[默认] GB/T 7714
   ...
```

---

## 📋 核心工作流程

```
论文要求文档
    ↓ (Mineru 转换)
[Format_Analyst] 格式分析师
    ↓ 输出《格式规范》
[Research_Collector] 资料查询者
    ↓ 输出《资料汇编》《参考文献》
[Outline_Architect] 大纲创作师
    ↓ 输出《论文大纲》
[Content_Writer] 内容填充者 (逐部分)
    ↓ 输出各章节 MD 文件
[HTML_Formatter] HTML 格式化专家
    ↓ 输出 HTML 文件
浏览器打开 → 全选复制 → 粘贴到 Word
```

---

## 🎭 核心角色

| 角色 | 职责 | 输出 |
|------|------|------|
| **Format_Analyst** | 分析论文格式要求 | 《格式规范》 |
| **Research_Collector** | 查询相关资料 | 《资料汇编》《参考文献》 |
| **Outline_Architect** | 创建论文大纲 | 《论文大纲》 |
| **Content_Writer** | 分部分撰写内容 | 各章节 MD 文件 |
| **HTML_Formatter** | 生成 Word 兼容 HTML | HTML 文件 |

📄 [查看完整角色定义](./roles/README.md)

---

## 📁 项目结构

```
paper-master/
├── README.md                    # 本文件
├── AGENTS.md                    # AI 代理指引
│
├── roles/                       # AI 角色定义
│   ├── Format_Analyst.md
│   ├── Research_Collector.md
│   ├── Outline_Architect.md
│   ├── Content_Writer.md
│   └── HTML_Formatter.md
│
├── templates/                   # 模板库
│   ├── user/                    # 用户自定义模板（放这里）
│   └── html/                    # HTML 输出模板
│
├── docs/                        # 文档
│   ├── workflow_guide.md        # 工作流指南
│   └── html_to_word_guide.md    # HTML 转 Word 指南
│
├── tools/                       # 工具脚本
│   └── project_manager.py       # 项目管理工具
│
├── examples/                    # 示例项目
│
└── projects/                    # 用户项目工作区
```

---

## 📐 模板使用

### 添加自定义模板

将你的论文格式要求（Word/PDF）通过 Mineru 转换为 MD 后，放入：

```
templates/user/你的模板名称.md
```

### 在对话中指定模板

```
用户：我要写论文，使用 templates/user/矿大结课论文格式.md 的格式要求
```

---

## 🛠️ 工具集

| 工具 | 功能 |
|------|------|
| `project_manager.py` | 初始化项目、验证结构 |

### 常用命令

```bash
# 初始化新项目
python tools/project_manager.py init <项目名称>

# 验证项目结构
python tools/project_manager.py validate <项目路径>
```

---

## 📄 HTML 到 Word

为什么使用 HTML 而非直接输出文本？

> Word 和 HTML 的底层富文本结构具有极高通用性。让 AI 生成带样式的 HTML，在浏览器中打开后全选复制，可以**完整保留所有排版样式**直接粘贴到 Word。

详细指南：[HTML 转 Word 指南](./docs/html_to_word_guide.md)

---

## 📖 相关文档

- 📋 [工作流指南](./docs/workflow_guide.md)
- 🎭 [角色定义](./roles/README.md)
- 📄 [HTML 转 Word 指南](./docs/html_to_word_guide.md)

---

## 📜 开源协议

MIT License

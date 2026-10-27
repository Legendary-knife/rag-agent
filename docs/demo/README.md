# 演示视频怎么用

这是给 GitHub README 和面试展示用的录屏。

先看视频：

[![企业 AI Agent 工作台演示](./enterprise-agent-workbench-demo-cover.jpg)](./enterprise-agent-workbench-demo.mp4)

视频里完整演示了四件事：

1. 把一份 Markdown 知识文件导入知识库。
2. 页面自动保存原文件、解析文本，并同步到 GitHub。
3. 点击“一键验证”，系统自动做 RAG 检索和 Agent 运行。
4. 页面展示 RAG 命中文档、Agent 回答和执行 Trace。

## 本地怎么复现

启动后端：

```bash
python3 -m uvicorn backend.app.main:app --port 8010
```

启动前端：

```bash
VITE_API_BASE_URL=http://127.0.0.1:8010/api npm run dev:web -- --host 127.0.0.1 --port 5176 --strictPort
```

打开页面：

```text
http://127.0.0.1:5176/
```

准备一份本地知识文件，例如：

```text
/tmp/enterprise-agent-demo/github-readme-demo-knowledge.md
```

页面里这样操作：

1. 右侧“知识库”区域，粘贴文件绝对路径。
2. 点击“从路径导入”。
3. 中间“业务问题”输入：`客户提交普通工单后多久首次响应？请引用知识库依据，并告诉我下一步该怎么处理。`
4. 点击“一键跑通 / 一键验证”。
5. 看“一键跑通”三步是否都完成。
6. 看“RAG 命中”和“Agent 回答预览”。
7. 看右侧“执行 Trace”。

## 面试时怎么讲

可以这样说：

> 这是一个企业 AI Agent 工作台，不是普通聊天页面。它支持把企业资料导入知识库，后端会解析文件、切 chunk、写入 SQLite 检索库。用户提问后，系统先做 RAG 检索，再把命中的资料交给大模型生成回答，同时保留完整执行 Trace。页面上的“一键跑通”可以直接证明这条链路是真实跑通的，不是写死的展示文案。

重点强调这几个能力：

- 知识库导入：原文件和解析文本都会保存。
- RAG 诊断：回答前能看到命中了哪些资料。
- Agent 执行：输出结论、依据和建议动作。
- Trace 可观测：每一步执行过程都能看到。
- GitHub 同步：知识库文件可随项目同步，方便展示。

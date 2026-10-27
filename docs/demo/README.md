# 演示录屏和操作说明

这份录屏用于 GitHub 项目说明和面试展示：

- 演示视频：[enterprise-agent-workbench-demo.mp4](./enterprise-agent-workbench-demo.mp4)
- 演示资料：`/tmp/enterprise-agent-demo/github-demo-knowledge.md`
- 演示问题：`客户提交工单多久首次响应？请引用知识库依据。`

[![企业 AI Agent 工作台演示](./enterprise-agent-workbench-demo-cover.jpg)](./enterprise-agent-workbench-demo.mp4)

## 本地启动

分别启动后端和前端：

```bash
python3 -m uvicorn backend.app.main:app --port 8010
VITE_API_BASE_URL=http://127.0.0.1:8010/api npm run dev:web -- --host 127.0.0.1 --port 5176 --strictPort
```

打开页面：

```text
http://127.0.0.1:5176/
```

## 演示流程

1. 打开工作台页面。
2. 在右侧知识库区域粘贴本地文件路径，点击“从路径导入”。
3. 确认页面出现“已导入”，并显示本地文件路径和 GitHub 同步状态。
4. 在中间输入业务问题。
5. 点击“一键跑通 / 一键验证”。
6. 查看三步状态：检查知识库、诊断 RAG、运行 Agent。
7. 查看 RAG 命中片段和 Agent 回答预览。
8. 查看右侧执行 Trace，说明系统不是固定话术，而是完整执行链路。

## 面试讲法

这个项目展示的是一个真实可运行的企业 Agent 工作台闭环：

- 文档进入知识库后会保存原文件和解析文本。
- 后端会把文本切成 chunk，并写入本地 SQLite 检索库。
- RAG 诊断台可以在模型回答前确认是否命中文档。
- 一键跑通会自动完成知识库检查、RAG 诊断和 Agent 运行。
- Agent 输出会带依据、建议动作和可观测 Trace。
- 知识库文件会同步到 GitHub，便于展示和复盘。

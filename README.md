# 电信 10000 号私有化信创 AI 语音对话端到端架构方案

一份完整的语音客服 AI 系统架构方案：以中国电信 10000 号场景为载体，覆盖接入层、媒体网关、流式语音管线（ASR → 决策路由 → LLM → TTS）、Agent 工具执行、信创全栈私有化、可观测与合规的端到端设计。

## 文档

- `architecture.md` — 方案全文（Markdown，含 Mermaid 架构图与时序图，GitHub 直接渲染）
- `architecture.html` — 可视化版（自包含单文件，内联 SVG 矢量图，可离线查看 / 打印 / 导出 PDF）

## 技术亮点

1. **容量口径推导**：把"日均千万级 API 调用"的需求口径，用调用量 → DAU → 并发会话 → 请求到达率的容量数学，落成可立项的峰值 QPS 与并发会话口径，并给出千万级 DAU 的水平分片扩容路径
2. **分层时延预算**：TTFS / TTFT / TTFB / E2E 分层 SLA，WebRTC 与 SIP 各一套预算，每跳有 P50/P95/P99 死线
3. **TTS 三引擎拓扑**：Qwen3-TTS 在线主用（97 ms 首包）+ CosyVoice 3.0 方言/离线专线 + MOSS-Nano CPU 兜底，P95 首包超限自动互切；风格控制采用 z-score 结构化控制量而非自然语言指令（可审计、可回归、可 clamp）
4. **决策路由层**：Microsoft-Decision-1 范式的私有化落地（Pre-Router + Post-Guardrail 双闸门），并对 Qwen-Audio-Jev 决策头路线（CHOICE/NOUL/SCORE）做跟踪评估
5. **信创合规**：全栈国产化（昇腾/鲲鹏/达梦/麒麟/统信）、等保、国密、数据不出域的工程设计；Agent 写操作确认回路与幂等设计

## 说明

- 具体容量规模与成本数字涉及商务口径，开源版从略；方法论与推导过程完整保留。
- 文中引用来源共 30 条，均为公开论文、官方仓库与公开报道，见文末「引用来源」。

## License

MIT © 2026 [dabing110](https://github.com/dabing110)（郭向兵）

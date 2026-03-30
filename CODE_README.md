# MiniMind 代码阅读顺序

## 第一阶段：模型结构（核心）

| 顺序 | 文件 | 说明 |
|------|------|------|
| 1 | model/model_minimind.py | **必读** - MiniMind 模型主体结构（Dense + MoE），核心 Transformer 实现 |
| 2 | model/model_lora.py | LoRA 微调实现，了解轻量化微调方法 |
| 3 | model/__init__.py | 模型导出和版本管理 |

## 第二阶段：数据处理

| 顺序 | 文件 | 说明 |
|------|------|------|
| 4 | dataset/lm_dataset.py | **必读** - 数据集加载和预处理，理解训练数据格式 |
| 5 | trainer/train_tokenizer.py | Tokenizer 训练代码（BPE + ByteLevel） |

## 第三阶段：训练流程（按序阅读）

| 顺序 | 文件 | 说明 |
|------|------|------|
| 6 | trainer/train_pretrain.py | **必读** - 预训练，了解语言模型如何学习 |
| 7 | trainer/train_full_sft.py | **必读** - 监督微调（SFT），指令跟随训练 |
| 8 | trainer/train_lora.py | LoRA 训练脚本 |
| 9 | trainer/train_dpo.py | DPO（直接偏好优化）训练 |
| 10 | trainer/train_ppo.py | PPO 强化学习训练 |
| 11 | trainer/train_grpo.py | GRPO/CISPO 等新型 RL 算法 |
| 12 | trainer/train_distillation.py | 模型蒸馏 |
| 13 | trainer/train_agent.py | Agent 强化学习（Tool Use 场景） |
| 14 | trainer/rollout_engine.py | Rollout 引擎解耦，支持多种生成后端 |
| 15 | trainer/trainer_utils.py | 训练工具函数 |

## 第四阶段：推理与部署

| 顺序 | 文件 | 说明 |
|------|------|------|
| 16 | eval_llm.py | **必读** - 模型推理入口 |
| 17 | scripts/chat_api.py | Chat 推理示例 |
| 18 | scripts/serve_openai_api.py | OpenAI API 兼容服务端 |
| 19 | scripts/web_demo.py | Streamlit WebUI |
| 20 | scripts/convert_model.py | LoRA 权重合并导出 |

## 推荐学习流程

```
1. model_minimind.py        → 理解 MiniMind 模型架构
2. lm_dataset.py            → 理解数据格式和处理
3. train_pretrain.py        → 掌握预训练流程
4. train_full_sft.py        → 掌握 SFT 监督微调
5. eval_llm.py              → 学会推理使用模型
```

**后续深入**（按需选择）：
- 想学 LoRA → model_lora.py + train_lora.py
- 想学强化学习 → train_ppo.py / train_grpo.py / train_dpo.py
- 想学 Agent → train_agent.py + rollout_engine.py
- 想部署 → scripts/serve_openai_api.py

## 目录结构概览

```
minimind/
├── model/                    # 模型结构（Dense + MoE + LoRA）
│   ├── model_minimind.py   # 核心 Transformer 实现
│   └── model_lora.py       # LoRA 实现
├── dataset/                  # 数据集处理
│   └── lm_dataset.py       # 数据加载
├── trainer/                  # 训练脚本集合
│   ├── train_pretrain.py   # 预训练
│   ├── train_full_sft.py    # 全参数 SFT
│   ├── train_lora.py       # LoRA 微调
│   ├── train_dpo.py        # DPO 偏好优化
│   ├── train_ppo.py        # PPO 强化学习
│   ├── train_grpo.py       # GRPO/CISPO
│   ├── train_agent.py      # Agent RL
│   ├── train_distillation.py # 模型蒸馏
│   └── rollout_engine.py    # Rollout 生成引擎
├── scripts/                  # 推理和部署脚本
│   ├── serve_openai_api.py # OpenAI API 服务
│   └── web_demo.py         # WebUI
├── eval_llm.py              # 推理入口
└── dataset/                  # 训练数据目录
```

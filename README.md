# AI Engineering Handbook

A structured set of notes and reference docs for building modern ML/AI systems — from fundamentals (math, Python, ML/DL) to production topics (LLMs, RAG, agentic workflows, and deployment).

## Contents

| Folder                | File                                              | Content Covered                                                                                                                       |
| --------------------- | ------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------- |
| `00-maths-statistics` | `1. Linear Algebra 2. Probability and Statistics` | Notes and reference material.                                                                                                         |
| `00-maths-statistics` | `00-maths-statistics/probability/probability.md`  | Notes and reference material.                                                                                                         |
| `00-maths-statistics` | `00-maths-statistics/statistics/statistics.md`    | Notes and reference material.                                                                                                         |
| `01-python`           | `01-python/python.ipynb`                          | Hands-on notebook: python.                                                                                                            |
| `02-machine-learning` | `02-machine-learning/machine-learning.md`         | What Is Machine Learning?; Applications of Machine Learning; Types of Machine Learning Systems                                        |
| `02-machine-learning` | `02-machine-learning/quantization.md`             | Quantization; Post‐Training Quantization (PTQ); Quantization‐Aware Training (QAT)                                                     |
| `03-deep-learning`    | `03-deep-learning/deep-learning.md`               | Notes and reference material.                                                                                                         |
| `03-deep-learning`    | `03-deep-learning/optimisers.md`                  | AdamW (Adam with Weight Decay); Decoupled Weight Decay                                                                                |
| `04-computer-vision`  | `04-computer-vision/computer-vision.md`           | Computer vision tasks; Image processing; Image transformation                                                                         |
| `04-computer-vision`  | `04-computer-vision/image_segmentation.md`        | Image segmentation; Segment Anything Model (SAM); SAM 2 (Segment Anything Model 2)                                                    |
| `04-computer-vision`  | `04-computer-vision/keypoints_detection.md`       | Notes and reference material.                                                                                                         |
| `04-computer-vision`  | `04-computer-vision/object_detection.md`          | YOLO (You Only Look Once); YOLOv3 (You Only Look Once version 3); Object tracking                                                     |
| `05-nlp`              | `05-nlp/nlp.ipynb`                                | Hands-on notebook: nlp.                                                                                                               |
| `05-nlp`              | `05-nlp/nlp.md`                                   | NLP applications; End to end NLP pipeline; NLP preprocessing                                                                          |
| `06-llms`             | `06-llms/evaluation.md`                           | Notes and reference material.                                                                                                         |
| `06-llms`             | `06-llms/fine-tuning.md`                          | Parameter-efficient fine-tuning (PEFT); LoRA and QLoRA                                                                                |
| `06-llms`             | `06-llms/llm_inference_optmization.md`            | KV Cache (Key-Value Cache); Multi-Query Attention; Grouped-Query Attention                                                            |
| `06-llms`             | `06-llms/llms.md`                                 | How do LLM work ?; Significance of pre-training and fine-tuning; Embeddings                                                           |
| `06-llms`             | `06-llms/prompt_engineering.md`                   | Advanced prompt engineering; Complexity of a Prompt; In-Context Learning (ICL)                                                        |
| `06-llms`             | `06-llms/transformers.md`                         | Attention mechanisms in Transformer models; Positional encodings; BERT (Bidirectional Encoder Representations from Transformers)      |
| `06-llms`             | `06-llms/vlm.md`                                  | CLIP (Contrastive Language-Image Pre-training); Swin Transformer; Masked Autoencoders (MAE)                                           |
| `07-diffusion-model`  | `07-diffusion-model/diffusion_models.md`          | Mathematical intution; Variance Schedule; what are the assumptions                                                                    |
| `08-rag`              | `08-rag/rag.md`                                   | Different types of Retriever; Core Retrieval Strategies; Advanced Document Retrievers                                                 |
| `08-rag`              | `08-rag/RAG_system.ipynb`                         | Hands-on notebook: RAG system.                                                                                                        |
| `09-agentic-ai`       | `09-agentic-ai/agentic-ai.md`                     | Prompt chaining; Routing; Parallelization                                                                                             |
| `09-agentic-ai`       | `09-agentic-ai/langchain.md`                      | What are MultiQueryRetriever and MultiVectorRetriever; What are Self-querying and TimeWeightedVectorStoreRetriever?; LangChain Memory |
| `10-rl`               | `10-rl/rl.md`                                     | Notes and reference material.                                                                                                         |
| `11-deployment`       | `11-deployment/API_development/fastapi.md`        | Routing and Request Handling; Routing in FastAPI; Request Handling in FastAPI                                                         |

## How to Use This Repo

- Browse the Markdown files directly in your editor (VS Code works great).
- Use the numbered folders as a rough learning path (fundamentals → advanced → production).
- Open the notebooks (`.ipynb`) for hands-on explorations where available.

## Notes

- This repo is primarily a **living handbook**: sections may be expanded, reorganized, or rewritten over time.
- If you spot mistakes or want to add content, feel free to open a PR.

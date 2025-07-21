# N8N ViralFlow
A fully automated n8n-based pipeline that transforms user input into short, scroll‑stopping videos with hooks, dynamic visuals, and dramatic TTS narration and autmatically uploads it on their Youtube.

![image alt](https://github.com/PrabhanshuKamal2121/N8N-ViralFlow/blob/ac874b4bda948819321a8e0c4e5a8f531ca54a8a/N8N%20ViralFlow.png)

---
## 🛠️ Tech Stack

[![n8n](https://img.shields.io/badge/n8n-FF3E00?style=for-the-badge&logo=n8n&logoColor=white)](https://n8n.io)  
[![Ollama](https://img.shields.io/badge/Ollama-000000?style=for-the-badge&logo=owl&logoColor=white)](https://ollama.ai)  
[![SearxNG](https://img.shields.io/badge/SearxNG-3F51B5?style=for-the-badge&logo=searx&logoColor=white)](https://searxng.github.io/searxng/)  
[![MinIO](https://img.shields.io/badge/MinIO-29B6F6?style=for-the-badge&logo=minio&logoColor=white)](https://min.io)  
[![Docker](https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white)](https://docker.com)  
[![Chatterbox TTS](https://img.shields.io/badge/Chatterbox%20TTS-FF4081?style=for-the-badge)](https://github.com/your-org/chatterbox-tts-server)  
[![Together.ai](https://img.shields.io/badge/Together.ai-FF6C37?style=for-the-badge&logo=together&logoColor=white)](https://together.ai/)  
[![AWS S3](https://img.shields.io/badge/AWS_S3-569A31?style=for-the-badge&logo=amazonaws&logoColor=white)](https://aws.amazon.com/s3)

---

## Example Youtube Channel
[![Example Youtube Channel](https://img.shields.io/badge/YouTube-FF0000?style=for-the-badge&logo=youtube&logoColor=white)](https://www.youtube.com/@PrabhanshuIndianHistory/shorts)

---
## 🎯 Table of Contents

- [📝 Summary](#-summary)  
- [✨ Features](#-features)  
- [🛠️ Tech Stack](#️-tech-stack)  
- [📋 Workflow Overview](#-workflow-overview)  
- [🔧 n8n Nodes & AI Models](#-n8n-nodes--ai-models)  
- [🚀 Quick Start](#-quick-start)  
- [📫 Contact](#-contact)

---

## 📝 Summary

Users fill out a stylized “Brain Rotter” form with:
1. **Topic** (e.g. Indian history)  
2. **Duration** (30s / 1min / 2min)  
3. **Generative Style** (e.g. Disney Pixar)

The workflow then:
- **Generates 20 facts** via web search  
- **Writes a punchy script** (“What if…?” hook, reveals, mic‑drop)  
- **Converts text→speech**, splits into segments  
- **Creates scene prompts**, generates images via Together.ai  
- **Transforms images→video clips**, concatenates, captions, adds music  
- **Uploads final Short to YouTube** with metadata & hashtags  

---

## ✨ Features

- **End‑to‑End Automation**: From form input to published YouTube Short  
- **AI‑Powered Content**: Facts generation, scriptwriting, image prompts  
- **Cinematic Visuals**: Realistic/dark‑themed images in user‑chosen style  
- **Dynamic Audio**: TTS narration + background music + word‑by‑word captions  
- **Short‑Form Focus**: Maximum 59 s, mobile‑friendly, platform‑optimized  

---

## 🛠️ Tech Stack

| Category            | Tools & Services                                      |
|---------------------|-------------------------------------------------------|
| **Orchestration**   | n8n (automation)                                      |
| **AI & LLMs**       | Ollama (deepseek‑r1:8b, mistral:7b, llama3.1:latest)  |
| **Image Gen**       | Together.ai (FLUX.1‑schnell)                          |
| **TTS**             | chatterbox‑tts‑server (HTTP POST `/tts`)              |
| **Transcription**   | nca‑toolkit (HTTP `/v1/media/transcribe`)             |
| **Video Processing**| nca‑toolkit (concatenate, ffmpeg compose, captioning) |
| **Storage**         | MinIO / AWS S3                                        |
| **Deployment**      | Docker, n8n Cloud / Self‑hosted                       |

---

## 📋 Workflow Overview

1. **Form Input Collection**  
   • `formTrigger`: Collects Topic, Duration, Style with custom CSS.  
2. **Facts Generation**  
   • `langchain.agent` (deepseek‑r1:8b): Fetches 20 trending, controversial facts.  
3. **Script Writing**  
   • `langchain.agent` (mistral:7b): Builds “SUPREME INDIANS” script with hook, reveals, pride, mic‑drop.  
4. **Script Cleanup**  
   • `code`: Strips formatting, newlines, asterisks.  
5. **Text‑to‑Speech**  
   • `httpRequest` → `chatterbox‑tts‑server` → returns WAV + timestamps.  
6. **Transcription & Segmentation**  
   - Transcribe audio → JSON/SRT.  
   - Split into ≤2 s scenes (`Split into N's Scenes`, `Fixer2`).  
7. **Image Prompting**  
   • `chainLlm` (llama3.1): Generates cinematic prompts per segment.  
8. **Image Generation**  
   • `httpRequest` → Together.ai API → base64 PNG → convert & upload to S3.  
9. **Clip Creation & Assembly**  
   - `httpRequest` → transform image→video clip  
   - `combine` → concatenate all clips  
10. **Enhancements**  
    - Captioning (word‑by‑word)  
    - Background music layering (FFmpeg compose)  
    - Trim to 59 s  
11. **YouTube Upload**  
    • `youTube` node: Publishes as a public Short with title, description, tags.  

---

## 🔧 n8n Nodes & AI Models

- **n8n-nodes-base.formTrigger** – Custom CSS form  
- **@n8n/n8n-nodes-langchain.agent** – deepseek‑r1:8b & mistral:7b  
- **@n8n/n8n-nodes-langchain.chainLlm** – llama3.1 for image prompts  
- **n8n-nodes-base.httpRequest** – TTS, transcription, image & video services  
- **n8n-nodes-base.code** – JS for cleaning, splitting, merging, random zoom speeds  
- **n8n-nodes-base.s3** – MinIO/AWS S3 uploads  
- **n8n-nodes-base.aggregate / merge / splitInBatches** – Data orchestration  
- **n8n-nodes-base.youTube** – YouTube Shorts publishing  

---

## 🚀 Quick Start

Learn how to install and get started with each component:

- **n8n Self Hosted AI** – A Must Try GitHub Open Source Project!  
  https://youtu.be/OCet5rGwEeI?si=sOSSSR8-QbAhUqsM

- **Chatterbox TTS Server** – Setup & Demo  
  https://youtu.be/VEEn6h2aRR0?si=c-8Lo1YG-iJAw5G8

- **SearchXng** – Installation & Configuration  
  https://youtu.be/O5b9FvHYjqc?si=MOKRk68Gm12IzS8M

- **Workflow Inspiration** – Automated Content Pipeline Overview  
  https://youtu.be/sOylPpFyQ8A?si=EfouFqOt1n0UZgqO

- **Ngrok** – Host N8N for free  
  https://youtu.be/RvAD2__YYjg?si=3_6tqVncQ0e5yqwL
---

## 📫 Contact
- **Made by Prabhanshu Kamal**
- **GitHub: PrabhanshuKamal2121**
- **LinkedIn: PrabhanshuK**

---

## ⚖️ Disclaimer
- **This pipeline is for educational/demo purposes. It uses publicly available AI models and services. Results may vary; always validate before publishing.**




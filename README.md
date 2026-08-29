## Muhammad Danial Maqbool

**MS Artificial Intelligence at LUMS** (GPA 3.85/4.0) · Lahore, Pakistan

I build computer-vision and backend systems, mostly around healthcare data. I
came into AI from mechanical engineering, which is where I picked up the habit
that runs through everything below: the interesting part of a system is usually
the failure mode nobody specified.

The thing I care most about is **whether a result is real** — calibration,
leakage, evaluation design, and the distance between a metric that looks good
and a decision that holds up.

---

## Larger projects

These are private or unreleased repositories, described here rather than linked.

### FHIR-compliant EHR system — primary portfolio project
`FastAPI` `PostgreSQL` `Docker` `React` `TypeScript` `AWS Bedrock` `FHIR`

A full-stack electronic health record system built independently and genuinely
containerised. Clinical data passes a **two-layer validation gate** — a
business-rules layer plus a formal FHIR validator — and anything that fails
triggers automatic repair and re-validation before a write reaches the database.
Every write emits a permanent audit-trail entry.

Claude via **AWS Bedrock** handles in-app clinical text features (the
compliance-appropriate path for healthcare). Speech-to-text runs
**faster-whisper on-device rather than through a cloud API**, a deliberate
patient-privacy decision rather than a performance one.

200+ commits, with pytest, mypy strict, Vitest, Playwright E2E and ruff.

### Diabetic retinopathy grading — knowledge distillation
`PyTorch` `EfficientNet` `CBAM` `GradCAM++` `Ordinal regression`

Distilled an **EfficientNet-B4 teacher (QWK 0.91)** into a custom 5.3M-parameter
**EfficientNet-B0 student** with multi-scale CBAM attention and a monotonic
ordinal-regression head, reaching **QWK 0.88** after 8-view test-time
augmentation and coordinate-ascent threshold search. APTOS 2019, 3,662 fundus
images across five ICDR grades with heavy class imbalance.

Interpretability was validated rather than asserted: **GradCAM++ activations
cross-checked against IDRiD lesion masks by IoU**. An earlier iteration that
tried supervising attention directly on those masks underperformed and was
dropped — the negative result is in the write-up.

Trained end to end on a single 8GB laptop GPU. Written up in ICML-style
two-column format with an explicit AI-usage disclosure.

### Full-body AI character replacement — privacy-preserving video
`SAM2` `ViTPose` `Wan 2.2 Animate 14B` `ComfyUI` `RunPod`

Extends LUMS **SITARA** research (PerCom 2026), which demonstrated face blurring
and basic synthetic replacement on a Raspberry Pi, toward **full-body character
replacement with consent-based identity recovery**. A five-stage ComfyUI
pipeline: detect and canonicalize, extract, remove the person and fill the
background (temporal median plus Telea inpainting), generate the character, then
composite. Includes an identity-free expression canonicaliser extracting 12
affect scalars, so expression transfers without identity following it.

*This is my own project extending that research, not the SITARA paper itself.*

### Autonomous navigation — TurtleBot3 / BARN Challenge
`ROS 2` `LiDAR` `OpenCV` `Gazebo`

Navigation across 50 randomised obstacle worlds using a four-state machine:
LiDAR pivot → camera and PID path following → reverse recovery → artificial
potential field evasion. The useful part was the debugging — diagnosing a
saturated occupancy grid that was causing constant left-turn drift, removing
that module, and adding a three-tier forward-motion safety gate verified against
live telemetry.

### 3D Gaussian Splatting — local pipeline
`Inria 3DGS` `COLMAP` `CUDA`

The full video → structure-from-motion → training → viewer pipeline running
locally on 8GB of VRAM. Mostly a toolchain fight: CUDA 11.8's `nvcc` rejects
MSVC ≥ 14.40 when building the rasteriser, fixed by pinning the v14.39 toolset
and scripting a reproducible environment activation.

### Multi-tenant RAG chatbot service — commercial
`Next.js` `Supabase/pgvector` `Groq Llama 3.3 70B` `Stripe`

A production service for paying clients: a one-line embeddable widget resolves
the tenant, loads per-client persona and knowledge boundaries, retrieves over
pgvector, and returns grounded answers. Ingestion, chunking, embedding, billing,
trial gating and a lead-capture dashboard included. Per-client knowledge
boundaries are enforced so the assistant refuses out-of-scope questions rather
than improvising.

---

## Background

**MS Artificial Intelligence**, LUMS SBASSE · 2025–present · GPA 3.85/4.0
Deep Learning · Generative AI (transformers, tokenization, LoRA/PEFT, RLHF, DPO)
· AI for Robotics

**B.E. Mechanical Engineering**, NUST · 2019–2023

**Mechanical Design Engineer**, Mekex Innovation Srl — Italy, remote ·
Jul 2023 – Jul 2025
Delivered 8+ industrial projects as primary technical contact for an
international client. Built Python automation for engineering workflows and led
junior engineers on design execution.

**Freelance**, ongoing · Five years on Fiverr with **228+ reviewed
engagements**, now focused on Python backends, web scraping and FHIR/HL7
integration work.

**Certifications** · Machine Learning Specialization (Andrew Ng, Stanford /
Coursera) · Python Data Analysis for Healthcare (LinkedIn Learning)

---

## Tools

**Languages** Python · C++ · TypeScript · SQL · Bash

**ML/CV** PyTorch · scikit-learn · OpenCV · CNNs · knowledge distillation ·
CBAM attention · GradCAM++ · ordinal regression · SAM2 · ViTPose

**LLM** Anthropic Claude · AWS Bedrock · OpenAI · Groq · RAG · pgvector ·
prompt and persona design

**Backend** FastAPI · PostgreSQL · Docker · REST · FHIR/HL7 v2 · audit logging

**Testing** pytest · mypy strict · Vitest · Playwright · ruff

**Robotics/3D** ROS 2 · Gazebo · LiDAR · PID · 3D Gaussian Splatting · COLMAP

---

## Where this is going

Looking for an MS thesis in **3D reconstruction and neural rendering**, with a
long-term interest in XR — 3D Gaussian Splatting and world models are the
concrete route in. The mechanical-engineering background is genuinely useful
here: geometry, camera models and calibration were the day job before they were
the research interest.

---

## A note on what is here

My public repositories are deliberately small and deliberately honest. Where a
result did not hold up, the README says so:

- `vecsearch` reports that its IVF was **slower than a flat scan** before the
  optimisation, and that at 50k vectors a flat scan is a perfectly reasonable
  production choice.
- `rag-eval` reports a **negative result**: BM25's defaults were already optimal
  on that corpus, and at k=5 the metric saturated so hard no retriever could be
  told from another.
- `schema-guard` states that its coercion layer is **partly redundant** with
  Pydantic's lax mode, and that its real contribution is the audit trail.
- The DR grading write-up keeps the attention-supervision experiment that
  **failed**, rather than reporting only the version that worked.

I would rather ship a result with its limitations attached than one that only
survives if nobody checks.

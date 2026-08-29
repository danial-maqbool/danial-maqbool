## Muhammad Danial Maqbool

**MS Artificial Intelligence at LUMS**, Lahore, Pakistan

I build computer vision and backend systems, mostly for healthcare data. I
studied mechanical engineering first and moved into AI after that, which is
probably why I tend to think about what breaks before I think about what works.

Most of what I do comes back to one question: is the result actually real. That
means calibration, checking for leakage, and watching the gap between a metric
that looks good and a decision you would trust.

---

## Projects

Some of these are public and pinned above. The rest are private or unreleased,
so they are described here rather than linked.

### FHIR compliant EHR system
`FastAPI` `PostgreSQL` `Docker` `React` `TypeScript` `AWS Bedrock` `FHIR`

A full stack electronic health record system I built on my own, and the one
project here that is properly containerised. Clinical data passes two layers of
validation, a business rules layer and then a formal FHIR validator. Anything
that fails gets repaired and re validated before it reaches the database, and
every write leaves a permanent audit entry.

Claude runs through AWS Bedrock for the in app clinical text features, since
that is the compliance friendly path for healthcare. Speech to text runs locally
with faster-whisper instead of going out to a cloud API. That was a privacy
decision rather than a performance one.

Around 200 commits, with pytest, mypy in strict mode, Vitest, Playwright and
ruff.

### [Diabetic retinopathy grading](https://github.com/danial-maqbool/Diabetic-Retinopathy-Stage-Detection-NN-Model)
`PyTorch` `EfficientNet` `CBAM` `GradCAM++` `Ordinal regression`

I distilled an EfficientNet-B4 teacher at QWK 0.91 into a 5.3M parameter
EfficientNet-B0 student with multi scale CBAM attention and a monotonic ordinal
regression head. The student reached QWK 0.88 after eight view test time
augmentation and a coordinate ascent threshold search. Trained on APTOS 2019,
3,662 fundus images across five severity grades with heavy class imbalance.

For interpretability I did not want to just show a heatmap and call it
explainable, so I cross checked the GradCAM++ activations against IDRiD lesion
masks by IoU. An earlier version tried supervising attention directly on those
masks and it underperformed, so I dropped it. That failed attempt is still in
the write up.

The whole thing trained on a single 8GB laptop GPU. Written up in ICML style two
column format with an AI usage disclosure.

### Full body AI character replacement
`SAM2` `ViTPose` `Wan 2.2 Animate 14B` `ComfyUI` `RunPod`

This extends SITARA, a LUMS research project from PerCom 2026 that did face
blurring and basic synthetic replacement on a Raspberry Pi. I am taking it
toward full body character replacement with consent based identity recovery.

It runs as a five stage ComfyUI pipeline: detect and canonicalize, extract the
person, remove them and fill the background with temporal median plus Telea
inpainting, generate the character, then composite. There is also an identity
free expression canonicaliser that pulls out 12 affect scalars, so expression
carries over without identity following it.

To be clear, this is my own project building on that research, not the SITARA
paper itself.

### Autonomous navigation, TurtleBot3 and the BARN Challenge
`ROS 2` `LiDAR` `OpenCV` `Gazebo`

Navigation across 50 randomised obstacle worlds, using a four state machine:
LiDAR pivot, then camera and PID path following, then reverse recovery, then
artificial potential field evasion.

The interesting part was the debugging. The robot kept drifting left and I
eventually traced it to a saturated occupancy grid, so I removed that module
entirely. After that I added a three tier forward motion safety gate and checked
it against live telemetry.

### 3D Gaussian Splatting
`Inria 3DGS` `COLMAP` `CUDA`

The full pipeline from video to structure from motion to training to viewer,
running locally on 8GB of VRAM. Honestly this was mostly a toolchain fight. CUDA
11.8 rejects MSVC 14.40 and above when building the rasteriser, so I pinned the
v14.39 toolset and scripted the environment setup so I would not have to work it
out twice.

### [PaperBoxd](https://github.com/danial-maqbool/PaperBoxd)
`Next.js` `Prisma` `TypeScript` `Vercel`

A reading log for research papers. You can discover work, log what you have
read, rate and review it, and follow what other researchers are reading. It
pulls from OpenAlex, Crossref, arXiv and Semantic Scholar and reconciles them
into one record, which is most of the actual work, since the same paper shows
up differently in each. Deployed and usable.

### Multi tenant RAG chatbot service
`Next.js` `Supabase/pgvector` `Groq Llama 3.3 70B` `Stripe`

A commercial service I run for paying clients. One line of embed code resolves
the tenant, loads that client's persona and knowledge boundaries, retrieves over
pgvector and returns a grounded answer. I built the ingestion side too, along
with billing, trial gating and a lead capture dashboard.

Each client gets their own knowledge boundaries, so the assistant says it does
not know rather than making something up.

---

## Background

**MS Artificial Intelligence**, LUMS SBASSE, 2025 to present
Coursework in deep learning, generative AI (transformers, tokenization,
LoRA/PEFT, RLHF, DPO) and AI for robotics.

**B.E. Mechanical Engineering**, NUST, 2019 to 2023

**Mechanical Design Engineer**, Mekex Innovation Srl, Italy, remote,
July 2023 to July 2025
Delivered 8+ industrial projects as the main technical contact for an
international client. Wrote Python automation for engineering workflows and led
junior engineers on design execution.

**Certifications**
Machine Learning Specialization (Andrew Ng, Stanford and Coursera), Python Data
Analysis for Healthcare (LinkedIn Learning)

---

## Tools

**Languages** Python, C++, TypeScript, SQL, Bash

**ML and CV** PyTorch, scikit-learn, OpenCV, CNNs, knowledge distillation, CBAM
attention, GradCAM++, ordinal regression, SAM2, ViTPose

**LLM** Anthropic Claude, AWS Bedrock, OpenAI, Groq, RAG, pgvector, prompt and
persona design

**Backend** FastAPI, PostgreSQL, Docker, REST, FHIR and HL7 v2, audit logging

**Testing** pytest, mypy strict, Vitest, Playwright, ruff

**Robotics and 3D** ROS 2, Gazebo, LiDAR, PID, 3D Gaussian Splatting, COLMAP

---

## What I am working toward

I am looking for an MS thesis in 3D reconstruction and neural rendering, with XR
as the longer term interest. Gaussian splatting and world models feel like the
practical way in.

The mechanical engineering background turns out to help more than I expected
here. Geometry, camera models and calibration were the day job long before they
were the research interest.

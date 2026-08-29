## Danial Maqbool

MS Artificial Intelligence at LUMS (GPA 3.85/4.0). Previously a mechanical
design engineer, which is where I learned that the interesting part of a system
is usually the failure mode nobody specified.

I build Python backends and ML systems, mostly around healthcare data. What I
care about, and what these repos are mostly about, is **whether a result is
real** — calibration, leakage, evaluation design, and the gap between a metric
that looks good and a decision that holds up.

---

### Public repositories

Each one runs on CPU with no API keys and regenerates its own results with
`python run.py`. Every number in every README came from actually running the
code, not from a paper.

**[calibrated-risk](https://github.com/danial-maqbool/calibrated-risk)** —
calibration, cost-sensitive thresholds and leakage detection
> Global calibration error of 0.006 looked excellent, but inside the narrow
> probability band where the decision actually gets made it was **0.076 — 13×
> worse**, estimated from 87 of 569 samples. That is why the textbook
> cost-optimal threshold costs more here than the empirical one. Also: fitting
> feature selection before the split manufactured **0.22 AUC out of pure
> noise**.

**[vecsearch](https://github.com/danial-maqbool/vecsearch)** —
IVF and product quantization in NumPy, validated against faiss
> Product quantization scored recall@10 of 0.23, which looks broken. Its
> **score ratio was 0.91** — the neighbours it returned were within 9% of
> optimal, for a 32× smaller index. Judging it on recall alone leads to the
> wrong decision. Restructuring the search loop from per-query to per-partition
> gave a **4× speedup with bit-identical output**.

**[rag-eval](https://github.com/danial-maqbool/rag-eval)** —
a retrieval evaluation harness
> Fixed-size chunking without overlap made **3–5 of 27 questions
> unanswerable** — not badly ranked, impossible, because the answer span was cut
> across a boundary. Everyone says "use overlap"; this counts the cost of not
> doing it. Ranking metrics and BM25 are written out rather than imported, so
> the definitions are inspectable.

**[schema-guard](https://github.com/danial-maqbool/schema-guard)** —
deterministic repair and validation for LLM structured output
> **8% of malformed model responses parse as-is; 96% after the repair ladder.**
> Structure gets repaired, meaning never does: `"5.1"` becomes `5.1`, `"five
> point one"` is rejected, and a missing required field is never filled with a
> default.

**103 tests across the four, CI on Python 3.10–3.12.**

---

### Currently building

A **FHIR-compliant EHR platform** — FastAPI, PostgreSQL and Docker, with a
two-layer validation gate (business rules plus a formal FHIR validator) where
failed records are repaired and re-validated before any write, and every write
leaves a permanent audit entry. 200+ commits, pytest, mypy strict, Playwright.

---

### Working with

`Python` · `FastAPI` · `PostgreSQL` · `Docker` · `PyTorch` · `scikit-learn` ·
`NumPy` · `Pydantic` · `pytest` · `FHIR / HL7 v2` · `RAG & vector search`

---

### A note on what is here

The repos are deliberately small and deliberately honest. Where a result did
not hold up, the README says so:

- `vecsearch` reports that this IVF is **slower than a flat scan** past a few
  probes before the optimisation, and that at 50k vectors a flat scan is a
  perfectly reasonable production choice.
- `rag-eval` reports a **negative result**: BM25's defaults were already optimal
  on that corpus, and at k=5 the metric saturated so hard that no retriever
  could be distinguished from another.
- `schema-guard` states that its coercion layer is **partly redundant** with
  Pydantic's lax mode, and that its real contribution is the audit trail.

I would rather ship a result with its limitations attached than one that only
survives if nobody checks.

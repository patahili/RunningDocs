# Windows AI Benchmarking Strategy White Paper

## 1. Organizational, Product, and Market Goals to Consider

### Windows Org Goals

Position Windows as the premier platform for AI development and deployment, with measurable leadership over Apple and other competitors in NPU benchmarks. [AI_Benchma...ate_080125], [AI Benchma...lling Deck]

Drive platform adoption and ecosystem momentum by winning key benchmarks and shaping the narrative for enterprise and developer purchase decisions. [AI_Benchma...ate_080125], [AI Benchma...lling Deck]

Empower every developer and customer to achieve more—with AI that performs best on Windows. [AI_Benchma...ate_080125]

### WinML Product Objectives

Achieve ≥95% parity with native execution for WinML stack across all major IHVs. [AI_Benchma...ate_080125], [AI Benchma...lling Deck]

Ensure WinML is the default NPU execution path in key benchmarks (e.g., Procyon AI CV 2.0). [AI_Benchma...ate_080125], [AI Benchma...lling Deck]

Influence future benchmark revisions to reflect real-world developer needs and Windows strengths. [AI_Benchma...ate_080125]

### Market Goals

Beat Apple M4 scores by ≥5% on direct comparison benchmarks for in-market SoCs. [AI_Benchma...ate_080125], [AI_Benchma...lling Deck]

Expand benchmarking to additional device tiers (low-cost, Chromebook) and coprocessors (GPU, CPU) as needed. [AI_Benchma...ate_080125]

Establish transparent, repeatable benchmarks that validate Windows as the trusted, relevant, and future-ready AI platform. [AI_Benchma...ate_080125]

---

## 2. Benchmarking Approaches & Metrics Most Impactful for WinML/Windows

### Key Benchmarks

**Geekbench AI**: Primary comparison point vs Apple; focus on small computer vision models and Windows Studio Effects. [AI_Benchma...ate_080125], [AI_Benchma...lling Deck]

**Procyon AI Computer Vision**: Direct NPU comparison; includes Relight, SuperRes, and other scenarios. [AI_Benchma...ate_080125], [AI_Benchma...lling Deck]

**MLPerf Client**: Cross-platform, generative AI; planned Apple NPU support; includes SLMs like Llama 3.1 and Phi 3.5. [AI_Benchma...ate_080125], [AI_Benchma...lling Deck]

### Metrics

**Performance (TOPS, pTOPS, tokens/sec, image/sec)**: Directly compare against Apple and other competitors. [AI_Benchma...ate_080125], [AI_Benchma...lling Deck]

**Parity to Native**: WinML stack should achieve ≥95% of native performance. [AI_Benchma...ate_080125], [AI_Benchma...lling Deck]

**Breadth of Coverage**: All IHVs submit scores, regardless of quality, to showcase platform breadth. [AI_Benchma...lling Deck]

**Repeatability & Transparency**: Benchmarks must be transparent, repeatable, and reflect real-world developer scenarios. [AI_Benchma...ate_080125]

### Approaches

Prioritize NPU benchmarks for Ignite and FY26 H1; expand to GPU/CPU as needed. [AI_Benchma...ate_080125], [AI_Benchma...lling Deck]

Use Olive as the unified quantization toolchain, but allow IHV native toolchains for best performance. [AI_Benchma...2025-08-13], [AI_Benchma...lling Deck]

Track MLPerf topics and ensure Microsoft controls the WinML submission process. [AI_Benchma...2025-08-13], [AI_Benchma...lling Deck]

---

## 3. How Benchmarking Reinforces WinML's Value Proposition

### Leadership Messaging

**"Win the Benchmarks, Win the Market"**: Benchmark wins drive platform adoption and ecosystem momentum. [AI_Benchma...ate_080125], [AI_Benchma...lling Deck]

Transparent, repeatable benchmarks validate Windows as the premier AI development platform. [AI_Benchma...ate_080125]

Benchmarks shape the story customers believe, influencing enterprise and developer purchase decisions. [AI_Benchma...ate_080125], [AI_Benchma...lling Deck]

### Partner & IHV Engagement

IHVs are incentivized to improve scores and adopt WinML as the default path. [AI_Benchma...ate_080125], [AI_Benchma...lling Deck]

**Breadth play**: All IHVs show their best work, driving buy-in and platform credibility. [AI_Benchma...lling Deck]

Microsoft's control of WinML submissions ensures consistent messaging and platform positioning. [AI_Benchma...2025-08-13], [AI_Benchma...lling Deck]

---

## 4. Potential Milestones or Phases for the Next 12 Months

### Short-Term (Q3–Q4 2025)

**Ignite showcase**: Launch Procyon AI CV 2.0 with WinML as default NPU execution path. [AI_Benchma...ate_080125], [AI_Benchma...lling Deck]

Complete feasibility study for enabling 5 new models across Olive, WinML, and IHV stacks. [AI_Benchma...ate_080125], [AI_Benchma...lling Deck]

**Geekbench AI 1.5 release (Sept), Procyon AI CV 2.0 release (Oct), WinML GA (Sept)**. [AI_Benchma...lling Deck]

### Medium-Term (Q1–Q2 2026)

Expand NPU execution (WinML & native) in all benchmarks. [AI_Benchma...ate_080125], [AI_Benchma...lling Deck]

Establish benchmark compete across additional device tiers (low cost, Chromebook). [AI_Benchma...ate_080125]

Influence model representation in future benchmark revisions. [AI_Benchma...ate_080125]

### Long-Term (Q3–Q4 2026)

Expand focus to GPUs and other coprocessors as needed. [AI_Benchma...ate_080125]

Continuously evolve benchmarks to showcase Windows leadership across emerging models, tools, and versions. [AI_Benchma...ate_080125]

---

## 5. Internal Data, Meetings, or Planning Artifacts to Reference

### Artifacts

**AI Benchmarks Rolling Deck**: P0 plan for Ignite, WinML stack enablement, benchmark score targets, resource planning. [AI_Benchma...lling Deck]

**AI_Benchmarking_WiSiProgramUpdate_080125**: Benchmark landscape, execution paths, strategic goals, feasibility mapping. [AI_Benchma...ate_080125]

**AI Benchmarking Weekly Sync 2025-08-13**: Decisions and open questions around quantization, MLPerf, IHV engagement, and toolchain strategy. [AI_Benchma...2025-08-13]

### Meetings

Weekly benchmarking syncs (track MLPerf, quantization, IHV engagement). [AI_Benchma...2025-08-13]

IHV engagement meetings (Intel, QC, AMD, NV). [AI_Benchma...lling Deck], [AI_Benchma...ate_080125]

Ignite planning and feasibility study sessions. [AI_Benchma...ate_080125], [AI_Benchma...lling Deck]

### Data Sources

Benchmark scores and release timelines (Geekbench AI, Procyon AI CV, MLPerf). [AI_Benchma...lling Deck], [AI_Benchma...ate_080125]

Model status and execution paths for WinML and native stacks. [AI_Benchma...lling Deck], [AI_Benchma...ate_080125]

Resource planning and funding gaps for MLPerf and Procyon enablement. [AI_Benchma...lling Deck], [AI_Benchma...ate_080125]

---

## 6. Risks, Gaps, and Dependencies to Anticipate

### Risks

Tight timeline for enabling new models and stacks by Ignite (~2.5 months). [AI_Benchma...ate_080125], [AI_Benchma...lling Deck]

Resource gaps for MLPerf and Procyon support; AMD engagement delayed. [AI_Benchma...2025-08-13], [AI_Benchma...ate_080125], [AI_Benchma...lling Deck]

Unclear requirements for IHV toolchains in Olive and WinML submission policy. [AI_Benchma...2025-08-13], [AI_Benchma...lling Deck]

Cloud-based model conversion timeline unknown; impacts developer experience. [AI_Benchma...2025-08-13], [AI_Benchma...lling Deck]

Ongoing challenges for developers with hardware compatibility and model recompilation. [AI_Benchma...2025-08-13]

### Gaps

Need for clear guidance on Microsoft's plan of record for WinML GA and MLPerf submissions. [AI_Benchma...2025-08-13], [AI_Benchma...lling Deck]

AMD needs to step up engagement; NV schedule slips. [AI_Benchma...ate_080125], [AI_Benchma...lling Deck]

Feasibility study required for new model enablement and pipeline building. [AI_Benchma...ate_080125], [AI_Benchma...lling Deck]

### Dependencies

Procyon 2.0 release (Oct), Olive and WinML readiness for Procyon models. [AI_Benchma...ate_080125], [AI_Benchma...lling Deck]

IHVs must verify and check in toolchains to Olive; fallback operators must provide performance guarantees. [AI_Benchma...lling Deck]

Engagement with ONNX team for fallback operator support. [AI_Benchma...lling Deck]

---

## Strategic Frameworks & Creative Directions

### Reframe Goals

Move from "score chasing" to "platform credibility and developer trust." Benchmarks should validate real-world scenarios and drive product quality, not just numbers. [AI_Benchma...ate_080125], [AI_Benchma...lling Deck]

Use benchmarks as a lever for IHV incentives and market differentiation, not just internal validation. [AI_Benchma...ate_080125], [AI_Benchma...lling Deck]

Shape the narrative: "Windows is the best place to run AI models, regardless of engine (GPU, CPU, NPU)". [AI_Benchma...lling Deck]

### Suggested Frameworks

**Proven, Trusted, Future-Ready**: Structure roadmap around transparent performance, trusted relevance, and future readiness. [AI_Benchma...ate_080125]

**Breadth & Depth**: Ensure all IHVs participate, but also drive deep engagement for flagship models and benchmarks. [AI_Benchma...lling Deck], [AI_Benchma...ate_080125]

**Continuous Improvement**: Build a pipeline for model enablement, validation, and benchmarking that can be reused for BYOM and future scenarios. [AI_Benchma...ate_080125]

---

## Clarifying Questions & Next Steps

What is the primary objective for WinML in H1 2026—performance leadership, developer accessibility, or ecosystem integration? [AI_Benchma...lling Deck]

Should benchmarking focus exclusively on NPU, or expand to GPU/CPU for broader ecosystem impact? [AI_Benchma...lling Deck], [AI_Benchma...ate_080125]

What is the official Microsoft policy for MLPerf submissions—centralized via WinML, or decentralized via IHVs? [AI_Benchma...2025-08-13], [AI_Benchma...lling Deck]

How do we want to manage performance gaps between native and WinML (e.g., graph splitting limitations)? [AI_Benchma...lling Deck], [AI_Benchma...2025-08-13]

What internal benchmarking infrastructure needs to be built or improved? [AI_Benchma...lling Deck]

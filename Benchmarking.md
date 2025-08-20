
# Windows AI Benchmarking Strategy White Paper

## Introduction: Why Benchmarks Matter
Benchmarks are more than performance metrics—they are strategic instruments that shape perception, drive product quality, and influence market adoption. For Windows, they serve as a proof point that our platform is not only competitive but leading in real-world AI performance across diverse hardware.

Benchmarks help us:
- **Build credibility** through transparent, repeatable performance data.
- **Drive optimization** across the software and hardware stack.
- **Influence purchase decisions** for developers and enterprises.
- **Incentivize IHVs** to prioritize Windows performance tuning.

> “Win the Benchmarks, Win the Market.”

---

## Mission & Strategic Plan

**Vision**: Empower every developer and customer to achieve more—with AI that performs best on Windows.

### Strategic Pillars

- **Proven Performance**: Transparent, repeatable benchmarks that validate Windows as the premier AI development platform.
- **Trusted and Relevant**: Benchmarks that reflect real-world developer needs—recognized, respected, and rooted in reality.
- **Future-Ready**: Continuously evolving to showcase Windows leadership across emerging models, tools, and benchmark versions.

### Now / Next / Future Plan

| Phase     | Focus Areas |
|----------|-------------|
| **Now**  | Procyon CV 2.0 enablement for Ignite, MLPerf model execution and feasibility, WinML performance tuning, IHV weekly syncs |
| **Next** | Benchmark model mapping to real-world scenarios, validation gate integration, MLPerf expansion across IHVs |
| **Future**| GPU benchmarking, power/memory metrics, cross-engine comparisons, BYOM pipeline, broader device tiers (Chromebooks, low-cost) |

---

## Ignite 2025 Proposal: Procyon CV 2.0 + MLPerf Showcase

### Objective
Deliver a dual-track Ignite showcase demonstrating Windows AI leadership through:
- **Procyon AI CV 2.0** benchmarks with WinML as the default NPU execution path
- **MLPerf Client** benchmarks with cross-platform execution

### Performance Targets (Applies to Both Tracks)
- WinML achieves **≥95% of native performance** across all platforms
- Benchmarks show **≥5% uplift over Apple M4** on supported models

### Models in Scope

#### Procyon CV 2.0
- **ConvNeXt-Tiny** – Image Classification
- **DETR (ResNet50)** – Object Detection
- **SAM2** – Segmentation
- **Swin2IR** – Super-Resolution
- **BLIP** – Captioning

#### MLPerf Client
- **Llama 4.1** – SLM
- **Phi 3.5** – SLM
- **Phi 4** – SLM

### Timeline
- **MLPerf**: Add details here
- **Procyon AI CV 2.0** release: October 2025
- **Ignite event**: November 21, 2025

### Risks
- Tight timeline (~2.5 months)
- Requires enablement across Olive, WinML, MLPerf stack, and IHV EPs
- MLPerf execution paths vary by IHV (OpenVINO, hybrid, TBD)

### Support Needed
- Olive Toolchain
- WinML stack readiness
- MLPerf coordination (ISV + IHV)
- Validation and tooling
---

## Open Topics

### MLPerf vs Procyon vs Geekbench AI

| Benchmark     | Pros | Cons |
|---------------|------|------|
| **MLPerf**    | Industry standard, generative AI focus | Limited NPU support, complex setup |
| **Procyon**   | Customizable, aligned with Ignite, WinML integration | Less external recognition |
| **Geekbench** | Direct Apple comparison, simple | Light models, less real-world relevance |

**Next Steps**:
- Decide benchmark priority for Ignite
- Align with LT on long-term benchmark strategy

---

### QDQ vs Native Execution Paths

| Path     | Pros | Cons |
|----------|------|------|
| **QDQ**  | • One quantized model for all 4 IHVs<br>• Much easier to manage and deploy<br>• Can deploy quantized model on device and have device do on-device compile<br>• Better for universality | • Biased towards QC on how ops are handled (other IHVs grumble)<br>• Need ONNX team to help even out the playing field (resourcing and buy-in challenge)<br>• Requires ONNXRuntime + driver updates |
| **Native** | • IHVs have more control and prefer this path<br>• More performance boost across IHVs (no QC bias)<br>• Less reliance on ONNX team buy-in<br>• Public toolchains, easier validation<br>• Better for performance | • Need to manage 4 different quantized files (one per IHV)<br>• Pain for deployment and validation<br>• May underperform vs QDQ on QC |

**TLDR**: If we want universality, QDQ is better. If we want performance, native is better. Both paths are supported by Olive.

---

### WinML as Default Path

**Pros**:
- Unified execution story
- Easier onboarding for ISVs
- Aligns with Olive and Windows AI Foundry

**Cons**:
- Not yet GA
- Performance tuning still in progress

**Next Steps**:
- Finalize WinML GA timeline
- Validate across models and IHVs

---

## Future Considerations

This section captures emerging topics that are not yet in scope but are important for long-term planning.

- GPU benchmarking and hybrid execution paths
- Power and memory metrics
- Benchmarking across low-cost and Chromebook tiers
- Cross-engine benchmarking
- BYOM pipeline and automation

# Replat Documentation

## Table of Contents
1. [Overview](#overview)
2. [Objective and Goals](#objective-and-goals)
3. [Replat Architecture](#replat-architecture)
4. [Expected Customer UX](#expected-customer-ux)
5. [Validation](#validation)
6. [FAQ](#faq)

---

## Overview

[Brief description of what Replat is and its purpose]

---

## Objective and Goals

[Brief description of Replat's objectives and goals]


---

## Replat Architecture

### High Level Architecture Diagram
Replat fundamentally transforms how ONNX Runtime (ORT) execution providers (EPs) are distributed and utilized within the Windows ecosystem. Traditionally, ORT clients have been required to bundle execution providers as part of their application packages, creating deployment complexity and increasing package sizes.

With Replat's integration into Windows ML, this paradigm shifts significantly. Windows ML becomes a system-level service available through the Windows App SDK package via the Microsoft Store. The platform intelligently detects the underlying hardware configuration and dynamically provisions the appropriate execution provider UUP (Unified Update Platform) packages for optimal performance.

This architectural evolution enables consuming applications to operate without embedding execution providers directly. Instead, they can dynamically request execution resources, including local NPU acceleration, through the Windows ML interface. This approach reduces application complexity, minimizes deployment overhead, and ensures optimal hardware utilization across diverse Windows device configurations.

![Replat Architecture Diagram](replat_arch.png)

[The attached image shows the complete Replat architecture with all components and their relationships]

---

### **Disabling CPU Execution: Transitioning from Dual Builds to Runtime Control**

As part of the AI Fabric and WinML replat effort, the team is shifting away from the legacy dual-build strategy for disabling CPU execution. Historically, CPU code paths were stripped at build time using flags like `enable CPU`, resulting in separate builds that either included or excluded CPU execution support. While effective, this approach introduced complexity and rigidity into the build pipeline.

The proposed change embraces a more flexible and maintainable model by enforcing CPU execution restrictions at runtime. This involves:

- **Runtime Configuration**: CPU EP access is now governed by session-level flags and policy settings, rather than build-time exclusions. This allows for dynamic control over which execution providers are enabled.
- **Production Safeguards**: In production, only the EP matching the device's package (e.g., NPU) is included. CPU EPs are excluded from these packages, preventing fallback scenarios. AI Fabric will implement additional hardening to ensure only the intended EP is active.
- **Session Protections**: Developers can disable fallback explicitly using session options like `disable_cpu_fallback`, which is supported by providers such as OpenVINO. AMD EPs do not support fallback, while Vitis allows limited fallback for specific operators but includes configuration to restrict this behavior.
- **Testing Flexibility**: The relaxed restrictions enable easier CI and local testing using CPU, without compromising production integrity. This is especially useful for development workflows and regression testing.

This shift reflects a broader effort to streamline deployment, reduce build complexity, and support dynamic configuration across heterogeneous hardware environments. It also aligns with the team's goal of minimizing platform-specific code and standardizing EP packaging and registration via MSIX and NuGet.

---

## Expected Customer UX


---

## Validation

### EP Ingestion and Gating

#### Situation

EP ingestion currently follows two distinct paths. IHVs build EPs, run certification, and submit results to Microsoft. ASG runs validation via PSAPI ingestion, and if tests pass, EPs are ingested. WinPD then runs a 'mini cert' to trust but verify before final ingestion.

With replat, this gets streamlined. IHVs build and certify, submit to Microsoft, WinPD runs mini cert, and if it passes, EP gets ingested directly.

Tim emphasized that WinPD should not be a bottleneck for customer models. Instead, clients like ASG and XBOX should build their own test suites and models. These get onboarded into Microsoft's automation harness - we provide infrastructure and devices, clients provide test plans and models.

The risk is clear: without a solid CP+ model egression test plan and defined roles & responsibilities, replat should not proceed. ASG may delay citing lack of time to build test harnesses. Jerry owns cert1p validation and is building an OSS version of the automation system.

#### Proposal

Microsoft provides certification tools and validation infrastructure. Clients provide test playlists, plans, and models. Everyone plugs into the automation harness.

![EP Validation Process](SupportingFiles/Replat_EP_Validation.png)

Key components:

1. **Shared Infrastructure:** WSSI IDC manages a shared lab/device pool across WSSI, WinPD, and ASG. They're best positioned given existing capabilities like WE2. This avoids duplication and ensures consistency.

2. **Client Integration:** Each client builds their own test suites and models, then integrates with Microsoft's automation harness. If client tests fail, EP ingestion is blocked automatically.

3. **Streamlined Process:** One lab, consistent processes, with Jerry's OSS automation system evaluated for broader use.

#### Next Steps

Lock the validation and replat plan by end of September. October is the RI milestone - by 10/7, we need a working plan in place.

Testing strategy:
- ASG performs accuracy and latency tests using ORT perf test
- App Compat conducts basic and feature-level testing  
- RI gates for AI Fabric with replat enabled by end of month

Collaboration between STCA and WSSI IDC is essential to automate 'trust but verify' processes. The validation strategy must be part of replat, not separate.

### App Compat

App Compat testing ensures existing Windows applications continue working with replat while enabling new dynamic EP capabilities. This covers both basic functionality and feature-level testing across different hardware configurations.

The framework validates that existing WinML apps work unchanged, Windows App SDK integration functions correctly through Microsoft Store delivery, and hardware detection with EP provisioning works across diverse device types.

Testing includes regression validation, fallback scenario verification, and edge case handling to ensure reliable performance across all deployment scenarios.


---

## FAQ


---

*Document Version: 1.0*  
*Last Updated: [Date]*  
*Next Review: [Date]*

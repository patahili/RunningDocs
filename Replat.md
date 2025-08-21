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

### CI Gates

### RI Gates

### AppCompat


---

## FAQ


---

*Document Version: 1.0*  
*Last Updated: [Date]*  
*Next Review: [Date]*

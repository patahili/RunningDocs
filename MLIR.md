# MLIR Architecture and Implementation

## Open Questions

## Architecture

### Architecture Flow: PDLL, Fusion, Decomposition, and Execution Providers

#### 1. High-Level IR (Input IR)
- Originates from model formats like ONNX or PyTorch.
- Defined by upstream tooling (e.g., WinML, AI Toolkit).
- Feeds into the compiler pipeline for transformation.

#### 2. Mid-Level IR (Team Domain)
This is the core of the team's responsibility:
- **PDLL**: Pattern Description Language Layer for transformation rules.
- **Fusion**: Combines ops for performance (e.g., convolution + activation).
- **Decomposition**: Breaks complex ops into primitives.
- **Subgraph & Tile-IR Generation**: Tailored to each IHV's HW IP architecture.
- **Feedback Loop**: Iterative refinement based on IHV feedback and performance metrics.

Referenced in:
- [Efficient Runtime and Unified IR - Walking Deck](https://microsoft.sharepoint-df.com/teams/WINPD-AIPlatformTools-AIPlatform-EfficientRuntimeandUnifiedIR/_layouts/15/Doc.aspx?sourcedoc=%7B031D9364-5B45-4B00-B451-90986F3AB032%7D&file=Efficient%20Runtime%20and%20Unified%20IR%20-%20Walking%20Deck.pptx&action=edit&mobileredirect=true&DefaultItemOpen=1&EntityRepresentationId=87106f4c-916c-41c6-b728-58e10274bfad)
- [DxGML-Subgraph-IR](https://microsoft.sharepoint.com/teams/Real-Time-ML/Shared%20Documents/Key-Material-Information/WindowsML-DxGraphicsML/DxGML-Subgraph-IR.pdf?web=1&EntityRepresentationId=b232403d-38a4-4386-9174-83278beeac71)
- [ONE_Microsoft_Platform_ML_Solution](https://microsoft.sharepoint.com/teams/Real-Time-ML/_layouts/15/Doc.aspx?sourcedoc=%7BA3AFD52E-B106-4710-9722-9395247579DB%7D&file=ONE_Microsoft_Platform_ML_Solution.docx&action=default&mobileredirect=true&DefaultItemOpen=1&EntityRepresentationId=4f91ed08-3fdd-4696-9cfe-1ab20c4e5f67)

#### 3. Low-Level IR (IHV-Owned)
- **IHV-Specific Kernel Compilers**: For GPU, this includes HLSL/SPIR-V.
- **Modernization Path**: IHVs may request deeper control, especially for GPU workloads.
- **DxGML Alignment**: Mid-to-low stack aligns with DirectX ML for real-time gaming and graphics ML workloads.

Referenced in:
- [2023-06 CoreOS E+P AI Long and Mid-Term Plan](https://microsoft.sharepoint.com/teams/coreos/_layouts/15/Doc.aspx?sourcedoc=%7B5CCE20A4-B7B7-4CF3-864D-2D28A97C1BAF%7D&file=2023-06%20CoreOS%20E%2BP%20AI%20Long%20and%20Mid-Term%20Plan.docx&action=default&mobileredirect=true&DefaultItemOpen=1&EntityRepresentationId=71db36de-37a6-4773-8462-e0a18c644a8e)
- [2024-10-02 NPU EP Requirements v1.11.1, Intel](https://microsoft.sharepoint.com/teams/WSSITeam/Shared%20Documents/WSSI%20PM%20Team/Windows%20AI/Specs/NPU%20EP%20Requirements%20Document/NPU%20EP%20Requirements%20Versions/2024-10-02-NPU-EP-Requirements-v1.11.1/2024-10-02%20NPU%20EP%20Requirements%20v1.11.1,%20Intel.pdf?web=1&EntityRepresentationId=0ebae372-09b3-43e8-b4b3-5c592454b0d1)


---

### Execution Provider (EP) Strategy
- **No Shared EP Across IPs**: Each IHV/IP requires a distinct EP due to architectural differences.
- **GPU vs NPU Divergence**: IHVs are pushing for unified EPs (e.g., Medusa), but not before GA.
- **Team Control**: Retain control over mid-level transformations, ensuring flexibility and alignment.

Referenced in:
- QC and Windows ML Workstream Tracker
- AMD and Windows ML Workstream Tracker

### Integration with WinML and DxGML
- **WinML**: Acts as the runtime orchestrator, selecting EPs and managing resource allocation.
- **DxGML**: Provides transformation patterns and fusion strategies for GPU workloads.
- **Compiler IR Handshake**: MLIR-based compiler bridges mid-level IR to low-level driver-specific IR.

Referenced in:
- [DxGML-Subgraph-IR](https://microsoft.sharepoint.com/teams/Real-Time-ML/Shared%20Documents/Key-Material-Information/WindowsML-DxGraphicsML/DxGML-Subgraph-IR.pdf?web=1&EntityRepresentationId=b232403d-38a4-4386-9174-83278beeac71)
- [Efficient Runtime and Unified IR - Walking Deck](https://microsoft.sharepoint-df.com/teams/WINPD-AIPlatformTools-AIPlatform-EfficientRuntimeandUnifiedIR/_layouts/15/Doc.aspx?sourcedoc=%7B031D9364-5B45-4B00-B451-90986F3AB032%7D&file=Efficient%20Runtime%20and%20Unified%20IR%20-%20Walking%20Deck.pptx&action=edit&mobileredirect=true&DefaultItemOpen=1&EntityRepresentationId=87106f4c-916c-41c6-b728-58e10274bfad)

### Key Benefits
- **Scalability**: Enables support across diverse IHVs without compromising performance.
- **Transparency**: Decoder ring initiative ensures IHVs understand model mappings.
- **Ownership**: Team owns the mid-to-low stack, critical for real-time workloads and WinML success.

---

## FAQ

### Q: What is the fallback to SPIR-V in the context of Unified IR, and why is it important?

In scenarios where the Unified Intermediate Representation (UIR) pipeline encounters limitations or incompatibilities—such as unsupported features, hardware constraints, or tooling gaps—a fallback mechanism to SPIR-V (Standard Portable Intermediate Representation - Vulkan) ensures continued functionality and compatibility. This fallback acts as a safety net, allowing shaders or compute workloads to be compiled and executed using a well-established, cross-platform IR format.

The fallback to SPIR-V is particularly relevant when targeting diverse hardware ecosystems or when integrating with existing toolchains that are already optimized for SPIR-V. It provides a practical path for maintaining performance and correctness without blocking development or deployment.

This mechanism is not intended as a primary path but rather as a resilience strategy. It ensures that developers can rely on a consistent execution model even when UIR is not fully supported or optimized for a given scenario. The fallback also facilitates incremental adoption of UIR by allowing teams to transition gradually while preserving compatibility.

### Q: What are Rutvi's 4 workstreams?

**High Level IR**: Dedicated design and implementation of high-level IR, considered a major effort on its own.

**NPU - WinML**: Unified IR POC across NPUs, starting with high-level IR alignment on input.

**GPU - WinML**: Real-time ML workloads targeting GPU through WinML runtime.

**GPU - Gaming and 3D Graphics (+ traditional DirectML customers) - AMD/Xbox alignment**: Real-time graphics workloads, including gaming and existing DirectML customers with specific AMD/Xbox alignment.

### Q: What is the strategic positioning of DirectX APIs versus Windows ML for different developer scenarios?

The strategic recommendation is that **Windows ML should serve as the single entry point for all ML use cases**, while **DirectX APIs should remain available specifically for game developers and gaming scenarios** to provide the flexibility and control they require. This dual approach recognizes the fundamental differences in developer needs between gaming and non-gaming ML workloads.

For game engines, the recommendation suggests they can be driven through Windows ML while maintaining compatibility with existing workflows. However, for individual game developers, maintaining DirectX API access is critically important. Game developers often require the full control and consistency provided by DirectX APIs, and removing this access could negatively impact a large developer base that has built their expertise and workflows around these lower-level interfaces.

The underlying rationale stems from the different priorities between gaming and enterprise scenarios. While DirectX APIs do provide cross-IHV support, other ISV customers prefer Windows ML for its higher-level consistency and quality across Independent Hardware Vendors (IHVs). Windows ML is specifically designed to offer more consistent quality and debuggability across IHVs, which is a key reason why customers in non-gaming scenarios shift from DirectX APIs to Windows ML. Even when the underlying Intermediate Representations (IRs) are similar between both approaches, Windows ML provides higher-level abstraction, cross-IHV consistency, and streamlined quality for ML workloads, making it easier for non-gaming developers to achieve reliable results without requiring deep hardware or API expertise.

In contrast, DirectX APIs provide granular control and flexibility that is preferred by game developers who need explicit schedulability and command-level access to hardware resources. Windows ML focuses on simplicity and policy-level control for broader ML use cases, while DirectX APIs cater to power users who need detailed control and optimization capabilities for real-time performance-critical scenarios. This strategic positioning allows both paths to coexist and serve their respective developer communities effectively.

### Q: What is a Dialect?

A dialect in the context of this meeting refers to a specific intermediate representation (IR) within the MLIR framework that defines a set of operators, data types, and semantics tailored for a particular abstraction level or use case, such as high-level model graphs, subgraphs, or lower-level hardware-specific operations. Each dialect is designed to capture the relevant details needed for optimization, transformation, and interoperability at its respective level in the compiler stack.

Dialects tackle and focus on several key areas:

• **Performance**: The dialect is designed to enable efficient optimization for hardware by providing a minimal, high-level representation that IHVs (independent hardware vendors) can use to apply hardware-specific transformations. This helps ensure that models can be executed efficiently across different platforms.

• **Co-engineering Efficiency**: The dialect allows IHVs to access a generic model representation while still being able to apply their own optimizations. This shared interface streamlines collaboration and reduces the need for multiple, framework-specific implementations.

• **Trace Operator Surface**: By keeping the operator set concise and focused on what is critical for hardware optimization, the dialect avoids unnecessary complexity and ensures that only relevant operations are exposed to IHVs.

• **Serialization and Stability**: The dialect is versioned and strongly typed, ensuring that the operator contracts remain stable over time. This stability is important for both higher and lower levels of the stack, supporting long-term maintainability.

• **Debuggability**: Using MLIR, the dialect supports tracing and annotating subgraphs and transformations, making it easier to debug and understand how high-level constructs are lowered to hardware-specific implementations.

• **Canonical Forms and Consistency**: The dialect enforces consistent patterns (e.g., quantization semantics) so IHVs can reliably recognize and optimize common operations, improving both performance and compatibility.

• **Explicit Manipulation**: The dialect encourages explicit operators for memory layout and tensor manipulation, rather than relying on implicit or introspective logic, which aids in optimization and clarity.

• **Logical Abstraction**: The dialect is kept at a logical level, not dealing with low-level memory management, to maintain abstraction and portability across hardware.

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

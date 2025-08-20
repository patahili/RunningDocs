# XBOX w/WinML

## Notes about XBOX + WinML

## Objective

## FAQ

### Opens

#### 1. Packaging - To CBS or to not CBS

**Problem Overview:**
The question of whether XBOX should use CBS (Component-Based Servicing) or public WASDK packages represents a critical architectural decision that impacts deployment, servicing, and compatibility. CBS packages are confidential, tied to internal builds and preview releases, and governed by NDAs or Microsoft Collaborate Terms of Use. They're intended for validation, development, or deployment within Microsoft's controlled partner ecosystem, not for public distribution unless explicitly approved.

The core issue emerges when considering post-GA scenarios: once WinML becomes GA and customers want to use WASDK, will there be dual WASDK packages on device - both public (from Store) and CBS versions? The answer is yes, and they serve different purposes:

**Public WASDK:**
- Delivered via Store or NuGet
- Used by external developers and apps compiled against public WinAppSDK versions
- Supports side-by-side versioning, allowing apps to target specific versions independently

**CBS WASDK:**
- Delivered via Component-Based Servicing as part of the Windows OS image
- Used by inbox apps and native experiences (Recall, Click to Do, Semantic Search on Copilot+ PCs)
- Tied to OS servicing and CD approvals, with semantic versioning for faster minor revs

**Two Key Opens:**

1. **Long-term Shipping Recommendation for XBOX**
   We need to determine what to recommend for XBOX's shipping configuration. The approach should involve examining how Paint and Photos handle this problem and applying similar learnings to XBOX's situation. This analysis will help establish the right precedent and architectural pattern for XBOX's deployment model.

2. **Short-term CBS Access for Development**
   XBOX needs access to WinML ASAP to begin development and testing. CBS will be available soon for engineering WinML, and we want to explore if it's technically feasible to give XBOX access to this CBS version to unblock them immediately while longer-term shipping decisions are being finalized.

The dual approach allows flexibility for developers while maintaining stability and control for system-level features, but resolving these two opens will provide XBOX with both immediate development access and a clear long-term deployment strategy.

### Resolved FAQ

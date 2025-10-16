# IHV Validation of CoPilot Plus (CP+) PC Features

## Overview

IHVs are held to a high level of standard in terms of key performance indicators (KPI's) for various CoPilot Features and Models. Developed over the last few years using objective, predictive, empirical and experimental methods, these KPI's act as the backbone of ensuring that NPU execution providers (EPs) delivered by IHVs (Intel, Qualcomm, AMD and Nvidia) meet Microsoft's requirements for an optimal set of CoPilot+ experiences. 

This document discusses how IHVs will be able to validate CoPilot+ features at the model, feature and system level. Specifically, this document discusses the state of affairs in the soon-to-be-deprecated "PSORT" stack (that does not use WinML) and the newer "Replat" stack which executes workloads on NPUs using the WinML stack.

## CP+ Feature Validation Landscape

The CP+ feature validation landscape can be divided into 3 levels:

### Model Level 
Accurate execution of models drives the functionality of CP+ features. Additionally, models, especially large ones such as Stable Diffusion XL (SDXL) and Small Language Models (SLMs) take up a significant amount of time in an end to end feature execution process. Model latency can include time taken to schedule a model's execution (i.e: a "workload") on the NPU, as well as time taken to load/unload models from memory in-between execution (hysteresis).

Accurate and performant models form the baseline for successful AI experiences and validating model KPI's act as gates for Microsoft to ingest EPs. Additional model-level KPI's include memory consumption, cache generation time (if applicable), cache loading time, disk size, etc.


### Feature Level
A feature involves the execution of one or more models, either in series or parallel. One model can power more than one feature (such as SDXL being used for Paint CoCreate and Photos). A feature's KPI includes the sum of the KPI's of its constituent models executing at requisite execution priorities and any OS or other system level overheads.

Feature-level KPI's are often evaluated after EP's are integrated and may or may not be used to gate EP ingestion. Feature-level KPI's are used to gate the release of ingested EPs to the public.

### System Level
At the system level, the concurrent execution of CP+ features taxes the system across different dimensions of fundamentals. Thread prioritization, thermal loading, system starvation, etc. come to light when multiple features compete for a finite set of resources on the system such as memory and NPU capacities. System level issues are evaluated through selfhost and the use of test apps to stress test the system beyond what selfhost use cases provide.

## How IHVs Validate EPs in the PSORT Path of Execution
PSORT path refers to the execution path of CP+ AI Fabric features without involving WinML. Execution of workloads on NPU is routed through ORT and EPs carried by each of the ORT clients (PSAPI and OCR). 

At the model level, accuracy is tested using test apps that measure the deviation of execution results against known baselines such as cosine values or CPU execution outputs. Performance of models are validated using test apps that schedule workloads on the NPU in ways that either simulate features (OCR Test App) or as raw workloads (ORT Perf Test).

At the system and feature level is where the biggest pain points lie. For these validations IHVs need to enable CP+ features in-house using experimental bits (OS, AI Fabric w/new features, engineering EPs). Because of the tight coupling between ORT clients and the respective EPs, an AI Fabric build for IHVs that includes PSAPI and OCR with the engineering EP needs to be provided to IHVs. This means that for each engineering drop, the following needs to be done

* IHV shares engineering EP with Microsoft
* PSAPI and OCR each need to integrate this EP into their packages
* An AI Fabric build that includes this PSAPI and ORT needs to be created
* The AI Fabric build then needs to be shared with IHV for use

Each subsequent EP drop requires the team to go through the steps highlighted above. While provisions have been made to enable IHVs to hot-swap (i.e: replace files in place without repackaging) EPs on their side using time-bound AI fabric packages with fewer security restrictions, the tight coupling of EP and ORT clients often requires AI Fabric, PSAPI and OCR updates to align with features and changes specific to EPs. This can lead to dependency breakdowns in the stack and the need to debug, evaluate and release new packages that work properly.

* What IHVs need to enable CP+ features on engineering devices
  * OS with CP+ features
  * AI Fabric with PSAPI/OCR integrated with the right EP
  * Either ability to hot-swap EP or repeated sharing of new AI Fabric packages with engineering EPs

## Path forward with WinML "Replat" Stack
With the transition to WinML, the ingestion, management and release of EP's is done as a standalone process. Ingested EPs are released as packages for WinML to manage and arbitrate on behalf of all WinML Clients. Therefore, WinML clients do not need to manage any part of the EP ingestion process; they can simply invoke API's that request WinML to prepare the underlying stack for them. This results in a few benefits:

* Multiple WinML clients can use the same underlying EP
* Clients do not need to ingest their own EPs. This avoids work on each client in terms of validation
* We reduce the chances of EP torn states as different clients would end up in different stages or phases of EP ingestion through releases

In the WinML stack, PSAPI and OCR do not need to carry IHV EPs. AI Fabric is a smaller, more nimble package that invokes WinML to prepare the device with the right EP and make use of them. Thus, engineering drops of AI Fabric, PSAPI and OCR do not need to be replaced on IHV-side unless there are brand new features that require new pieces of code in these areas. IHVs only need to replace the decoupled underlying EPs which are guaranteed to not contain breaking changes across WinML minor version updates. 

* In this scenario, IHVs will need the following to enable system and feature level testing
  * OS with CP+ features
  * AIFabric with PSAPI and OCR
  * WinML
  * EP Packages

## Comparison of PSORT and Replat Validation Enablement Paths for IHVs

The diagram below shows both the PSORT (yellow) and Replat (Purple) stacks and enabling IHVs with packages for system and feature validation. The dotted lines encompass the steps needed to produce viable packages for IHVs to use for EP development and testing. Note the smaller and more decoupled path within the replat (purple) box.

![Replat IHV Validation Diagram](SupportingFiles/Replat_IHV_Validation.png)

## Enabling IHVs with E2E Feature Enablement Through Replat Stack

WinML is slated to enter WIP around 12A and will signal the start of the deprecation of the PSORT stack. Due to the imminent transition of CP+ feature execution via WinML and the pain points surrounding the PSORT based AI Fabric package, it is recommended that IHVs be set up to validate their EP via the replat stack. Replat packages are being shared with IHVs starting 10/13, with EP hot-swap capability being enabled by the end of October '25.

While replat is in development, AI Fabric packages have side-by-side (SxS) functionality in them to use either the PSORT or the replat stack, depending on the state of a velocity key. IHVs will need this velocity key enabled to utilize the replat stack. The velocity key will be available in the OS after 9D and can also be hard-coded into IHV-friendly AI Fabric packages if needed.

IHVs can be set up for success in two ways:
1. Provide IHVs with fully signed and secure packages. 
   * IHV's will provide engineering EPs to Microsoft and Microsoft will spin signed EP packages within a to-be-determined tight turnaround SLA to IHVs
2. Provide IHVs with a time-bound AI Fabric package with security relaxed enough for them to hot-swap EPs
   * Microsoft will need to reissue new AI Fabric packages at the end of the time-bound date so that IHVs continually have usable bits to work with

Recommendation: Enable IHVs with time-bound AI Fabric Packages with EP hot swap capability
* AI Fabric, PSAPI and OCR will continue to evolve with new features and new packages will need to be shared anyway
* IHVs are free to replace EPs as many times as they want without any intervention from Microsoft. No infrastructure, SLA or agreements are needed to spin signed packages for engineering EP.

## Directly Responsible Teams and Individuals Involved

| Component | Responsible Team/Individual | Details |
|-----------|----------------------------|---------|
| OS with CP+ Features and WinML | Standard EEAP/WIP processes | Can be obtained through standard EEAP, WIP or other processes. WinML is now GA and can be obtained from the store. WinML MSIX can also be provided alongside AI Fabric MSIX files if needed |
| Velocity Key | OS Team | Either in 9D or higher OS. Can be baked into AI Fabric MSIX packages if needed |
| AI Fabric with time-bound packages | AI Fabric Team / Austin Hodges | Can create IHV release branches that spin builds at deterministic intervals |
| WPD STCA | Jerry Xu / Terry Yang | Can provide signed packages for any ingested EP to IHVs as part of WinML release process. Since AI Fabric will allow IHVs to hot-swap EP, the need for intermediary engineering EPs should not be required |

## Timeline to Set IHVs up for Success

* October
  * [10/13] First set of Replat AI Fabric + EPs available to IHV (w/o EP swap capability)
  * [10/31] Replat AI Fabric w/EP swap
* November
  * IHVs verify that E2E system/feature validation has been enabled
  * Establish SLA between MS and IHV for signed packages of ingested EP
  * Establish SLA for AI Fabric package updates within package expiration boundaries
* December
  * 12A Replat WIP + IHV enablement work concluded

---
title: "In-Network Intelligence for Distributed Collaborative Inference Acceleration"
abbrev: "In-Network Inference"
category: info

docname: draft-wang-cats-innetwork-infer-latest
submissiontype: IETF  # also: "independent", "editorial", "IAB", or "IRTF"
number:
date:
consensus: true
v: 3
area: "Routing"
workgroup: "Computing-Aware Traffic Steering"
keyword:
 - in-network intelligence
 - distributed inference
 - collaborative inference
 - deep learning
   
venue:
  group: "Computing-Aware Traffic Steering"
  type: "Working Group"
  mail: "cats@ietf.org"
  arch: "https://mailarchive.ietf.org/arch/browse/cats/"
  github: "kongyanye/draft-wang-cats-innetwork-infer"
  latest: "https://kongyanye.github.io/draft-wang-cats-innetwork-infer/draft-wang-cats-innetwork-infer.html"

author:
 -
    fullname: "Hanling Wang"
    organization: Pengcheng Laboratory
    email: "wanghl03@pcl.ac.cn"
 
    fullname: "Qing Li"
    organization: Pengcheng Laboratory
    email: "liq@pcl.ac.cn"
 
    fullname: "Yong Jiang"
    organization: Tsinghua Shenzhen International Graduate School, Pengcheng Laboratory
    email: "jiangy@sz.tsinghua.edu.cn"
    
normative:

informative:

--- abstract

The rapid proliferation of deep learning models has led to growing demands for low-latency and high-throughput inference across heterogeneous environments. While edge devices often host data sources, their limited compute and network resources restrict efficient model inference. Cloud servers provide abundant capacity but suffer from transmission delays and bottlenecks. Emerging programmable in-network devices (e.g., switches, FPGAs, SmartNICs) offer a unique opportunity to accelerate inference by processing tasks directly along data paths.

This document introduces an architecture for *Distributed Collaborative Inference Acceleration*. It proposes mechanisms to split, offload, and
coordinate inference workloads across edge devices, in-network resources, and cloud servers, enabling reduced response time and improved utilization.

--- middle

# Introduction

Large foundation models and domain-specific deep neural networks are increasingly deployed in real-time services such as surveillance video analysis,
autonomous driving, industrial inspection, and natural language interfaces. Inference for such models requires both **low latency** and **scalable
throughput**.

Current deployments typically follow two paradigms:

* **Edge-only inference**, which minimizes data transmission but is constrained by limited device resources.
* **Cloud-centric inference**, which exploits large compute capacity but introduces network delays.

However, neither paradigm fully exploits the potential of programmable **in-network intelligence**, where intermediate devices along the data
path can actively participate in computation. By integrating such devices into distributed collaborative inference, networks can enable **end-to-end acceleration of large-scale deep learning model inference**.

This document outlines the motivation, problem statement, and architectural considerations for *Distributed Collaborative Inference Acceleration (DCIA)*. The goal is to establish a framework where deep learning inference tasks are intelligently partitioned, scheduled, and executed across heterogeneous resources, including edge devices, in-network resources, and cloud servers.

# Problem Statement

* **Latency bottlenecks:** Large model inference may exceed the latency tolerance of interactive applications if computed only at edge or cloud.  
* **Resource fragmentation:** Heterogeneous resources (edge GPUs, in-network accelerators, cloud clusters) are not effectively coordinated.  
* **Lack of steering semantics:** Existing approaches to service steering are not optimized for inference workload partitioning and scheduling.  

# Proposed Approach

The framework for DCIA includes the following:

1. **Model Partitioning and Mapping**  
   Split large models into sub-tasks (e.g., early layers at edge, mid layers in-network, final layers in cloud) and map them based on
   node capabilities, load, and network conditions.

2. **In-Network Execution**  
   Enable inference acceleration in programmable switches, FPGAs, or SmartNICs, utilizing data-plane programmability to process features in transit (e.g., feature extraction, embedding computation).

3. **Task Scheduling and Steering**  
   Extend service capability advertisements with inference-oriented metrics (e.g., GPU/FPGA availability, model version, layer compatibility), and dynamically balance inference tasks across heterogeneous resources.

4. **Load Balancing Protocols**  
   Support task redirection and failover when a device becomes overloaded, and explore transport-level extensions to allow adaptive task splitting along paths.

# Use Cases

* **Video Analytics:** Smart cameras extract features locally, switches perform intermediate tensor transformations, and cloud servers handle
  complex classification.
* **Autonomous Vehicles:** Onboard processors execute lightweight inference, roadside units conduct mid-layer fusion, and cloud clusters
  finalize planning decisions.  
* **Interactive AI Services:** Edge devices handle pre-processing, in-network resources accelerate embeddings, and cloud models provide
  final responses.

# Conventions and Definitions

{::boilerplate bcp14-tagged}


# Security Considerations

Inference partitioning must consider:

* **Data confidentiality**, ensuring sensitive inputs are not exposed in untrusted network elements.  
* **Model integrity**, preventing tampering or unauthorized reuse of model partitions.  
* **Policy enforcement**, allowing operators to specify where inference may or may not occur.  


# IANA Considerations

This document has no IANA actions.


--- back

# Acknowledgments
{:numbered="false"}

The authors would like to thank colleagues and reviewers in the community who provided feedback on the early version of this draft.

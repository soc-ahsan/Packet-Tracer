# 🌐 Enterprise Multi-Hop Routing Architecture

This repository contains a high-scale point-to-point backbone network topology designed and simulated in Cisco Packet Tracer. The architecture is built to analyze multi-hop packet propagation, structural latency, routing table convergence, and path determination behaviors between an internal endpoint host and a remote enterprise data center server.

---

## 📌 Table of Contents
1. [Project Objectives](#-project-objectives)
2. [Network Architecture Overview](#-network-architecture-overview)
3. [Interactive Topology Diagram](#-interactive-topology-diagram)
4. [Comprehensive Addressing Plan](#-comprehensive-addressing-plan)
5. [Routing Implementation Logic](#-routing-implementation-logic)
6. [Verification & Diagnostic Testing](#-verification--diagnostic-testing)

---

## 🎯 Project Objectives

The primary objectives of designing this multi-node infrastructure include:
* **Multi-Hop Propagation Analysis:** Simulating and studying packet behavior, serialization delays, and TTL (Time-to-Live) decrements across a high hop-count environment from an endpoint host (`Laptop0`) to a destination target (`Server0`).
* **Backbone Routing Table Convergence:** Evaluating the stability and behavior of routing matrices when path updates are systematically synchronized across consecutive transit segments.
* **Deterministic Traffic Pathing:** Ensuring optimal, loop-free packet forwarding mechanisms across multiple autonomous intermediate routing points.
* **Network Baselines & Telemetry:** Establishing a foundation for Security Operations Center (SOC) style traffic inspection, hop validation, and logical perimeter tracking.

---

## 🏗️ Network Architecture Overview

The system is engineered using a granular, point-to-point backbone sequence designed to prioritize linear propagation analytics and transport isolation.

* **Client LAN Zone:** Configured within the `192.168.1.0/24` subnet, serving as the local network segment where `Laptop0` relies on its default gateway (`Router0`) for external communication.
* **Core Transit Backbone:** Consists of 10 interconnected Cisco 2811 Integrated Services Routers (ISR) spanning sequential subnets (`16.10.1.0` through `24.10.1.0`), creating a highly structured transport network.
* **Enterprise Data Center Zone:** Hosted on the `25.10.1.0/24` subnet block, establishing a secure perimeter environment where the backend resource (`Server0`) operates.

---

## 🗺️ Interactive Topology Diagram

The following logical flow charts the point-to-point progression of data paths across the system using GitHub native Mermaid rendering:

```mermaid
graph LR
    subgraph Client_LAN [Client LAN Segment]
        Laptop0[💻 Laptop0 <br> 192.168.1.10/24] 
        Router0[🎛️ Router0 <br> Gateway: 192.168.1.1]
        Laptop0 --- Router0
    end

    subgraph Core_Transit_Backbone [Multi-Hop Core Backbone]
        Router0 ===|16.10.1.0| Router1[Router1]
        Router1 ===|17.10.1.0| Router2[Router2]
        Router2 ===|18.10.1.0| Router3[Router3]
        Router3 ===|19.10.1.0| Router4[Router4]
        Router4 ===|20.10.1.0| Router5[Router5]
        Router5 ===|21.10.1.0| Router6[Router6]
        Router6 ===|22.10.1.0| Router7[Router7]
        Router7 ===|23.10.1.0| Router8[Router8]
        Router8 ===|24.10.1.0| Router9[Router9]
    end

    subgraph DC_Zone [Enterprise Data Center]
        Router9 ===|25.10.1.0| Server0[🗄️ Server0 <br> 25.10.1.2/24]
    end

    style Laptop0 fill:#e6f2ff,stroke:#0066cc,stroke-width:2px
    style Server0 fill:#ffe6e6,stroke:#cc0000,stroke-width:2px
    style Core_Transit_Backbone fill:#f9f9f9,stroke:#666,stroke-width:1px,stroke-dasharray: 5 5

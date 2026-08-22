# John Dondlinger
### Systems Architect | Cloud-Native C# & Edge Engineer | Creator of Metropolis & ZLA

<p align="center">
  <img src="https://readme-typing-svg.demolab.com?font=Fira+Code&weight=600&size=24&pause=1000&color=512BD4&center=true&vCenter=true&width=600&lines=Metropolis-Prime+%2F+MetroNode+Architect;The+Archives+DuckDB+Telemetry+Lake;Watchtowers+Cloudflare+Workers+AI+%26+DO;ZLA+Zero-Liability+Blazor+WASM+PWAs" alt="Typing SVG" />
</p>

<p align="center">
  <a href="https://dotnet.microsoft.com/"><img src="https://img.shields.io/badge/C%23_.NET_10-512BD4?style=for-the-badge&logo=dotnet&logoColor=white" /></a>
  <a href="https://github.com/yavru421/speech-mcp-server"><img src="https://img.shields.io/badge/Kokoro_Speech_MCP-000000?style=for-the-badge&logo=modelcontextprotocol&logoColor=white" /></a>
  <a href="https://workers.cloudflare.com/"><img src="https://img.shields.io/badge/Cloudflare_Workers_%26_DO-F38020?style=for-the-badge&logo=cloudflare&logoColor=white" /></a>
  <a href="https://duckdb.org/"><img src="https://img.shields.io/badge/DuckDB_Telemetry-FFF000?style=for-the-badge&logo=duckdb&logoColor=black" /></a>
  <a href="https://www.rust-lang.org/"><img src="https://img.shields.io/badge/Rust-000000?style=for-the-badge&logo=rust&logoColor=white" /></a>
  <a href="https://developer.nvidia.com/cuda-zone"><img src="https://img.shields.io/badge/NVENC_/_CUDA-76B900?style=for-the-badge&logo=nvidia&logoColor=white" /></a>
</p>

---

## ⚡ Metropolis Infrastructure Topology Map (Bottom-to-Top)

```mermaid
flowchart TD
    subgraph L1["📚 Layer 1: Memory & Telemetry Lake"]
        Archives["The Archives (mind.duckdb / agent_memory.duckdb / st_codex.duckdb)"]
    end

    subgraph L2["🖥️ Layer 2: Primary Bare-Metal Host"]
        MetroNode["Metropolis-Prime (MetroNode Host PC)"]
        GPU["NVIDIA NVENC / CUDA Hardware Accelerator"]
        MetroNode --- GPU
    end

    subgraph L3["🔌 Layer 3: Tethered Sidecars & MCP Mesh"]
        Boroughs["Boroughs (PCIe / USB Accelerators & MCP Protocol Sidecars)"]
        SpeechMCP["Speech MCP Server (C# Kokoro ONNX Speech Engine)"]
        Boroughs --- SpeechMCP
    end

    subgraph L4["📡 Layer 4: Field Devices & Network Fabric"]
        Villages["Villages (Rogue Field SBCs / Battery Pis)"]
        Megalopolis["Megalopolis (Multi-Host Network Fabric)"]
    end

    subgraph L5["⚡ Layer 5: Edge Cloud Router"]
        Watchtowers["Watchtowers (Cloudflare Workers AI & Durable Objects Router)"]
    end

    subgraph L6["🛡️ Layer 6: Zero-Liability Client Ecosystem"]
        ZLA["Zero-Liability Architecture (Blazor WASM PWAs / WebRTC & PeerJS)"]
    end

    Archives --> MetroNode
    MetroNode --> Boroughs
    Boroughs --> Villages
    Boroughs --> Megalopolis
    Megalopolis --> Watchtowers
    Watchtowers --> ZLA

    style Archives fill:#FFF000,color:#000,stroke:#333,stroke-width:2px
    style MetroNode fill:#000000,color:#fff,stroke:#333,stroke-width:2px
    style GPU fill:#76B900,color:#fff,stroke:#333,stroke-width:2px
    style Boroughs fill:#512BD4,color:#fff,stroke:#333,stroke-width:2px
    style SpeechMCP fill:#000000,color:#fff,stroke:#512BD4,stroke-width:2px
    style Villages fill:#333333,color:#fff,stroke:#333,stroke-width:2px
    style Megalopolis fill:#222222,color:#fff,stroke:#333,stroke-width:2px
    style Watchtowers fill:#F38020,color:#fff,stroke:#333,stroke-width:2px
    style ZLA fill:#512BD4,color:#fff,stroke:#333,stroke-width:2px
```

---

## 🏛️ Metropolis Canonical Infrastructure Breakdown

<details open>
<summary><b>🏛️ Metropolis Infrastructure Entities (Click to Collapse)</b></summary>

<br />

| Canonical Metropolis Entity | Classification | System Role & Hardware/Software Bounds |
| :--- | :--- | :--- |
| **`Metropolis-Prime` / `MetroNode`** | Primary Host PC | High-throughput local compute host, NVENC video encoding (1080p60), and orchestrator kernel. |
| **`Boroughs`** | Tethered Sidecars | Attached PCIe cards, USB accelerators, and local MCP sidecars (`workspace-execution`, `speech-mcp-server`, `duckdb-supercharger`, `agy-mcp`, `orchestrator-do`). |
| **`Villages`** | Field SBC Devices | Standalone, battery-powered Raspberry Pi and field SBC nodes executing edge telemetry. |
| **`Megalopolis`** | Multi-Host Fabric | Inter-node networking fabric linking `MetroNode`, `Boroughs`, `Villages`, and edge services. |
| **`Watchtowers`** | Cloudflare Edge Router | Edge routing layer using Cloudflare Workers, **Durable Objects (DO)**, and Workers AI (<35ms latency). |
| **`The Archives`** | Memory & Telemetry Lake | Single-source-of-truth DuckDB telemetry lake (`mind.duckdb`, `agent_memory.duckdb`, `st_codex.duckdb`). |

</details>

<details open>
<summary><b>🛡️ Zero-Liability Architecture (ZLA) Specification (Click to Collapse)</b></summary>

<br />

*Client-side execution and peer-to-peer data transport with zero central server storage exposure.*
- **WebRTC & PeerJS Transport**: Direct peer-to-peer data channels for real-time state sync without server-side database footprint.
- **Local-First PWA Stack**: Installable Blazor WebAssembly PWAs backed by IndexedDB storage, WebSockets, and Windows DPAPI client secrets vaults.

</details>

---

## ⚙️ Native Systems & Low-Latency Engines (Open-Source)

| Engine / Component | Architecture / API | Telemetry & Latency | Source Repository |
| :--- | :--- | :--- | :--- |
| **`win32-process-array-dispatcher`** | Win32 `CreateProcessW` / C# P-Invoke | **$4.2\text{ ms}$** process spawn (vs $142\text{ ms}$ PowerShell) | [![GitHub](https://img.shields.io/badge/GitHub-win32--process--array--dispatcher-512BD4?style=flat-square&logo=github)](https://github.com/yavru421/win32-process-array-dispatcher) |
| **`dxgi-cuda-frame-delta`** | Direct3D 11 DXGI + CUDA `sm_89` (AD107) | **$0.68\text{ ms}$** per 4K frame (**$1,470\text{ FPS}$**) | [![GitHub](https://img.shields.io/badge/GitHub-dxgi--cuda--frame--delta-76B900?style=flat-square&logo=github)](https://github.com/yavru421/dxgi-cuda-frame-delta) |
| **`speech-mcp-server`** | C# .NET 10 / Kokoro ONNX / WASAPI | **$<100\text{ ms}$** startup, 48kHz neural voice | [![GitHub](https://img.shields.io/badge/GitHub-speech--mcp--server-000000?style=flat-square&logo=github)](https://github.com/yavru421/speech-mcp-server) |
| **`METRO-SPEC-2026.08-REV1`** | Host Whitepaper & Distributed Consensus | Production Architecture Specification | [![Spec](https://img.shields.io/badge/Whitepaper-Architecture_Spec-F38020?style=flat-square)](https://dondlingergc.com/architecture) |

---

## 🚀 Live Production Portfolio & Featured Projects (`dondlingergc.com`)

| Production Service / Repo | Live Endpoint / Repository | Status Badge & Highlights |
| :--- | :--- | :--- |
| **Architecture Specification** | [dondlingergc.com/architecture](https://dondlingergc.com/architecture) | [![Live](https://img.shields.io/badge/Live-MudBlazor_Spec-F38020.svg?style=flat-square)](https://dondlingergc.com/architecture) Systems Whitepaper & Trace |
| **Speech MCP Server** | [github.com/yavru421/speech-mcp-server](https://github.com/yavru421/speech-mcp-server) | [![Live](https://img.shields.io/badge/Open_Source-C%23_Kokoro_ONNX-000000.svg?style=flat-square&logo=github)](https://github.com/yavru421/speech-mcp-server) Zero-Latency Neural TTS MCP Engine |
| **TAP Client** | [tap.dondlingergc.com](https://tap.dondlingergc.com) | [![Live](https://img.shields.io/badge/Live-MudBlazor_WASM-512BD4.svg?style=flat-square)](https://tap.dondlingergc.com) Enterprise Control Panel |
| **Personalization Engine** | [personalization.dondlingergc.com](https://personalization.dondlingergc.com) | [![Live](https://img.shields.io/badge/Live-Taskbar_Bridge-F38020.svg?style=flat-square)](https://personalization.dondlingergc.com) Metropolis System Bridge |
| **Skydrop File Transfer** | [skydrop.dondlingergc.com](https://skydrop.dondlingergc.com) | [![Live](https://img.shields.io/badge/Live-PeerJS_ZLA-000000.svg?style=flat-square)](https://skydrop.dondlingergc.com) Zero-Storage File Sharing |
| **Timeline ZLA Engine** | [timelinezla.dondlingergc.com](https://timelinezla.dondlingergc.com) | [![Live](https://img.shields.io/badge/Live-WebRTC_Sync-76B900.svg?style=flat-square)](https://timelinezla.dondlingergc.com) Real-time PDF & Canvas Sync |
| **WaZ Weather Engine** | [wazweather.dondlingergc.com](https://wazweather.dondlingergc.com) | [![Live](https://img.shields.io/badge/Live-WASM_Telemetry-FFF000.svg?style=flat-square&labelColor=black)](https://wazweather.dondlingergc.com) Weather Telemetry Engine |
| **Heckler Soundboard** | [heckler.dondlingergc.com](https://heckler.dondlingergc.com) | [![Live](https://img.shields.io/badge/Live-WebAudio_WASM-512BD4.svg?style=flat-square)](https://heckler.dondlingergc.com) High-Velocity Audio Engine |

---

## 📈 System Benchmarks & Telemetry Performance

```
┌───────────────────────────────────────┬────────────────────────┬──────────────────────┐
│ Benchmark Metric                      │ Local / Edge Target    │ Verified Result      │
├───────────────────────────────────────┼────────────────────────┼──────────────────────┤
│ DXGI → CUDA Frame Delta (4K)          │ NVIDIA AD107 (SM_89)   │ 0.68ms (1,470 FPS)   │
├───────────────────────────────────────┼────────────────────────┼──────────────────────┤
│ Direct Win32 CreateProcessW Dispatch  │ Local Host (C# Native) │ 4.20ms per process   │
├───────────────────────────────────────┼────────────────────────┼──────────────────────┤
│ Kokoro Neural Audio Synthesis         │ Local C# (.NET 10)     │ <100ms startup / ONNX│
├───────────────────────────────────────┼────────────────────────┼──────────────────────┤
│ DuckDB Telemetry Event Ingestion      │ Local Host (`MetroNode`)│ >50,000 events/sec   │
├───────────────────────────────────────┼────────────────────────┼──────────────────────┤
│ Cloudflare Durable Object State Sync  │ Edge (`Watchtowers`)   │ <35ms global latency │
├───────────────────────────────────────┼────────────────────────┼──────────────────────┤
│ NVENC Hardware H.264/HEVC Render      │ NVIDIA GPU Acceleration│ 240 FPS @ 1080p      │
├───────────────────────────────────────┼────────────────────────┼──────────────────────┤
│ ZLA Peer-to-Peer Data Transfer (WebRTC│ Client-side WASM PWA   │ Zero Server Storage  │
└───────────────────────────────────────┴────────────────────────┴──────────────────────┘
```

---

## 📐 Algebraic Pipeline Theory (APT)

$$\mathcal{Y} = \mathcal{A}_n(\mathcal{A}_{n-1}(\dots \mathcal{A}_1(\mathcal{X})\dots))$$

**Algebraic Pipeline Theory (APT)** formalizes workflows as deterministic, composable sequence pipelines. Every system—from hardware-accelerated NVENC video processing to multi-node LLM sidecar orchestration—is engineered as pure, measurable transform functions.

---

## 🛠️ Technology Belt

```
┌─────────────────┬─────────────────────────────────────────────────────────────────┐
│ Core Stack      │ C# (.NET 9/10), C++ / CUDA (sm_89), Rust, TypeScript, DuckDB    │
├─────────────────┼─────────────────────────────────────────────────────────────────┤
│ Edge Computing  │ Cloudflare Workers, Durable Objects (DO), D1, KV, Vectorize, R2 │
├─────────────────┼─────────────────────────────────────────────────────────────────┤
│ Frontend & PWA  │ Blazor WebAssembly (WASM), MudBlazor, ASP.NET Core, HTML5/CSS3  │
├─────────────────┼─────────────────────────────────────────────────────────────────┤
│ AI & Telemetry  │ Agentic MCP Sidecars, Kokoro ONNX, DuckDB Analytics, C-ABI FFI  │
├─────────────────┼─────────────────────────────────────────────────────────────────┤
│ Acceleration    │ Direct3D 11 / DXGI, CUDA Warp Shuffles, FFmpeg, NVENC, NPP      │
└─────────────────┴─────────────────────────────────────────────────────────────────┘
```

---

## 📊 Core Principles & Mindset

> *"Measure twice, formalize once."*

- **Mechanical Realism**: Hardware capabilities, OS boundaries, and memory limitations dictate architecture—no theoretical software loops.
- **Zero Fluff Delivery**: Production-ready code, explicit schema contracts, and verifiable telemetry.

---

## 💼 Contact & Engineering Inquiries

- **Architecture Whitepaper**: [dondlingergc.com/architecture](https://dondlingergc.com/architecture)
- **Portfolio & Live Demos**: [dondlingergc.com](https://dondlingergc.com)
- **GitHub Profile**: [github.com/yavru421](https://github.com/yavru421)

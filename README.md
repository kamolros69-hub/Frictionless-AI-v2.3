# Frictionless AI (v2.0-Alpha)

An open-source AI infrastructure framework designed to eliminate systemic bottlenecks, optimize resource boundaries, and deliver near-zero latency for enterprise AI applications.

---

## ⚡ Core Philosophy
Traditional AI integrations often suffer from high latency, gateway timeouts, and unpredictable resource spikes. **Frictionless AI** decouples computing layers and applies algorithmic optimization to ensure a highly responsive, crash-proof infrastructure.

## 🚀 Key Features

* **Monte Carlo Tree Search (MCTS) v2.0:** Evaluates response paths dynamically to reduce redundant LLM calls and improve reasoning layout.
* **Asynchronous Streaming (FastAPI + SSE):** Utilizes Server-Sent Events to completely eliminate `HTTP 504 Gateway Timeout` errors.
* **Strict Resource Boundaries:** Implements containerized resource isolation to ensure AI sub-processes never compromise core system memory.

---

## 🛠️ Architecture Blueprint

```text
  [ Client UI ]
       │ ▲ (Server-Sent Events)
       ▼ │
┌────────────────────────────────────────┐
│  Frictionless AI Gateway (FastAPI)     │
│  └─► MCTS Reasoning Engine             │
└──────────────────┬─────────────────────┘
                   ▼ (Sub-process Isolation)
        ┌──────────────────────┐
        │  Docker Container    │
        │  Max: 4 Cores / 8GB  │
        └──────────────────────┘
```

---

## 💻 Technical Implementation

### 1. Zero-Latency Streaming (FastAPI & SSE)
Below is the core implementation for handling low-latency asynchronous responses:

```python
import asyncio
from fastapi import FastAPI
from fastapi.responses import StreamingResponse

app = FastAPI(title="Frictionless AI API")

async def frictionless_event_generator():
    # Simulated low-latency MCTS path resolution & streaming
    for token in ["Resolving", " optimal", " path", " via", " MCTS", "..."]:
        yield f"data: {token}\n\n"
        await asyncio.sleep(0.05)

@app.get("/api/v2/stream")
async def stream_ai_response():
    return StreamingResponse(frictionless_event_generator(), media_type="text/event-stream")
```

### 2. Isolated Resource Pod (`docker-compose.yml`)
To keep your production app secure, resource usage is capped at the infrastructure level:

```yaml
version: '3.8'

services:
  frictionless-core:
    build: .
    ports:
      - "8000:8000"
    deploy:
      resources:
        limits:
          cpus: '4.0'
          memory: 8G
        reservations:
          cpus: '2.0'
          memory: 2G
    restart: always
```

---

## 📦 Quick Start

1. **Clone the project:**
   ```bash
   git clone https://github.com
   cd frictionless-ai
   ```

2. **Run Infrastructure:**
   ```bash
   docker-compose up --build -d
   ```
   Open `http://localhost:8000/docs` to test the API gateway endpoints.

---

## 🤝 Contributing
Contributions are what make the open-source community an amazing place. We are currently seeking help on:
* Optimizing MCTS tree-pruning to lower compute token costs.
* Stress testing SSE streams under high concurrency loads.

Feel free to open an **Issue** or submit a **Pull Request**!

---

## 📄 License
Distributed under the MIT License. Developed and maintained by **Kamol Yodsuk** ([@kamolros69-hub](https://github.com)).

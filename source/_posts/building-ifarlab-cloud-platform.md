---
title: "Building the IFARLAB Cloud Platform: Lessons from an EU Horizon Europe R&D Project"
date: 2026-03-31 13:00:00
tags:
  - cloud-architecture
  - Docker
  - Node.js
  - React
  - IoT
  - ROS2
  - EU-project
  - MATISSE
  - machine-learning
categories:
  - Software Architecture
description: "How I architected a unified cloud platform that integrates FMI/FMU co-simulation, ROS 2 telemetry, and 3D Digital Twins for the MATISSE EU Horizon Europe project."
---

When I joined the [MATISSE EU Horizon Europe KDT Project](https://matisse-kdt.eu/) at Eskisehir Osmangazi University, the challenge was clear: multiple academic research groups were producing independent models — FMI/FMU co-simulations, ROS 2 robot telemetry, 3D Digital Twins, computer vision pipelines — and none of them could talk to each other.

My job was to build the infrastructure that brings them together.

<!-- more -->

## Key Takeaways

- A central Platform API simplified auth, routing, logging, and versioning across services.
- Docker + NGINX + `docker-compose` was sufficient for research-scale deployment.
- Observability and ADRs early prevented repeated architecture debates later.
- Real-time telemetry (WebSockets) introduced subtle reliability and state-sync problems.
- Storage choices worked best when matched to workload (MongoDB, InfluxDB, PostgreSQL).

## The Problem

The MATISSE project is a large-scale EU Horizon Europe initiative. At ESOGU, our lab (IFARLAB) works on several parallel research tracks:

- **Co-simulation models** using FMI/FMU standards for industrial process simulation
- **ROS 2 telemetry** from robotic systems for real-time monitoring
- **3D Digital Twins** for visual representation of physical systems
- **YOLOv8-based defect detection** for robotic quality inspection

Each of these was developed by different researchers, in different languages, with different data formats and deployment requirements. There was no shared infrastructure, no unified API, and no single dashboard where you could see everything.

The question wasn't just "how do we deploy these?" — it was "how do we make them work as one system?"

## The Architecture

I designed the **IFARLAB Cloud Platform** as a centralized ecosystem with a clear separation of concerns:

### Platform API — The Central Hub

The Platform API is a Node.js/Express service that acts as the single entry point for all frontend requests. It connects to 6 backend services:

- **Simulation Service** — dispatches and monitors FMI/FMU co-simulation runs
- **Telemetry Service** — ingests and serves real-time ROS 2 data via WebSocket
- **Vision Service** — handles YOLOv8 inference requests and returns detection results
- **Digital Twin Service** — serves 3D model data and state synchronization
- **Auth Service** — JWT-based authentication and role management
- **Dashboard Service** — aggregates data for Grafana-embedded dashboards

Each service runs in its own Docker container. The Platform API handles routing, authentication verification, and response normalization.

### Why a Central API Instead of Direct Service Access?

The alternative was letting the React frontend call each service directly. We rejected this for several reasons:

1. **Authentication** — JWT verification happens once at the Platform API, not in every service
2. **CORS management** — one origin to configure, not six
3. **Service discovery** — the frontend doesn't need to know service addresses; the Platform API handles routing
4. **Rate limiting and logging** — centralized, not duplicated
5. **API versioning** — easier to manage a single versioned interface

The trade-off: the Platform API becomes a potential bottleneck. For our scale (research lab, not millions of users), this was acceptable. For larger systems, you'd consider an API gateway like Kong or AWS API Gateway.

## Deployment Stack

```
React Dashboard (Cloudflare CDN)
        ↓ HTTPS
Platform API (Node.js :3000)
    ↓ REST          ↓ WebSocket       ↓ REST
Simulation      Telemetry         Vision Service
(Python)        (Python/ROS2)     (FastAPI + YOLOv8)
    ↓               ↓                 ↓
MongoDB          InfluxDB          PostgreSQL
```

Everything runs on Docker with `docker-compose` for orchestration. NGINX sits in front as a reverse proxy handling TLS termination and load distribution.

### Key Decisions

**MongoDB for simulation metadata** — simulations have varying schemas depending on the model type. Document storage handles this naturally without rigid table definitions.

**InfluxDB for telemetry** — time-series data from ROS 2 sensors needs efficient range queries ("give me all temperature readings from the last 5 minutes"). InfluxDB is purpose-built for this.

**PostgreSQL for vision results** — detection results have consistent structure (bounding boxes, confidence scores, labels) and benefit from relational queries and joins.

## YOLOv8 Defect Detection System

One of the most tangible outputs was a real-time cup damage detection system for robotic pick-and-place operations.

**The pipeline:**
1. Camera captures image of cup on conveyor belt
2. Image sent to Vision Service via REST
3. YOLOv8 model runs inference
4. Detection results (bounding boxes, damage type, confidence) returned
5. Robot controller decides: pick or reject

**Results:**
- **98% recall** on a custom 2,475-image dataset
- Sub-200ms inference time on GPU
- 4 damage categories: crack, chip, stain, deformation

This work is documented in our paper submitted to IEEE SIU 2026: *"YOLOv8-Based Real-Time Cup Damage Detection for Robotic Pick-and-Place."*

## Project Coordination Tools

Beyond architecture, managing a multi-team research project requires disciplined coordination. Here's what worked for us:

- **Jira** for task tracking within our team
- **Confluence** for technical documentation
- **PlantUML** for architecture diagrams (version-controlled in GitLab)
- **Custom dashboard** for progress tracking across work packages

## Lessons Learned

### 1. Start with the API contract, not the implementation
Before writing code, we defined the JSON contracts between services. This let frontend and backend teams work in parallel.

### 2. Docker-compose is enough for research-scale projects
We didn't need Kubernetes. For a team of 5-10 researchers deploying to a few servers, `docker-compose` with proper health checks and volume management was sufficient.

### 3. Observability from day one
We added structured logging and Grafana dashboards before the first "real" deployment. When something broke (and it did), we could diagnose it in minutes rather than hours.

### 4. Document the "why," not just the "how"
Architecture Decision Records (ADRs) — short documents explaining why we chose MongoDB over PostgreSQL for simulations, or why we centralized authentication — saved us from re-debating decisions months later.

### 5. Real-time is harder than it looks
WebSocket connections for ROS 2 telemetry introduced challenges: reconnection logic, message buffering during network drops, and client-side state synchronization. Don't underestimate the complexity of real-time data delivery.

## What's Next

The platform continues to evolve. Current priorities:
- Edge deployment for YOLOv8 inference (reducing latency by running models closer to the camera)
- ROS 2 integration improvements for bi-directional robot control
- Automated CI/CD pipeline with GitLab for multi-service deployment

If you're interested in the technical details, the project is partially open-source: [ESOGU-IFARLAB-Cloud-Application on GitHub](https://github.com/ESOGU-SRLAB/ESOGU-IFARLAB-Cloud-Application).

*Working on an EU research project? I'd love to exchange experiences. Reach out on [LinkedIn](https://www.linkedin.com/in/burak2kanber/) or [GitHub](https://github.com/datkanber).*

---

> **Funding Acknowledgment:** This work is part of the [MATISSE project](https://matisse-kdt.eu/), funded by the European Union's Horizon Europe programme under the Key Digital Technologies Joint Undertaking (KDT JU). Views and opinions expressed are the author's own and do not necessarily reflect those of the European Union or KDT JU. Neither the European Union nor the granting authority can be held responsible for them.

## Related Posts

- {% post_link plantuml-system-architecture-diagrams PlantUML for System Architecture Diagrams %}
- {% post_link welcome-to-my-blog Welcome to My Blog (Context & Topics) %}
- {% post_link just-build-it-book-announcement Just Build It — Book Announcement %}

---
title: "Announcing My Book: Just Build It — From Consuming to Producing Technology"
date: 2026-03-31 14:00:00
tags:
  - book
  - IoT
  - Python
  - Docker
  - machine-learning
  - ROS2
  - autonomous-systems
categories:
  - General
description: "I'm writing a technical book that takes you from a Raspberry Pi on your desk to an autonomous drone fleet — building real systems chapter by chapter."
---

I'm writing a book, and it's not a typical programming tutorial.

**"Just Build It: From Consuming to Producing Technology"** is a hands-on engineering book where every chapter builds on the previous one. You start with a Raspberry Pi and a GPS module. By the end, you've built an autonomous cargo drone fleet with real-time telemetry, machine learning APIs, computer vision, and ROS 2 integration.

<!-- more -->

## Key Takeaways

- The book is project-driven: every chapter extends a single evolving system.
- It emphasizes production thinking early (deployment, observability, contracts, CI/CD).
- Exercises are tiered (basic → intermediate → advanced) to build real autonomy.

## The Philosophy

The title says it all. Most of us spend years consuming technology — reading tutorials, watching courses, following documentation. At some point, the shift has to happen: you need to **produce**, not just consume.

This book is designed to force that transition. There's no chapter you can passively read and feel like you learned something. Every concept appears as a working part of a real system.

## What the Book Covers

The book is organized into 4 parts across 13 chapters:

### Part 1: Foundations — The Birth of a System
- **Chapter 1** — First Connection: turning a Raspberry Pi into a GPS-tracked bike system. Docker, MariaDB, SQL fundamentals.
- **Chapter 2** — The World of Data: statistics, feature engineering, train/test split, RandomForest, model evaluation, overfitting.
- **Chapter 3** — API Bridges: HTTP lifecycle, FastAPI, Pydantic validation, endpoint design patterns.
- **Chapter 4** — From Localhost to Production: staging vs production, readiness/liveness probes, rollback, migration, observability, CI/CD.
- **Chapter 5** — Architectural Thinking: PlantUML diagrams, data contracts, schema evolution, backward compatibility.

### Part 2: Python and the Autonomous System
- **Chapter 6** — Python Fundamentals through a drone's brain: variables, data structures, OOP, inheritance.
- **Chapter 7** — Resilient Systems: exception handling hierarchies, logging, file I/O, external API integration.
- **Chapter 8** — Scaling: PyTest with boundary testing and mocking, Docker layer optimization, async programming, REST vs WebSocket.

### Part 3: Fleet Intelligence
- **Chapter 9** — The Swarm: multi-drone coordination, task assignment algorithms, conflict resolution.
- **Chapter 10** — Computer Vision: OpenCV basics, YOLOv8 object detection, training custom models, real-time inference pipelines.

### Part 4: Industrial Systems
- **Chapter 11** — Robot Operating System: ROS 2 fundamentals, topics, services, actions, robot arm control.
- **Chapter 12** — Edge AI: deploying models on resource-constrained hardware, TensorRT optimization.
- **Chapter 13** — Digital Twin: connecting physical systems to their virtual counterparts, real-time synchronization.

## Who Is This Book For?

The ideal reader has 1–4 years of experience. They know Python (or are learning it) but have never built an end-to-end working system. They're tired of fragmented tutorials that teach isolated concepts without showing how everything connects.

If you've ever thought, "I know the pieces but I can't put them together" — this book is for you.

## What Makes It Different?

1. **Cumulative architecture** — Each chapter builds on the system from the previous chapter. There are no isolated examples that you build and throw away.

2. **Real failure modes** — Every chapter includes common mistakes, why they happen, and how to fix them. I don't just show the happy path.

3. **Practical exercises at three levels** — Basic (follow along), Intermediate (extend the system), and Advanced (design and architect).

4. **Production thinking from chapter one** — Docker, SQL, API design, deployment, and observability appear in the first few chapters — not as an afterthought at the end.

5. **It comes from real project experience** — The patterns in this book are drawn from hands-on work on cloud platforms, IoT systems, and enterprise automation. These aren't hypothetical examples.

## Current Status

The expanded and enriched edition is in progress. The first edition was published independently through Amazon Kindle Direct Publishing in 2025. The current revision significantly expands each chapter with:
- Step-by-step explanations
- More code examples with inline commentary
- Exercises at every level
- "Common Mistake" callout boxes
- Mini-lab sections for hands-on practice

## A Taste of the Approach

Here's the opening of Chapter 1:

> *"Your hardware list with 'buy' written at the end doesn't mean the project has started. The real challenge is giving these components a purpose."*

You start with a Raspberry Pi, a GPS module, and a powerbank. By the end of Chapter 1, you have a working bike tracker storing GPS coordinates in a Dockerized MariaDB database, queryable with SQL. That's not a toy example — it's the foundation that every subsequent chapter builds upon.

## Follow the Progress

I'll be sharing excerpts, behind-the-scenes decisions, and lessons learned from the writing process on this blog. If you're interested in the book or have feedback, reach out:

- [GitHub](https://github.com/datkanber)
- [LinkedIn](https://www.linkedin.com/in/burak2kanber/)
- Email: burak2kanber@gmail.com

*The best way to learn technology is to build something real with it. That's the whole point.*

## Related Posts

- {% post_link welcome-to-my-blog Welcome to My Blog (Context & Topics) %}
- {% post_link building-ifarlab-cloud-platform Building the IFARLAB Cloud Platform (Architecture Lessons) %}

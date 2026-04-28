---
layout: project
title: Mini-IDS
author: me
---

A lightweight home network intrusion detection & monitoring system built with
C, Python, Flask and SQLite.

| Status: | In development |
|Tech Stack: | C, Python, Flask, SQLite, Docker, Linux, Networking |
|Github: | [GitHub Repo](https://github.com/0xF47E/mini-ids) |

___

## Dev Log

### Project Planning

**Initial goal**:

build a lightweight home network monitoring system consisting of:

- C-based network scanner
- Python-based controller
- structured scan output
- persistent scan history
- change detection over time

**Key decisions**:

- Scanner written in C for low-level networking control
- Controller written in Python for orchestration and data handling
- Communication via NDJSON over stdout
- SQLite used for persistent scan storage
- System designed to run inside docker

___

### Project Initialization

**2026-02-04**

Initial repository setup.

**Key decisions**:

- CI workflow to include automated build and test steps
- validate scanner compilation

**What I Learned**:

- Basic Github Actions workflow setup
- Importance of automated builds from day one

___

### Minimal Scanner Implementation

**2026-02-04**

First working scanner version completed.

**Capabilities**:

- Buildable C project with Makefile
- CLI entry point
- TCP connect scanning using sockets
- Single host / single port scanning

**What I Learned**:

- Basic socket programming in C

___

### Structured Scanner Output

**2026-02-05**

Scanner output changed from debug text to NDSJON

- Easier parsing by controller
- Streaming-friendly output format

**Example Output:**

```bash
{"ts":1771690369, "target":"127.0.0.1","port":22,"state":"closed"}
```

**Additional Improvements:**

- better error handling
- updated `.gitignore` for C artifacts

___

### Python Controller Introduction

**2026-02-07**

Added the orchestration layer in Python

**Responsibilities:**

- Execute scanner as subprocess
- Capture stdout
- Parse NDJSON lines
- save results to file

**What I Learned:**

- Subprocess handling
- Combining C and Python cleanly

___

### Docker Environment

**2026-02-08**

Containerized the project.

**Docker Responsibilities:**

- Build scanner
- RUn controller
- Provide reproducible runtime environment

___

### Scanner Enhancements

**2026-02-08**

Expanded the scanner functionality.

**Changed:**

- multiple port scanning
- improved result handling
- better logging behavior

___

### Controller Behavior Adjustments

**2026-02-10**

Refined controller workflow.

**Goals:**

- Stabilize default behavior
- Prepare for future scheduled scans
- Improve orchestration logic

___

### Port Parsing Improvements

**2026-02-12**

Improved CLI port handling.

**Changes:**

- Dynamic memory allocation for ports
- Support comma-separated lists

___

### Scanner Refactor

**2026-02-13**

Internal cleanup and structural improvements.

**Changes:**

- Refactored scanner flow
- Improved internal structure
- Port sorting before scanning using quicksort

___

### Database Integration

**2026-02-21**

Controller upgraded to persistent storage with SQLite.

**Database Responsibilities:**

- Persistent scan history
- Enable future diff/change detection
- Foundation for alerts and dashboard

___

### CIDR Parsing & ARP Host Discovery

**2026-02-24**

Most difficult phase so far.
Implemented subnet scanning and active host discovery.

**Goals:**

- Accept CIDR notation
- Scan multiple hosts in a subnet
- Avoid unnecessary port scans on offline hosts

**Key decision:**

- ARP discovery before TCP scanning
- Raw sockets for ARP requests
- Low TCP timeout for internal network scanning

**What I Learned:**

- Raw sockets are challenging
- SOCK_DGRAM can simplify ARP crafting
- Bitwise logic requires careful debugging

___

### Data Access Layer + First Web UI

**2026-02-25**

Large architecture improvement.

**Data Access Layer**

Database logic extracted into a shared module.

**Web UI**

First browser-based interface using Flask.

___

## Current Status

Implemented:

- TCP connect scanning
- Multi-port scanning
- CIDR subnet support
- ARP host discovery
- NDJSON component interface
- Python orchestration
- Docker runtime
- SQLite persistence
- Shared DAL
- Simple Web UI
- CI pipeline

## Next Steps

Planned features:

- Snapshot diff detection
- Alert system
- Telegram notfications
- Improved dashboard
- Scheduled recurring scans
- Parallelized scanning
- Historical graphs / trends

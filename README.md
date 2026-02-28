# Linux-process-management-lab-with--signal-demos
# 🐧 Linux Process Management Lab

A hands-on lab demonstrating Linux process management and signal handling using real terminal examples.

This project explores how processes behave when receiving different termination signals and explains the critical difference between **SIGTERM** and **SIGKILL** — something every DevOps engineer must understand.

---

## 📌 Project Overview

Process management is a fundamental skill in DevOps and system administration.

In production environments (servers, containers, Kubernetes clusters), stopping a process incorrectly can cause:

- Data corruption
- Service downtime
- Lost logs
- Broken deployments

This lab demonstrates how Linux signals work and why graceful termination matters.

---

## 🧠 What Are Linux Signals?

Signals are software interrupts sent to a process to notify it that an event has occurred.

They are used for:

- Process termination
- Process control
- Inter-process communication (IPC)
- Handling unexpected behavior

Signals allow the operating system to communicate with running processes.

---

## 📬 Common Linux Signals

| Signal   | Number | Description |
|----------|--------|------------|
| SIGTERM  | 15     | Graceful termination request |
| SIGKILL  | 9      | Immediate force termination |
| SIGINT   | 2      | Interrupt from keyboard (Ctrl+C) |
| SIGHUP   | 1      | Terminal closed / reload signal |

---

## ⚖️ SIGTERM vs SIGKILL

Understanding the difference between these two signals is critical in real-world environments.

| Feature | SIGTERM | SIGKILL |
|----------|----------|----------|
| Signal Number | 15 | 9 |
| Can be caught by process? | ✅ Yes | ❌ No |
| Allows cleanup? | ✅ Yes | ❌ No |
| Graceful shutdown? | ✅ Yes | ❌ No |
| Recommended for production? | ✅ Yes | ⚠️ Only if necessary |

### 🔹 SIGTERM (Graceful Shutdown)

- Default signal when running `kill <PID>`
- Allows the application to:
  - Close files
  - Save data
  - Release resources
  - Shut down cleanly

This is how production systems should normally be stopped.

---

### 🔹 SIGKILL (Force Termination)

- Sent using `kill -9 <PID>`
- Cannot be caught or ignored
- Immediately stops the process
- No cleanup is performed

Using SIGKILL in production can result in:

- Corrupted files
- Incomplete transactions
- Lost data

---

## 🧪 Lab Demonstration

### 1️⃣ Start a Test Process

```bash
sleep 300

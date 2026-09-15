# Phase 1: Linux, OS Internals & Networking Fundamentals

The foundation phase. Every later phase (Docker, Kubernetes, Terraform, CI/CD)
is, underneath, a set of OS and networking primitives wearing a nicer interface.
This phase makes those primitives explicit before touching any tool that hides them.

## Modules

| # | Module | Study Notes (PDF) | Topic Map (Wiki) | Status |
|---|--------|--------------------|--------------------|--------|
| 1 | Linux Foundations → Kernel Internals | [PDF](./module-01-linux-foundations-kernel-internals.pdf) | [Wiki](../../wiki/Module-1-Linux-Foundations) | 🟡 |
| 2 | Permissions → Access Control Models | — | [Wiki](../../wiki/Module-2-Permissions-Access-Control) | ⚪ |
| 3 | Processes → Scheduling → Concurrency | — | [Wiki](../../wiki/Module-3-Processes-Scheduling) | ⚪ |
| 4 | Memory → Virtual Memory → Advanced Tuning | — | [Wiki](../../wiki/Module-4-Memory-Management) | ⚪ |
| 5 | Storage & Filesystems | — | [Wiki](../../wiki/Module-5-Storage-Filesystems) | ⚪ |
| 6 | Networking: Basics → Advanced | — | [Wiki](../../wiki/Module-6-Networking) | ⚪ |
| 7 | Containers From First Principles | — | [Wiki](../../wiki/Module-7-Containers-Cgroups-Namespaces) | ⚪ |
| 8 | Shell Scripting | — | [Wiki](../../wiki/Module-8-Shell-Scripting) | ⚪ |
| 9 | Security Hardening | — | [Wiki](../../wiki/Module-9-Security-Hardening) | ⚪ |
| 10 | Performance Engineering & Debugging | — | [Wiki](../../wiki/Module-10-Performance-Debugging) | ⚪ |

## Capstone
Build a minimal container runtime from scratch (`unshare` + `chroot` + cgroups)
and write an incident-response runbook for a simulated "server under load" scenario.

## Key connections established in this phase
- cgroups/namespaces (Module 7) → directly explains Docker/Kubernetes internals in Phase 3
- Network namespaces & iptables (Module 6) → directly explains Docker networking & kube-proxy in Phase 3
- OOM killer tuning (Module 4) → directly explains Kubernetes memory limits/OOMKilled events

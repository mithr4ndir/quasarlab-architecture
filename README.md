# 🌌 Quasarlab: My Homelab DevOps Universe

Welcome to **Quasarlab**, a self-hosted DevOps lab environment designed to simulate real-world infrastructure — fully codified, observable, and secure. This architecture powers a hybrid mix of Linux and Windows systems using modern DevOps tooling, storage orchestration, and centralized monitoring.

---

## 🧠 Purpose

To demonstrate and experiment with:
- Infrastructure-as-Code provisioning
- Configuration management and service orchestration
- PKI and authentication integration
- Observability (metrics, logs, alerts)
- Hybrid VM infrastructure
- Scalable storage provisioning (ZFS + iSCSI)

---

## 🗺️ Architecture Overview

- **Hypervisor**: Proxmox VE (bare metal)
- **Storage Backend**: TrueNAS Core (ZFS + iSCSI targets)
- **Operating Systems**: Ubuntu, Windows Server
- **Networking**: pfSense + VLANs
- **Monitoring & Observability**: Prometheus, Grafana, Vector, Elastic Stack
- **CI/CD**: GitHub Actions
- **Automation**: Terraform, Puppet, PowerShell, Bash
- **Identity & Auth**: AD, SAML, PKI, Onelogin

![Diagram](./diagrams/quasarlab-overview.png) <!-- Optional if you plan to include -->

---

## 🔗 Linked Repositories

| Repository | Description |
|------------|-------------|
| [`terraform-quasarlab`](https://github.com/mithr4ndir/terraform-quasarlab) | Infrastructure provisioning with Terraform |
| [`puppet-nebula`](https://github.com/mithr4ndir/puppet-nebula) | Configuration management for Linux & Windows services |
| [`cosmic-observability`](https://github.com/mithr4ndir/cosmic-observability) | Logging + metrics pipeline: Vector → Elastic/Grafana |
| [`scripts-from-orion`](https://github.com/mithr4ndir/scripts-from-orion) | Bash and PowerShell automation scripts |
| [`quasarlab-ci-cd-pipeline`](https://github.com/mithr4ndir/quasarlab-ci-cd-pipeline) | GitHub Actions CI/CD pipeline demo |
| [`quasarlab-storage-core`](https://github.com/mithr4ndir/quasarlab-storage-core) | ZFS/iSCSI TrueNAS integration and snapshots |
| [`pki-vault-asteria`](https://github.com/mithr4ndir/pki-vault-asteria) | Internal PKI demo with automated cert issuance/renewal |

---

## 💽 Storage Architecture: TrueNAS + ZFS + iSCSI

### 🧱 ZFS Configuration
- **Pool Layout**: Mirrors + single disk cache (ZIL)
- **Datasets**: Created for VM storage, backups, logs
- **Snapshots**: Daily via cron; replication planned via `rclone`
- **Compression**: Enabled (lz4) for storage efficiency

### 🔗 iSCSI Target Setup
- **Targets**: Configured per Proxmox cluster node
- **Authentication**: Mutual CHAP for added security
- **Provisioning**: Exposed as raw disk devices to Proxmox for VM use
- **Resiliency**: Backed by RAID-Z2 equivalent with S.M.A.R.T. alerts

> Configuration files and automation scripts available in [`quasarlab-storage-core`](https://github.com/mithr4ndir/quasarlab-storage-core)

---

## 📊 Observability Stack

- **Metrics**: Prometheus + Node Exporter
- **Logs**: Vector agent → Elastic stack
- **Dashboards**: Grafana with panels for system health, disk I/O, network flow
- **Alerting**: Future integration with Slack/Webhooks for threshold-based alerts

---

## 📦 Automation & CI/CD

- **Terraform**: Codifies infra state — VMs, network configs, firewall rules
- **Puppet**: Manages installed services, hardening, user creation
- **CI/CD**: GitHub Actions builds/deploys containerized or script-based apps

---

## 🎯 Roadmap

- [ ] Automate snapshot pruning + offsite replication (e.g., S3 via `rclone`)
- [ ] Use GitHub Actions to lint Puppet/Terraform config
- [ ] Build PKI trust chain using Vault with renewable certs
- [ ] Grafana alerting to Slack or webhook endpoints

---

# GCP Calculator MCP Server (Golang)

[![Go Reference](https://pkg.go.dev/badge/github.com/Mireu-Lab/GCP-Calculator-MCP.svg)](https://pkg.go.dev/github.com/Mireu-Lab/GCP-Calculator-MCP)
[![License: LGPL v3](https://img.shields.io/badge/License-LGPL_v3-blue.svg)](https://www.gnu.org/licenses/lgpl-3.0)
[![GitHub Wiki](https://img.shields.io/badge/docs-GitHub_Wiki-brightgreen.svg)](https://github.com/Mireu-Lab/GCP-Calculator-MCP/wiki)
[![Go CI](https://github.com/Mireu-Lab/GCP-Calculator-MCP/actions/workflows/ci.yml/badge.svg)](https://github.com/Mireu-Lab/GCP-Calculator-MCP/actions)
[![Go Version](https://img.shields.io/badge/Go-1.21%2B-00ADD8?logo=go)](https://go.dev/)

> **GCP Calculator MCP Server** is a high-performance **Model Context Protocol (MCP)** server and CLI tool engineered in Go. It provides comprehensive cost calculation, dynamic regional multiplier evaluation, Committed Use Discount (CUD) modeling, and accurate dual currency estimation (USD & KRW) for all 115+ Google Cloud Platform (GCP) services.

---

## ✨ Key Features

- 🌍 **Dynamic Regional Pricing Multipliers**
  - Automatic pricing tier adjustment across major GCP regions (`us-central1`: 1.00, `asia-northeast3` (Seoul): 1.20, `asia-northeast1` (Tokyo): 1.18, `europe-west1`: 1.10, etc.).
- 📉 **Commitment Discounts & Spot Savings**
  - Spot/Preemptible discounts (~70-91%) and **1-Year (37% discount)** and **3-Year (55% discount)** Committed Use Discounts (CUD).
- 💵 **Dual Currency Support (USD & KRW)**
  - Real-time exchange rate synchronization (1 USD = 1,334.51 KRW) aligned with Google Finance and official exchange benchmarks.
- ⚡ **Universal Evaluator for 115+ GCP Products**
  - Dynamic cost evaluation against structured catalog datasets covering Compute, Storage, Databases, Analytics, Vertex AI, Networking, and Security.
- 🔌 **Full Model Context Protocol (MCP) Integration**
  - Seamlessly integrates with Antigravity, Claude Desktop, Cursor, and any LLM agent supporting JSON-RPC 2.0 stdio with 8 production-ready tools:
    - `calculate_compute_engine`
    - `calculate_cloud_run`
    - `calculate_storage`
    - `calculate_gke`
    - `calculate_cloud_sql`
    - `calculate_bigquery`
    - `calculate_gcp_service`
    - `estimate_infrastructure`

---

## 🚀 Quick Start

### 1. Installation & Build

```bash
git clone https://github.com/mireu-workflow/GCP-Calculator-MCP.git
cd GCP-Calculator-MCP
go build -o gcp-calculator-mcp main.go
```

### 2. MCP Server Configuration (Antigravity / Claude Desktop / Cursor)

Add the server to your `mcp_config.json` or `claude_desktop_config.json`:

```json
{
  "mcpServers": {
    "gcp-calculator": {
      "command": "/absolute/path/to/gcp-calculator-mcp",
      "args": ["server"]
    }
  }
}
```

---

## 💻 CLI Usage & Examples

```bash
# 1. Compute Engine VM (Seoul region + 3-Year CUD discount)
./gcp-calculator-mcp compute -machine e2-standard-4 -region asia-northeast3 -commitment 3-year

# 2. Cloud Storage (Seoul region + Standard 500GB)
./gcp-calculator-mcp storage -class standard -gb 500

# 3. Dynamic Universal GCP Service Evaluation (Sole-tenant Nodes)
./gcp-calculator-mcp service "Sole-tenant Nodes" '{"nodes": 2, "hours_per_month": 730, "region": "asia-northeast3", "commitment": "3-year"}'

# 4. BigQuery Data Warehouse Estimation
./gcp-calculator-mcp bigquery -query-tb 10 -storage-gb 500

# 5. Launch MCP Stdio Server
./gcp-calculator-mcp server
```

---

## 🛠 MCP Tools Specification

| Tool Name | Description |
| :--- | :--- |
| `calculate_compute_engine` | Calculate monthly cost for GCP Compute Engine VMs, GPUs, Cloud TPUs, CUD, Spot, and Disks. |
| `calculate_cloud_run` | Calculate monthly cost for GCP Cloud Run serverless applications including free tier allowances. |
| `calculate_storage` | Calculate monthly cost for GCP Cloud Storage tiers and network egress. |
| `calculate_gke` | Calculate monthly cost for Google Kubernetes Engine (Autopilot and Standard node pools). |
| `calculate_cloud_sql` | Calculate monthly cost for Cloud SQL instances (MySQL, PostgreSQL, SQL Server, High Availability). |
| `calculate_bigquery` | Calculate monthly cost for BigQuery active storage and on-demand query data scanned. |
| `calculate_gcp_service` | Universal evaluator dynamically querying the complete 115+ GCP service catalog. |
| `estimate_infrastructure` | Full infrastructure cost estimation and FinOps optimization recommendations. |

---

## 📄 License

This project is licensed under the [GNU Lesser General Public License v3.0 (LGPL-3.0)](LICENSE).

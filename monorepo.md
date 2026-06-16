ถ้าคุณจะทำ **Property AI Agent Platform** แบบ Enterprise จริง ผมแนะนำ **Monorepo + Microservices + Shared Packages** ตามโครงสร้างนี้

# Property AI Agent Platform Monorepo

## Repository

property-ai-agent-platform

---

# Directory Structure

```text
property-ai-agent-platform/

├── apps/
│
│   ├── agent-backend/
│   ├── admin-portal/
│   ├── customer-portal/
│   ├── mobile-api/
│   └── api-gateway/
│
├── services/
│
│   ├── property-service/
│   ├── inventory-service/
│   ├── crm-service/
│   ├── customer-service/
│   ├── lead-service/
│   ├── quotation-service/
│   ├── booking-service/
│   ├── contract-service/
│   ├── payment-service/
│   ├── community-service/
│   ├── maintenance-service/
│   ├── visitor-service/
│   ├── notification-service/
│   ├── analytics-service/
│   └── scoring-service/
│
├── agents/
│
│   ├── sales-agent/
│   ├── customer-service-agent/
│   ├── property-agent/
│   ├── payment-agent/
│   ├── community-agent/
│   └── executive-agent/
│
├── packages/
│
│   ├── shared-kernel/
│   ├── tool-sdk/
│   ├── mcp-sdk/
│   ├── event-sdk/
│   ├── auth-sdk/
│   ├── audit-sdk/
│   ├── logging-sdk/
│   ├── cache-sdk/
│   ├── database-sdk/
│   ├── kafka-sdk/
│   ├── telemetry-sdk/
│   ├── ai-sdk/
│   └── domain-events/
│
├── mcp/
│
│   ├── property-mcp-server/
│   ├── customer-mcp-server/
│   ├── payment-mcp-server/
│   ├── community-mcp-server/
│   └── analytics-mcp-server/
│
├── infrastructure/
│
│   ├── docker/
│   ├── kubernetes/
│   ├── helm/
│   ├── terraform/
│   ├── argocd/
│   └── monitoring/
│
├── databases/
│
│   ├── postgres/
│   ├── clickhouse/
│   ├── redis/
│   └── opensearch/
│
├── kafka/
│
│   ├── topics/
│   ├── schemas/
│   └── consumers/
│
├── docs/
│
│   ├── prd/
│   ├── architecture/
│   ├── openapi/
│   ├── kafka/
│   ├── mcp/
│   ├── adr/
│   └── runbooks/
│
├── scripts/
│
├── tests/
│
│   ├── integration/
│   ├── contract/
│   ├── performance/
│   └── e2e/
│
├── .github/
│
│   └── workflows/
│
├── turbo.json
├── pnpm-workspace.yaml
├── nx.json
├── package.json
└── README.md
```

---

# Agent Backend

```text
apps/agent-backend

src/

├── agents/
├── tools/
├── mcp/
├── application/
├── domain/
├── infrastructure/
├── presentation/
└── shared/
```

Responsibilities:

* OpenAI Tool Calling
* MCP Client
* Agent Runtime
* Tool Router
* Memory
* Audit
* Multi-Agent Orchestration

---

# Shared Packages

## tool-sdk

```text
packages/tool-sdk

ToolRegistry
ToolExecutor
ToolDefinition
ToolSchema
```

Used by:

* Agent Backend
* MCP Servers
* Agents

---

## event-sdk

```text
packages/event-sdk

KafkaProducer
KafkaConsumer
Saga
Outbox
```

---

## ai-sdk

```text
packages/ai-sdk

OpenAI Adapter
Claude Adapter
Gemini Adapter
Semantic Kernel Adapter
Microsoft Agent Framework Adapter
LangGraph Adapter
```

---

# Services

Each service follows:

```text
src/

├── application/
├── domain/
├── infrastructure/
├── presentation/
└── tests/
```

DDD + Clean Architecture

---

# Kafka Topics

```text
lead.created

lead.assigned

booking.created

booking.cancelled

contract.generated

payment.completed

maintenance.created

maintenance.closed

community.fee.overdue

visitor.registered
```

---

# Deployment

Development:

Docker Compose

Staging:

Kubernetes

Production:

Kubernetes + ArgoCD

---

# Build System

Recommended:

* PNPM Workspace
* Turborepo
* Nx

Commands:

pnpm install

pnpm dev

pnpm build

pnpm test

pnpm lint

```
```

### Stack ที่แนะนำ

สำหรับโปรเจกต์นี้

```text
Monorepo      : Turborepo
Package Mgmt : PNPM
Backend       : NestJS
Frontend      : React
Mobile        : React Native
Database      : PostgreSQL
Analytics     : ClickHouse
Cache         : Redis
Messaging     : Kafka
Search        : OpenSearch
Storage       : Cloudflare R2
AI            : OpenAI + MAF + MCP
Deployment    : Kubernetes + ArgoCD
```

โครงสร้างนี้รองรับทั้ง

* CRM
* Property Management
* Community Management
* CDP
* AI Agent
* MCP
* Multi-Tenant SaaS

และสามารถขยายจากทีม 5 คน ไปจนถึงหลายสิบทีมพัฒนาในองค์กรได้โดยไม่ต้องเปลี่ยน Repository Structure ใหม่ในอนาคต.

# PRD (Product Requirements Document)

## Enterprise AI Agent Backend Platform

### สำหรับธุรกิจอสังหาริมทรัพย์ (Property Management + CRM + CDP + Community + AI Agent)

---

# 1. Executive Summary

### Product Name

**Property AI Agent Platform**

### Vision

สร้าง AI Agent Platform กลางสำหรับธุรกิจอสังหาริมทรัพย์ ที่สามารถเชื่อมต่อทุกระบบงานในองค์กรผ่าน Tool Calling และ MCP เพื่อให้ AI ทำงานแทนพนักงานในด้าน

* Sales
* Customer Service
* Community Management
* Maintenance
* Executive Analytics
* Collections
* Contract Management

---

# 2. Business Goals

## เป้าหมายธุรกิจ

### ลดต้นทุน

* ลด Call Center 40%
* ลดงาน Manual Data Entry 70%
* ลดเวลาทำ Report 90%

### เพิ่มรายได้

* AI Lead Qualification
* AI Upsell/Cross Sell
* AI Property Recommendation

### เพิ่ม Productivity

* Sales Agent Assistant
* Customer Service Copilot
* Executive Copilot

---

# 3. Personas

## Sales

ความต้องการ

* ค้นหาบ้าน
* คำนวณผ่อน
* ออกใบเสนอราคา
* จองบ้าน

---

## Customer Service

ความต้องการ

* ตรวจสอบข้อมูลลูกค้า
* ตรวจสอบการชำระ
* รับเรื่องร้องเรียน

---

## Community Officer

ความต้องการ

* ค่าส่วนกลาง
* แจ้งซ่อม
* Visitor Management

---

## Executive

ความต้องการ

* KPI Dashboard
* Revenue Forecast
* Community Score

---

# 4. Scope

## Included

### CRM

* Lead
* Opportunity
* Customer 360

### Property

* Inventory
* Unit
* Project

### Sales

* Quotation
* Booking
* Contract

### Payment

* Collection
* Installment

### Community

* Common Fee
* Maintenance
* Visitor

### AI

* Tool Calling
* MCP
* Multi Agent

---

## Excluded

* Core Banking
* Accounting ERP
* HRM

---

# 5. High-Level Architecture

```text
Users
 │
 ├── Web
 ├── Mobile
 ├── Line OA
 ├── Teams
 └── WhatsApp

           │

           ▼

Enterprise AI Agent Platform

           │

 ┌─────────┼─────────┐

 ▼         ▼         ▼

OpenAI   Claude   Gemini

           │

           ▼

Agent Backend

           │

 ┌─────────┼─────────┐

 ▼         ▼         ▼

Tools     MCP      Memory

           │

           ▼

Microservices

           │

 ┌─────────┼─────────┐

 ▼         ▼         ▼

Postgres Redis Kafka
```

---

# 6. Functional Requirements

# FR-001 Property Search

User:

> หาบ้านเดี่ยวไม่เกิน 5 ล้าน

Tool:

```json
{
  "name":"search_property"
}
```

Output

```json
{
  "properties":[]
}
```

---

# FR-002 Property Detail

User:

> บ้าน A101 มีรายละเอียดอะไร

Tool

```json
{
  "name":"get_property_detail"
}
```

---

# FR-003 Lead Management

Tool

```json
{
  "name":"create_lead"
}
```

Features

* Create Lead
* Assign Sales
* Lead Score

---

# FR-004 Customer 360

Tool

```json
{
  "name":"get_customer"
}
```

ข้อมูล

* Profile
* Contracts
* Payment
* Community
* Maintenance

---

# FR-005 Mortgage Calculator

Tool

```json
{
  "name":"calculate_mortgage"
}
```

คำนวณ

* ดาวน์
* ดอกเบี้ย
* ค่างวด

---

# FR-006 Booking

Tool

```json
{
  "name":"create_booking"
}
```

Flow

```text
Check Availability
 ↓
Reserve Unit
 ↓
Generate Booking
 ↓
Publish Event
```

---

# FR-007 Contract

Tool

```json
{
  "name":"generate_contract"
}
```

---

# FR-008 Payment

Tool

```json
{
  "name":"check_payment"
}
```

---

# FR-009 Maintenance

Tool

```json
{
  "name":"create_maintenance_ticket"
}
```

---

# FR-010 Community Fee

Tool

```json
{
  "name":"get_community_fee"
}
```

---

# FR-011 Visitor Management

Tool

```json
{
  "name":"register_visitor"
}
```

---

# FR-012 Executive Dashboard

Tool

```json
{
  "name":"get_executive_dashboard"
}
```

Metrics

* Sales
* Revenue
* Occupancy
* Collection

---

# 7. AI Agent Design

## Sales Agent

Tools

```text
search_property
calculate_mortgage
create_booking
generate_contract
```

---

## Customer Service Agent

Tools

```text
get_customer
check_payment
create_ticket
```

---

## Community Agent

Tools

```text
get_community_fee
create_maintenance_ticket
register_visitor
```

---

## Executive Agent

Tools

```text
dashboard
forecast
analytics
```

---

# 8. Tool Registry

```text
search_property
get_property_detail
create_lead
update_lead
get_customer
calculate_mortgage
create_booking
cancel_booking
generate_contract
check_payment
record_payment
create_ticket
assign_ticket
get_community_fee
register_visitor
dashboard
forecast
```

ประมาณ 50-100 Tools

---

# 9. MCP Design

MCP Servers

```text
Property MCP

Customer MCP

Payment MCP

Community MCP

Analytics MCP
```

Discovery

```text
Agent
 ↓
MCP Client
 ↓
MCP Server
 ↓
Tools
```

---

# 10. Event-Driven Architecture

Kafka Topics

```text
lead.created

lead.assigned

booking.created

booking.cancelled

contract.generated

payment.completed

maintenance.created

maintenance.closed

visitor.registered

community.fee.overdue
```

---

# 11. Microservices

```text
Property Service

Inventory Service

Customer Service

Lead Service

Booking Service

Contract Service

Payment Service

Community Service

Maintenance Service

Notification Service

Analytics Service
```

---

# 12. Database Design

## PostgreSQL

Schemas

```text
customer

property

inventory

lead

booking

contract

payment

community_fee

maintenance

visitor
```

---

# Redis

ใช้

```text
Cache

Session

Rate Limit

Tool Cache
```

---

# Kafka

ใช้

```text
Event Streaming

Saga

Audit
```

---

# 13. Security

Authentication

```text
JWT

OAuth2

Azure AD
```

Authorization

```text
RBAC

ABAC
```

Roles

```text
Admin

Sales

Customer Service

Community Officer

Executive
```

---

# 14. Audit

ต้องเก็บ

```text
Prompt

Tool Call

Response

User

Timestamp

Correlation ID
```

---

# 15. Observability

OpenTelemetry

Metrics

```text
Tool Latency

LLM Latency

Token Usage

Error Rate

Kafka Lag
```

---

# 16. Non Functional Requirements

Availability

```text
99.9%
```

Response Time

```text
Tool < 2 sec

Agent < 5 sec
```

Scalability

```text
1,000,000 Customers

100,000 Properties

10,000 Concurrent Users
```

---

# 17. Deployment

## Kubernetes

Components

```text
agent-backend

tool-registry

mcp-client

postgresql

redis

kafka

prometheus

grafana

jaeger
```

---

# 18. Technology Stack

Backend

```text
NestJS
TypeScript
```

AI

```text
OpenAI
Microsoft Agent Framework
Semantic Kernel
LangGraph
MCP
```

Database

```text
PostgreSQL
Redis
```

Messaging

```text
Kafka
```

Storage

```text
MinIO / Cloudflare R2
```

Search

```text
OpenSearch
```

Deployment

```text
Docker
Kubernetes
ArgoCD
GitHub Actions
```

---

# 19. Roadmap

### Phase 1

* Property
* CRM
* Booking
* Payment
* Tool Calling

### Phase 2

* Community
* Maintenance
* Visitor

### Phase 3

* MCP
* Multi-Agent
* AI Scoring
* Executive Copilot

### Phase 4

* Predictive Analytics
* Autonomous Agent
* AI Revenue Optimization

---

# Deliverables

* PRD
* System Architecture Document
* Microservice Specification
* OpenAPI Specification
* Tool Catalog
* MCP Specification
* Kafka Event Catalog
* PostgreSQL Schema Design
* AI Agent Design
* Security Architecture
* Deployment Architecture
* Runbook & SOP

เอกสารนี้สามารถใช้เป็น Master PRD สำหรับเริ่มออกแบบ Solution Architecture, OpenAPI, Database, Kafka Topics และเริ่มพัฒนา Agent Backend ระดับ Enterprise ได้ทันทีครับ।

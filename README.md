![Your Image](https://drive.google.com/uc?export=view&id=1bQbsGnsEQhjvxv8HuHHw0VWiW0wfuhzu)

# 99x AI Hub Documentation

Welcome to the **99x AI Hub Documentation!** This repository provides end-to-end guidance on using and managing the 99x AI Hub, a centralized platform designed to make AI management simple, efficient, and powerful across organizations.

---

## 📖 About AI Hub

**99x AI Hub** is the central management and observability platform for AI agents within 99x. It enables developers and teams to:

- Register and govern AI agents.
- Monitor performance in real-time.
- Manage organizational access with a unified dashboard.

With a well-structured architecture and robust features, AI Hub ensures seamless integration, scalability, and security for all users.

---

## 📂 Table of Contents

- [Overview](#overview)
- [Architecture](#architecture)
- [Tech Stack](#tech-stack)
- [Features](#features-and-scope)
- [Metrics & Observability](#metrics-and-kpis)
- [Quick Start Guide](#quick-start-guide)
- [Integration](#integration)
- [Dashboard Guide](#dashboard-guide)
- [Best Practices](#best-practices)
- [FAQ](#faq)

---

## 🌟 Overview <a id="overview"></a>

The **99x AI Hub** provides a fully customizable platform to manage your AI agents. It is equipped with:

- A modern dashboard built with **React/Next.js** for visualization.
- A high-performance backend powered by **ASP.NET Core 8.0**.
- Integrated **PostgreSQL** for relational data and robust identity management via **Microsoft Entra ID**.

---

## 🏗️ Architecture <a id="architecture"></a>

### System Design

AI Hub’s architecture ensures scalability and performance through clear layer separation:

- **Frontend:** Built with React/Next.js + Tailwind.
- **Backend:** ASP.NET Core 8.0 API Gateway handling all business logic.
- **Database:** Supports relational data via PostgreSQL.
- **Identity Management:** Multi-tenant trust with Microsoft Entra ID.

### Core Data Models

- **Users:** Managed via Office 365/Entra ID with hierarchical multi-tenant support.
- **Agents:** Each agent instance is associated with a team.
- **Teams:** Supports parent-child relationships.
- **Roles:** Fine-grained RBAC (Admins, Users).

---

## ⚙️ Tech Stack <a id="tech-stack"></a>

| Component       | Technology      | Azure Service              |
|------------------|-----------------|----------------------------|
| Frontend        | Next.js/Tailwind| Azure Static Web Apps      |
| Backend         | .NET Core 8.0   | Azure App Service (B1)     |
| Database        | PostgreSQL      | Azure Database for PostgreSQL |
| Authentication  | Microsoft Entra | Azure Key Vault (OIDC)     |

The platform is **cloud-native**, with deployment infrastructure managed via **Azure DevOps** and IaC templates.

---

## 🌍 Features <a id="features-and-scope"></a>

- **Agent Management:** Full CRUD operations, live status updates, detailed tagging, and role assignments.
- **Team Governance:** Invite and manage members, roles, and organization hierarchies effortlessly.
- **Advanced Security:** Role-based access control (RBAC) and strict tenant isolation via **Auth:AllowedTenantIds**.
- **Integration Flexibility:** Universal HTTP-based APIs compatible with Python, Node.js, C#, and no-code platforms like Zapier.

---

## 📊 Metrics and KPIs <a id="metrics-and-kpis"></a>

### Observability Metrics:

| Category     | Key Metrics                          |
|--------------|--------------------------------------|
| **Performance** | Execution time, throughput, latency  |
| **Accuracy**    | Success rates, error classifications |
| **Resources**   | Token usage, cost-per-task         |

#### Supported AI Models:
- GPT4, Claude3, Gemini, Llama3, Mistral.

---

## 🚀 Quick Start Guide <a id="quick-start-guide"></a>

### 1. Prerequisites

- Platform requires **Entra ID authentication**. All API calls require a Bearer token.
- **Production Dashboard:** [AI Hub Dashboard](https://staihub.z16.web.core.windows.net)

### 2. Register Your Agent
Use the following command to register an agent:

```bash
curl -X POST http://localhost:5000/agents \
  -H "Authorization: Bearer YOUR_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "name": "Support Bot",
    "category": "CustomerService",
    "model": "GPT4"
  }'
```

### 3. Push Metrics (Bulk Example)
Batch-pushing data ensures efficiency:

```bash
curl -X POST http://localhost:5000/agents/{id}/metrics/bulk \
  -H "X-Api-Key: sk-abcd1234" \
  -d '[
    {"name": "response_time", "value": 1.2, "unit": "seconds"},
    {"name": "tokens_used", "value": 150, "unit": "count"}
  ]'
```

---

## 🤝 Integration <a id="integration"></a>

The platform offers universal HTTP-based APIs, ensuring compatibility with any system capable of making HTTP requests.

### SDK Examples

#### JavaScript (Node.js)
```javascript
// Example Node.js push metric
const pushMetric = async (name, value) => {
    await fetch(`https://api.aihub.99x.io/agents/${AGENT_ID}/metrics`, {
        method: 'POST',
        headers: {
            'X-Api-Key': 'YOUR_API_KEY',
            'Content-Type': 'application/json'
        },
        body: JSON.stringify({ name, value, unit: 'seconds' })
    });
};
```

#### Python
```python
# Example Python push metric
import requests

def report_usage(tokens):
    requests.post(
        f"https://api.aihub.99x.io/agents/{AGENT_ID}/metrics",
        headers={"X-Api-Key": "YOUR_API_KEY"},
        json={"name": "token_usage", "value": tokens, "unit": "count"}
    )
```

---

## 🌟 Dashboard Guide <a id="dashboard-guide"></a>

The **AI Hub Dashboard** allows intuitive monitoring and analysis:

### Key Views:
- **Global Insights:** Organization-wide stats (active agents, token spend, and success rates).
- **Team Analysis:** Compare performance metrics across teams.
- **Agent Drill-down:** Investigate specific agent performance and historical trends.

---

## ✅ Best Practices <a id="best-practices"></a>

- **Optimize Frequency:** Reduce API flooding. Use bulk metric uploads every 5 minutes.
- **Error Reporting:** Classify errors (e.g., `RateLimit`, `SafetyGuardrail`).
- **Security First:** Rotate API keys every 90 days.
- **Version Control:** Use dimensions to track major model changes (e.g., GPT-4 to GPT-5).

---

## 🙋 FAQ <a id="faq"></a>

- **How does authentication work?**
  All access is secured via Entra ID for users and a unique `X-Api-Key` for agents.

- **Is participation mandatory?**
  No, but it’s highly recommended for efficient AI management.

---

## 🔗 Useful Links

- [AI Hub Dashboard](https://staihub.z16.web.core.windows.net)
- [Contributing Guide](CONTRIBUTING.md)

---

Let me know if you'd like me to customize it further! 🌟

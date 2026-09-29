<div align="center">

# 🐵 MonkeysCloud

### Modern tools for teams who ship fast.

A high-performance **PHP 8.4 framework** and an **agentic AI IDE**, built by the same team, designed to work together.

[![MonkeysLegion](https://img.shields.io/badge/MonkeysLegion-v2-4F46E5?style=for-the-badge)](https://monkeyslegion.com)
[![MonkeysCode](https://img.shields.io/badge/MonkeysCode-AI_IDE-F59E0B?style=for-the-badge)](https://monkeyscode.com)
[![PHP](https://img.shields.io/badge/PHP-8.4+-777BB4?style=for-the-badge&logo=php&logoColor=white)](https://php.net)
[![License](https://img.shields.io/badge/License-MIT-22C55E?style=for-the-badge)](https://github.com/MonkeysCloud/MonkeysLegion-Skeleton/blob/main/LICENSE)

[**MonkeysLegion**](#-monkeyslegion--php-84-framework) · [**MonkeysCode**](#-monkeyscode--the-agentic-ide) · [**Packages**](#-the-monkeyslegion-ecosystem) · [**Quick start**](#-quick-start) · [**Contributing**](#-contributing)

</div>

---

## 🦍 MonkeysLegion — PHP 8.4 Framework

> **Attribute-first. Zero magic. Production-ready.**
> A modular PHP 8.4 framework built on property hooks, asymmetric visibility, a compiled DI container, and a strict PSR-15 pipeline. It takes you from `composer create-project` to production without the boilerplate.

```bash
composer create-project monkeyscloud/monkeyslegion-skeleton my-app
cd my-app && composer serve   # → http://127.0.0.1:8000
```

<table>
<tr>
<td width="50%" valign="top">

#### ⚡ Built on modern PHP
- **PHP 8.4 property hooks** and `public private(set)` asymmetric visibility, with no getters or setters
- **Attribute-first**: `#[Route]`, `#[Entity]`, `#[Singleton]`, `#[Listener]`, `#[Authenticated]`
- **Compiled PSR-11 container** with auto-wiring
- **`.mlc` typed configuration** instead of PHP arrays
- **PHPStan level 9** and PSR-12 across the board

</td>
<td width="50%" valign="top">

#### 🧰 Batteries included
- **Auth**: JWT, RBAC/ABAC, OAuth socialite, 2FA, API keys, **passkeys / WebAuthn**
- **Data**: micro-ORM, query builder, entity-diff migrations, factories, read/write splitting
- **APIs**: live **OpenAPI 3.1** + Swagger UI, JSON:API resources, **GraphQL**, pagination
- **Frontend**: **Inertia.js** (React/Vue + SSR), **Vite**, MLView templates, **Live** reactive components
- **Async**: queues, batching, scheduling, WebSockets, webhooks, notifications

</td>
</tr>
<tr>
<td width="50%" valign="top">

#### 🤖 AI-native
- **Apex**: multi-model AI orchestration with pipelines, guardrails, structured output, and agents
- **MCP server and client**: expose your app as tools to any AI agent
- **Poly-Syntax**: JSON/XML/YAML/TOML/CSV conversion tuned to save tokens in LLM and RAG context
- **Search**: Meilisearch, Typesense, OpenSearch, Elasticsearch, and Solr, with hybrid BM25 + vector

</td>
<td width="50%" valign="top">

#### 🏢 Enterprise-ready
- **Multi-tenancy**: single-DB, schema-per-tenant, or DB-per-tenant
- **Feature flags**: percentage rollouts and A/B tests
- **Observability**: OpenTelemetry, Prometheus/StatsD, tracing, DevTools profiler
- **Security**: CSP, rate limiting (token bucket + sliding window), AES-GCM/XChaCha20 encryption with key rotation
- **Ops**: Docker stack, DB backups to S3/GCS, SSH/SFTP, Stripe

</td>
</tr>
</table>

### ✍️ What v2 looks like

```php
#[RoutePrefix('/api/v2/users')]
#[Middleware(['cors', 'throttle:60,1'])]
#[Authenticated]
final class UserController
{
    public function __construct(
        private readonly UserService $service,
        private readonly UserRepository $users,
    ) {}

    #[Route('GET', '/{id:\d+}', name: 'users.show', tags: ['Users'])]   // → auto OpenAPI 3.1
    public function show(ServerRequestInterface $request, string $id): Response
    {
        return UserResource::make($this->users->findOrFail((int) $id));
    }

    #[Route('POST', '/', name: 'users.create', tags: ['Users'])]
    #[RequiresRole('admin')]
    public function create(CreateUserRequest $dto): Response   // validated DTO binding
    {
        return UserResource::make($this->service->createUser($dto), 201);
    }
}

#[Entity(table: 'users')]
#[Timestamps]
class User
{
    #[Id]
    #[Field(type: 'unsignedBigInt', autoIncrement: true)]
    public private(set) int $id;                 // asymmetric visibility

    #[Field(type: 'string', length: 255)]
    public string $email {
        set(string $value) {                     // PHP 8.4 property hook
            $this->email = strtolower(trim($value));
        }
    }
}
```

### 🚀 Performance

<table>
<tr>
<td valign="top">

| HTTP throughput *(estimated)* | req/sec |
|---|---:|
| **MonkeysLegion v2** | **~12,500** |
| Slim 4 + PSR-15 | ~8,200 |
| Symfony 7.2 | ~4,800 |
| Laravel 12 | ~2,100 |

</td>
<td valign="top">

| Micro-benchmark | Ops/sec |
|---|---:|
| DTO construction | **10.9M** |
| Property hooks | **11.1M** |
| Entity creation | **6.3M** |
| Peak memory | **4 MB** |

</td>
</tr>
</table>

<sub>PHP 8.5 on Apple Silicon. Reproduce with `php tests/Performance/benchmark_detailed.php` in the skeleton.</sub>

📦 [**Skeleton**](https://github.com/MonkeysCloud/MonkeysLegion-Skeleton) · 🧱 [**Framework**](https://github.com/MonkeysCloud/MonkeysLegion) · 🌐 [**monkeyslegion.com**](https://monkeyslegion.com) · 📖 [**Docs**](https://monkeyslegion.com/docs)

---

## 🧠 MonkeysCode — The Agentic IDE

> **The AI IDE with Capuchin built in. Frontier models included.**
> The agentic IDE, and the agent that works without it.

MonkeysCode is an AI-first code editor and desktop agent powered by **Capuchin**, our own model, with **Claude, Gemini, and ChatGPT** included in the subscription. You can run it fully local, bring your own key, or use our models.

<table>
<tr>
<td width="33%" valign="top">

#### 🐒 Capuchin AI
- **Capuchin Flash** for instant edits
- **Capuchin Reason** for planning
- Serves **92.7%** of production requests
- Frontier models on a monthly allowance

</td>
<td width="33%" valign="top">

#### 🛠 Real agents
- **50+ agent tools**
- **4 execution environments**
- **Background and parallel agents**
- **Test-gated apply**: agents can't commit code that fails your tests

</td>
<td width="33%" valign="top">

#### 🔒 Private by design
- **On-device index** (Merkle-tracked, tree-sitter chunked)
- **Air-gapped mode** with local models and an internal registry
- **Signed event logs** that can be replayed and show tampering
- **Open core, no lock-in**

</td>
</tr>
</table>

| Product | What it is |
|---|---|
| 🖥 **MonkeysCode IDE** | Full agentic code editor for macOS, Windows, and Linux |
| 🤖 **Code Agent** | Standalone desktop app for running agents, included in every plan |
| ⌨️ **MonkeysCode CLI** | Headless agents for the terminal and CI |
| 🐹 **[Go SDK](https://github.com/MonkeysCloud/monkeyscode-go)** | Programmatic agent automation |

```bash
# MonkeysCode CLI (macOS / Linux)
curl -fsSL https://monkeyscode.com/cli/install.sh | bash
```

| **Free** | **Pro** | **Pro+** | **Ultra** | **Team** |
|:---:|:---:|:---:|:---:|:---:|
| $0 | $20/mo | $60/mo | $200/mo | $30/seat/mo |
| BYOK or local models | Unlimited Capuchin + $20 frontier allowance | $60 frontier allowance, priority queue | Unlimited Capuchin, $120 frontier allowance | Shared encrypted index, roles, central billing |

<sub>Every paid plan includes per-task budgets and a hard spend cap, so there are no surprise bills.</sub>

⬇️ [**Download**](https://monkeyscode.com/download) · 🌐 [**monkeyscode.com**](https://monkeyscode.com) · 📖 [**Docs**](https://monkeyscode.com/docs) · 🟢 [**Status**](https://status.monkeyscode.com)

---

## 📦 The MonkeysLegion Ecosystem

More than 50 standalone packages, each usable on its own or together through the [`monkeyslegion`](https://github.com/MonkeysCloud/MonkeysLegion) meta-package.

<details open>
<summary><b>🔧 Core & HTTP</b></summary>

| Package | Description |
|---|---|
| [Core](https://github.com/MonkeysCloud/MonkeysLegion-Core) | Framework kernel: typed config, service providers, pipeline |
| [Contracts](https://github.com/MonkeysCloud/MonkeysLegion-Contracts) | Interfaces and abstract bases with no framework coupling |
| [DI](https://github.com/MonkeysCloud/MonkeysLegion-Di) | PSR-11 container: auto-wiring, attributes, compiled container |
| [MLC](https://github.com/MonkeysCloud/MonkeysLegion-Mlc) | The `.mlc` typed configuration format |
| [Env](https://github.com/MonkeysCloud/MonkeysLegion-Env) | Environment variable management |
| [HTTP](https://github.com/MonkeysCloud/MonkeysLegion-Http) | PSR-7/PSR-15 messages, middleware, SAPI emitter |
| [Router](https://github.com/MonkeysCloud/MonkeysLegion-Router) | Attribute-driven router with compiled trie matching and model binding |
| [HTTP Client](https://github.com/MonkeysCloud/MonkeysLegion-HTTP-Client) | Fluent outbound client: pooling, retry/backoff, PSR-18, async |
| [Rate Limit](https://github.com/MonkeysCloud/MonkeysLegion-Rate-Limit) | Token bucket and sliding window, per route, user, and IP |
| [Session](https://github.com/MonkeysCloud/MonkeysLegion-Session) | Session management |

</details>

<details>
<summary><b>💾 Data & Persistence</b></summary>

| Package | Description |
|---|---|
| [Database](https://github.com/MonkeysCloud/MonkeysLegion-Database) | PDO connections, read/write splitting, pooling (MySQL, PostgreSQL, SQLite) |
| [Query](https://github.com/MonkeysCloud/MonkeysLegion-Query) | Performance-first query builder and micro-ORM |
| [Entity](https://github.com/MonkeysCloud/MonkeysLegion-Entity) | Attribute-based data mapper, scanner, and hydration |
| [Migration](https://github.com/MonkeysCloud/MonkeysLegion-Migration) | Entity-schema diff engine and dialect-aware DDL |
| [Cache](https://github.com/MonkeysCloud/MonkeysLegion-Cache) | Multi-driver cache, atomic locks, tiered caching |
| [Search](https://github.com/MonkeysCloud/MonkeysLegion-Search) | Multi-engine search with hybrid BM25 + vector |
| [Tenancy](https://github.com/MonkeysCloud/MonkeysLegion-Tenancy) | Single-DB, schema-per-tenant, and DB-per-tenant isolation |
| [Backup](https://github.com/MonkeysCloud/MonkeysLegion-Backup) | Database backup and restore to local disk, S3, or GCS |
| [Files](https://github.com/MonkeysCloud/MonkeysLegion-Files) | Storage, uploads, and image processing |

</details>

<details>
<summary><b>🌐 APIs & Serialization</b></summary>

| Package | Description |
|---|---|
| [OpenAPI](https://github.com/MonkeysCloud/MonkeysLegion-OpenApi) | Automatic OpenAPI 3.1 spec and Swagger UI |
| [GraphQL](https://github.com/MonkeysCloud/MonkeysLegion-GraphQL) | Code-first GraphQL server with DataLoader and subscriptions |
| [Resources](https://github.com/MonkeysCloud/MonkeysLegion-Resources) | API resources and transformers with JSON:API support |
| [Serializer](https://github.com/MonkeysCloud/MonkeysLegion-Serializer) | Attribute-driven object ↔ JSON/XML |
| [Pagination](https://github.com/MonkeysCloud/MonkeysLegion-Pagination) | Offset and cursor pagination, RFC 8288 Link headers |
| [Validation](https://github.com/MonkeysCloud/MonkeysLegion-Validation) | Attribute-driven validation and DTO binding |
| [Poly-Syntax](https://github.com/MonkeysCloud/MonkeysLegion-Poly-Syntax) | JSON/XML/YAML/TOML/CSV transforms tuned for LLM tokens |

</details>

<details>
<summary><b>🔐 Security & Auth</b></summary>

| Package | Description |
|---|---|
| [Auth](https://github.com/MonkeysCloud/MonkeysLegion-Auth) | Multi-guard, JWT, RBAC, OAuth, 2FA, API keys |
| [Permissions](https://github.com/MonkeysCloud/MonkeysLegion-Permissions) | Enterprise RBAC and ABAC engine |
| [WebAuthn](https://github.com/MonkeysCloud/MonkeysLegion-WebAuthn) | Passkeys / FIDO2 registration and assertion |
| [Encryption](https://github.com/MonkeysCloud/MonkeysLegion-Encryption) | AES-GCM, XChaCha20, envelope encryption, key rotation |

</details>

<details>
<summary><b>🎨 Frontend & Real-time</b></summary>

| Package | Description |
|---|---|
| [Template](https://github.com/MonkeysCloud/MonkeysLegion-Template) | MLView engine with components, slots, and caching |
| [Live](https://github.com/MonkeysCloud/MonkeysLegion-Live) | Server-driven reactive components built on [MonkeysJS](https://github.com/MonkeysCloud/MonkeysJS) |
| Inertia | Inertia.js adapter for React/Vue with SSR |
| Vite | Vite manifest, `@vite` directive, dev-mode detection |
| [Sockets](https://github.com/MonkeysCloud/MonkeysLegion-Sockets) | Cluster-ready WebSockets (Native, ReactPHP, Swoole), plus a [JS client](https://github.com/MonkeysCloud/MonkeysLegion-Sockets-Js) |
| [I18n](https://github.com/MonkeysCloud/MonkeysLegion-I18n) | Internationalization and localization |
| [Markdown](https://github.com/MonkeysCloud/monkeyslegion-markdown) | Pure-PHP CommonMark-style renderer |

</details>

<details>
<summary><b>⚙️ Async, Messaging & Integrations</b></summary>

| Package | Description |
|---|---|
| [Queue](https://github.com/MonkeysCloud/MonkeysLegion-Queue) | Multi-driver queues, batching, chaining, rate limiting |
| [Schedule](https://github.com/MonkeysCloud/MonkeysLegion-Schedule) | Cron-style task scheduling |
| [Events](https://github.com/MonkeysCloud/MonkeysLegion-Events) | PSR-14 dispatcher, attribute listeners, event sourcing |
| [Mail](https://github.com/MonkeysCloud/MonkeysLegion-Mail) | SMTP, Markdown templates, DKIM |
| [Notifications](https://github.com/MonkeysCloud/MonkeysLegion-Notifications) | Database, Mail, Slack, Teams, and Webhook channels |
| [Webhooks](https://github.com/MonkeysCloud/monkeyslegion-webhooks) | Outgoing and incoming webhooks with HMAC signing and retries |
| [Feature Flags](https://github.com/MonkeysCloud/monkeyslegion-feature-flags) | Boolean flags, percentage rollouts, A/B testing |
| [Stripe](https://github.com/MonkeysCloud/MonkeysLegion-Stripe) | First-class Stripe integration |
| [Process](https://github.com/MonkeysCloud/MonkeysLegion-Process) | Async subprocesses, pools, pipelines, signals |
| [SSH](https://github.com/MonkeysCloud/MonkeysLegion-SSH) | SSH, SFTP, and SCP with a fluent API |

</details>

<details>
<summary><b>🤖 AI</b></summary>

| Package | Description |
|---|---|
| [Apex](https://github.com/MonkeysCloud/MonkeysLegion-Apex) | AI orchestration: multi-model routing, pipelines, guardrails, agents |
| [MCP](https://github.com/MonkeysCloud/MonkeysLegion-MCP) | Model Context Protocol server and client over stdio and Streamable HTTP |

</details>

<details>
<summary><b>🛠 Developer Experience & Ops</b></summary>

| Package | Description |
|---|---|
| [CLI](https://github.com/MonkeysCloud/MonkeysLegion-Cli) | Code generation, migrations, Tinker-style REPL |
| [Dev Server](https://github.com/MonkeysCloud/MonkeysLegion-Dev-Server) | Hot-reload development server |
| [DevTools](https://github.com/MonkeysCloud/MonkeysLegion-DevTools) | Debugging, profiling, and diagnostics |
| [Telemetry](https://github.com/MonkeysCloud/MonkeysLegion-Telemetry) | PSR-3 logging, Prometheus/StatsD metrics, distributed tracing |
| [Logger](https://github.com/MonkeysCloud/MonkeysLegion-Logger) | PSR-3 structured logger with no dependencies |
| Testing | HTTP testing DSL, database traits, fakes, snapshots |
| [Docker](https://github.com/MonkeysCloud/MonkeysLegion-Docker) | Docker stack from development to production |

</details>

---

## ⚡ Quick Start

```bash
# 1. Create a project
composer create-project monkeyscloud/monkeyslegion-skeleton my-app
cd my-app

# 2. Configure
cp .env.example .env
php ml key:generate

# 3. Run
composer serve            # → http://127.0.0.1:8000

# 4. Verify (PSR-12 + PHPStan level 9 + tests)
composer check
```

**Requirements:** PHP 8.4+, Composer 2.x, and MySQL 8.4 / PostgreSQL / SQLite.

---

## 🏗 How It Fits Together

```
┌──────────────────────────────────────────────────────────────────┐
│  MonkeysCode  ·  Capuchin AI  ·  IDE  ·  Code Agent  ·  CLI      │
│                ↓ builds, tests and ships ↓                       │
├──────────────────────────────────────────────────────────────────┤
│  Your App  (Skeleton · Inertia/React/Vue · MLView · Live)        │
├──────────────────────────────────────────────────────────────────┤
│  MonkeysLegion v2                                                │
│  Router · DI · Entity/Query · Auth · Queue · OpenAPI · GraphQL   │
│  Apex AI · MCP · Search · Tenancy · Telemetry · Sockets · …      │
├──────────────────────────────────────────────────────────────────┤
│  PHP 8.4+  ·  PSR-3 / 7 / 11 / 14 / 15 / 18                      │
└──────────────────────────────────────────────────────────────────┘
```

---

## 🤝 Contributing

We welcome bug reports, documentation fixes, and new packages.

- 🐛 [Report an issue](https://github.com/MonkeysCloud/MonkeysLegion-Skeleton/issues)
- 💡 [Request a feature](https://github.com/MonkeysCloud/MonkeysLegion-Skeleton/issues)
- 📖 [Read the docs](https://monkeyslegion.com/docs)

> [!IMPORTANT]
> **All MonkeysLegion v2 contributions must follow the [Code Standards & Conventions](./monkeyslegion_v2_code_standards.md).**
>
> - PHP 8.4+ with `declare(strict_types=1)` in every file
> - Property hooks instead of getters and setters
> - Attribute-first architecture with no magic strings
> - PHPStan level 9 and PSR-12 compliance
> - 100% type safety
>
> Using an AI coding agent? Point it to [`AGENTS.md`](https://github.com/MonkeysCloud/MonkeysLegion-Skeleton/blob/main/AGENTS.md).

---

## 📬 Contact

**General:** [info@monkeyslegion.com](mailto:info@monkeyslegion.com) · **Press:** [press@monkeyslegion.com](mailto:press@monkeyslegion.com)

<div align="center">

<br>

**Built with ❤️ by the MonkeysCloud team**

*Structure without complexity.*

[![GitHub](https://img.shields.io/badge/GitHub-MonkeysCloud-181717?style=flat-square&logo=github)](https://github.com/MonkeysCloud)
[![X](https://img.shields.io/badge/X-@MonkeysLegion-000000?style=flat-square&logo=x)](https://twitter.com/MonkeysLegion)
[![MonkeysLegion](https://img.shields.io/badge/web-monkeyslegion.com-4F46E5?style=flat-square)](https://monkeyslegion.com)
[![MonkeysCode](https://img.shields.io/badge/web-monkeyscode.com-F59E0B?style=flat-square)](https://monkeyscode.com)
[![monkeys.cloud](https://img.shields.io/badge/web-monkeys.cloud-0EA5E9?style=flat-square)](https://monkeys.cloud)

</div>

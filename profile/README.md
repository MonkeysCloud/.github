<div align="center">

# 🐵 MonkeysCloud

**Modern PHP Ecosystem for Teams Who Ship Fast**

[![MonkeysLegion](https://img.shields.io/badge/MonkeysLegion-Framework-blue?style=for-the-badge)](https://monkeyslegion.com)
[![MonkeysCMS](https://img.shields.io/badge/MonkeysCMS-CMS-green?style=for-the-badge)](https://monkeyscms.com)
[![License](https://img.shields.io/badge/License-MIT-yellow?style=for-the-badge)](LICENSE)
[![PHP](https://img.shields.io/badge/PHP-8.2+-777BB4?style=for-the-badge&logo=php&logoColor=white)](https://php.net)

*Ship production-ready PHP applications in record time.*

[MonkeysLegion](https://monkeyslegion.com) • [MonkeysCMS](https://monkeyscms.com) • [Documentation](https://monkeyslegion.com/docs) • [Get Started](#quick-start)

</div>

---

## 🚀 Our Projects

### MonkeysLegion — PHP Framework

> The lightweight, modular framework that lets modern teams move from commit to cloud without the boilerplate.

```bash
composer create-project "monkeyscloud/monkeyslegion-skeleton"
```

**What you get out of the box:**

- ⚡ **Blazing-fast router** — High-performance routing with minimal overhead
- 🧩 **Rock-solid DI container** — Clean dependency injection for testable code
- 🛠️ **First-class CLI** — Powerful command-line tools for scaffolding and automation
- 🐳 **Zero-config Docker stack** — Development to production without configuration headaches
- 🧪 **Testing ready** — Wired for testing, observability, and scale on day one

📦 [View MonkeysLegion Skeleton](https://github.com/MonkeysCloud/MonkeysLegion-Skeleton) | 🌐 [monkeyslegion.com](https://monkeyslegion.com)

---

### MonkeysCMS — Content Management System

> Drupal-grade structure, WordPress-simple editing, code-first developer experience.

**The CMS tradeoff is outdated.** MonkeysCMS combines the best of both worlds:

| Feature | WordPress | Drupal | MonkeysCMS |
|---------|-----------|--------|------------|
| Learning Curve | ✅ Easy | ❌ Steep | ✅ Easy |
| Content Structure | ❌ Fragile | ✅ Powerful | ✅ Powerful |
| Code-First | ❌ Click-heavy | ⚠️ Config-heavy | ✅ Native |
| Long-term Maintenance | ❌ Plugin chaos | ⚠️ Complex | ✅ Clean |

**Core Features:**

- 📝 **Content Types & Fields** — Define data models for pages, posts, products, and more
- 🔗 **Real Relationships** — Explicit relations, not meta-table hacks
- 🏷️ **Taxonomy System** — Categories, tags, hierarchies, classification
- 🧱 **Blocks & Regions** — Reusable components with predictable layouts
- 🔐 **RBAC Permissions** — Granular roles and security
- 🔌 **Admin REST API** — Build headless or hybrid applications
- 📦 **Modular Architecture** — Install only what you need

📦 [View MonkeysCMS](https://github.com/MonkeysCloud/MonkeysCMS) | 🌐 [monkeyscms.com](https://monkeyscms.com)

---

## 📦 Ecosystem Packages

| Package | Description | Status |
|---------|-------------|--------|
| [monkeyslegion-skeleton](https://github.com/MonkeysCloud/MonkeysLegion-Skeleton) | Base skeleton for rapid application development | ✅ Stable |
| [monkeyslegion-router](https://github.com/MonkeysCloud/monkeyslegion-router) | High-performance PSR-7 router | ✅ Stable |
| [monkeyslegion-container](https://github.com/MonkeysCloud/monkeyslegion-container) | Lightweight DI container | ✅ Stable |
| [monkeyslegion-cli](https://github.com/MonkeysCloud/monkeyslegion-cli) | Command-line tools and scaffolding | ✅ Stable |
| [monkeyslegion-db](https://github.com/MonkeysCloud/monkeyslegion-db) | Database abstraction and ORM | ✅ Stable |
| [monkeyslegion-auth](https://github.com/MonkeysCloud/monkeyslegion-auth) | Authentication and authorization | ✅ Stable |
| [monkeyslegion-cache](https://github.com/MonkeysCloud/monkeyslegion-cache) | PSR-6/16 caching layer | ✅ Stable |
| [monkeyslegion-i18n](https://github.com/MonkeysCloud/monkeyslegion-i18n) | Internationalization support | ✅ Stable |
| [monkeyslegion-files](https://github.com/MonkeysCloud/monkeyslegion-files) | File uploads & storage (Local/S3/GCS) | ✅ Stable |
| [MonkeysCMS](https://github.com/MonkeysCloud/MonkeysCMS) | Full-featured CMS | 🚧 Beta |

---

## ⚡ Quick Start

### Start a new MonkeysLegion project

```bash
# Create new project
composer create-project "monkeyscloud/monkeyslegion-skeleton" my-app

# Navigate to project
cd my-app

# Start development server
php monkeys serve
```

### Start with MonkeysCMS

```bash
# Clone MonkeysCMS
git clone https://github.com/MonkeysCloud/MonkeysCMS.git

# Install dependencies
cd MonkeysCMS && composer install

# Configure and run
cp .env.example .env
php monkeys serve
```

---

## 🏗️ Architecture

```
┌─────────────────────────────────────────────────────────┐
│                     MonkeysCMS                          │
│        (Content Types • Blocks • Themes • API)         │
├─────────────────────────────────────────────────────────┤
│                   MonkeysLegion                         │
│    (Router • DI • CLI • ORM • Auth • Cache • i18n)     │
├─────────────────────────────────────────────────────────┤
│                      PHP 8.2+                           │
└─────────────────────────────────────────────────────────┘
```

---

## 🎯 Perfect For

- **Marketing sites** — Landing pages, product pages, case studies, docs
- **Documentation** — Knowledge bases with taxonomies and versioning
- **Multi-site agencies** — Reusable modules, consistent architecture
- **Hybrid web apps** — CMS-managed content + app-driven features
- **API-first projects** — Headless delivery to Next.js, mobile, dashboards

---

## 🤝 Contributing

We welcome contributions! Whether you're fixing bugs, improving documentation, or building new modules and themes—your contributions shape the platform.

- 🐛 [Report Issues](https://github.com/MonkeysCloud/MonkeysCMS/issues)
- 💡 [Feature Requests](https://github.com/MonkeysCloud/MonkeysCMS/issues)
- 📖 [Documentation](https://monkeyslegion.com/docs)
- 🗺️ [View Roadmap](https://github.com/MonkeysCloud/MonkeysCMS/issues)

---

## 📬 Contact

- **General:** [info@monkeyslegion.com](mailto:info@monkeyslegion.com)
- **Press:** [press@monkeyslegion.com](mailto:press@monkeyslegion.com)

---

<div align="center">

**Built with ❤️ by the MonkeysCloud Team**

*Structure without complexity.*

[![GitHub](https://img.shields.io/badge/GitHub-MonkeysCloud-181717?style=flat-square&logo=github)](https://github.com/MonkeysCloud)
[![Twitter](https://img.shields.io/badge/Twitter-@MonkeysLegion-1DA1F2?style=flat-square&logo=twitter)](https://twitter.com/MonkeysLegion)

</div>

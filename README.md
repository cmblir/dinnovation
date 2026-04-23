<div align="center">

# 🚀 Dinnovation

### Digital Industry Innovation Data Platform

**One unified pipeline for collecting, processing, and loading market data — at scale.**

[![Python](https://img.shields.io/badge/python-3.9+-blue.svg?style=flat-square&logo=python&logoColor=white)](https://pypi.python.org/pypi/dinnovation)
[![PyPI](https://img.shields.io/pypi/v/dinnovation.svg?style=flat-square&color=blue)](https://pypi.python.org/pypi/dinnovation)
[![Status](https://img.shields.io/pypi/status/dinnovation.svg?style=flat-square)](https://pypi.python.org/pypi/dinnovation)
[![License](https://img.shields.io/badge/license-Apache%202.0-green.svg?style=flat-square)](LICENSE)
[![Stars](https://img.shields.io/github/stars/cmblir/dinnovation?style=flat-square&color=yellow)](https://github.com/cmblir/dinnovation/stargazers)

[**Quick Start**](#-quick-start) • [**Features**](#-why-dinnovation) • [**Architecture**](#-architecture) • [**Docs**](./quick_start/README.md) • [**Contributing**](#-contributing)

</div>

---

## 🤔 The Problem

Building data pipelines from scratch is painful. You write a crawler for every site, bolt on a scheduler, then handle DB loading — and end up spending more than half your time on infrastructure instead of insights.

## 💡 The Solution

**Dinnovation unifies the entire collect → process → load workflow behind a single API.** Originally built to power a Big Data Center's daily operations, it ships with a built-in scheduler and a GitHub Actions release pipeline out of the box.

---

## ✨ Why Dinnovation?

<table>
<tr>
<td width="25%" align="center"><b>🌐 Multi-Source</b></td>
<td width="25%" align="center"><b>⚡ Auto Pipeline</b></td>
<td width="25%" align="center"><b>📦 Plug & Play</b></td>
<td width="25%" align="center"><b>🔄 CI/CD Ready</b></td>
</tr>
<tr>
<td>Pull from multiple financial and corporate data sites through one consistent interface</td>
<td>Schedule end-to-end ETL jobs without cron or external orchestrators</td>
<td>One <code>pip install</code> and you're shipping data straight to your warehouse</td>
<td>Push code → bump version → publish to PyPI & GitHub Releases automatically</td>
</tr>
</table>

---

## 📦 Installation

```bash
pip install dinnovation
```

<details>
<summary><b>Install from source</b></summary>

```bash
git clone https://github.com/cmblir/dinnovation.git
cd dinnovation
pip install -r requirements.txt
# or
python setup.py install
```
</details>

<details>
<summary><b>📋 Full dependency list</b></summary>

| Library | Version |
|---|---|
| pandas | 1.5.3 |
| numpy | 1.24.2 |
| tqdm | 4.64.1 |
| OpenDartReader | 0.2.1 |
| beautifulsoup4 | 4.11.2 |
| urllib3 | 1.26.14 |
| selenium | 4.8.2 |
| webdriver_manager | 3.8.5 |
| chromedriver_autoinstaller | 0.4.0 |
| psycopg2 | 2.9.5 |
| sqlalchemy | 2.0.4 |
| cryptography | 41.0.3 |

**Required:** `Python >= 3.9`

</details>

---

## 🚀 Quick Start

```python
from dinnovation import DataCollector

# Collect → process → load, in one chain
collector = DataCollector(source="dart")
collector.collect().process().load(db="postgres")
```

Read the full walkthrough in the [**Quick Start Guide →**](./quick_start/README.md)

---

## 🏗 Architecture

A single core module ingests from multiple sources, runs them through a processing layer, and emits to your database or files — no need to glue separate libraries together.

```mermaid
flowchart LR
    A[📊 Source Site A] --> M
    B[📈 Source Site B] --> M
    C[🏛 DART API] --> M
    D[🌐 Other Sources] --> M

    M[🧩 Dinnovation<br/>Core Module] --> P[⚙️ Process<br/>& Transform]

    P --> DB[(🗄 PostgreSQL)]
    P --> F[📁 File Export]

    style M fill:#4F46E5,stroke:#312E81,color:#fff,stroke-width:2px
    style P fill:#10B981,stroke:#047857,color:#fff,stroke-width:2px
    style DB fill:#F59E0B,stroke:#B45309,color:#fff
```

---

## 🔁 Auto Process

The built-in scheduler runs the entire ETL cycle for you — including retries and alerts on failure.

```mermaid
flowchart TD
    S([⏰ Scheduler Trigger]) --> C[📥 Collect Data]
    C --> P[🔄 Process & Clean]
    P --> L[📤 Load to Database]
    L --> N{✅ Success?}
    N -->|Yes| D([🎉 Pipeline Complete])
    N -->|No| R[🔁 Retry / Alert]
    R --> C

    style S fill:#8B5CF6,stroke:#5B21B6,color:#fff,stroke-width:2px
    style D fill:#10B981,stroke:#047857,color:#fff,stroke-width:2px
    style R fill:#EF4444,stroke:#991B1B,color:#fff
```

---

## ⚙️ Workflow

A single `git push` triggers version bump → package build → PyPI publish → GitHub Release.

```mermaid
flowchart LR
    Dev[👩‍💻 Code Change] --> Git[📤 git push]
    Git --> GA[⚡ GitHub Actions]
    GA --> V[🔢 Bump Version]
    V --> B[📦 Build Package]
    B --> PyPI[(📚 PyPI Release)]
    B --> GH[(🏷 GitHub Release)]

    style GA fill:#2088FF,stroke:#0366D6,color:#fff,stroke-width:2px
    style PyPI fill:#3775A9,stroke:#1F4E79,color:#fff
    style GH fill:#24292E,stroke:#000,color:#fff
```

---

## 📚 Documentation

| Resource | Description |
|---|---|
| 📖 [**Quick Start**](./quick_start/README.md) | Get your first pipeline running in 5 minutes |
| 🧪 **Examples** | See the `/examples` directory |
| 🛠 **API Reference** | *Coming soon* |

---

## 🗺 Roadmap

- [x] DART and major financial-site connectors
- [x] PostgreSQL loading support
- [x] Automated GitHub Actions release workflow
- [ ] BigQuery / Snowflake loading support
- [ ] CLI tool (`dinnovation run <pipeline>`)
- [ ] Web dashboard for monitoring

---

## 🤝 Contributing

Contributions are welcome — bug fixes, new data-source connectors, docs improvements, all of it.

```bash
# 1. Fork & clone
# 2. Create a feature branch
git checkout -b feature/amazing-feature

# 3. Commit your changes
git commit -m "feat: add amazing feature"

# 4. Push and open a PR
git push origin feature/amazing-feature
```

---

## ⚖️ License & Disclaimer

Released under the [**Apache 2.0 License**](LICENSE).

> ⚠️ **Important Legal Disclaimer**
>
> Dinnovation is **not affiliated with, endorsed by, or vetted by** any source sites. Use at your own risk and discretion. For information about your rights to use the actual data downloaded, refer to the **Terms of Use of each respective site**. Dinnovation is intended for **personal use only**.

---

<div align="center">

### ⭐ If Dinnovation saves you time, please consider giving it a star!

Made with ❤️ by [**@cmblir**](https://github.com/cmblir)

</div>

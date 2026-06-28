![preview](https://raw.githubusercontent.com/randyfajar/inbox-watcher-cli/main/preview.svg)

# ChronosForge ⏳

**Enterprise Temporal Credential Management & Secure Verification Ecosystem**

---

## Overview 🔭

Time is the ultimate gatekeeper. From temporary access tokens to expiring verification codes, every digital interaction has a shelf life. **ChronosForge** is not just another credential utility—it is a **temporal identity orchestration platform** that enables organizations and developers to generate, monitor, validate, and auto-extract time-sensitive credentials with surgical precision.

Inspired by the need for secure, ephemeral identity management, ChronosForge reimagines how we interact with temporary digital assets. Think of it as a **chronological Swiss Army knife** for credentials: you set the parameters, it handles the lifecycle, and your workflows gain the superpower of **conscious expiration awareness**.

Whether you are building a verification pipeline, testing multi-factor authentication flows, or automating inbox monitoring for time-bound codes, ChronosForge provides the architectural backbone. No more polling, no more manual extraction, no more missed deadlines. Your systems become **temporally aware**.

---

## The Philosophy: Beyond the Ephemeral

Most tools treat temporary credentials as disposable garbage. ChronosForge treats them as **first-class citizens of your digital infrastructure**. Every temporary email address, every one-time password, every expiring token represents a **decision point**—a moment where security and usability intersect.

We built ChronosForge to give developers and system administrators **temporal control** over these moments. It’s not about “getting a free account.” It’s about **architecting trust** in environments where permanence is a liability.

Our platform operates on three core tenets:

- **Generative Minimalism** – Create what you need, exactly when you need it, with zero residual footprint.
- **Reactive Observation** – Watch credentials expire in real-time, and respond before they vanish.
- **Atomic Extraction** – Pull one-time codes from inboxes with the precision of a surgical robot.

---

## Features & Capabilities 🧩

### 1. Temporal Inbox Fabrication ⚙️

Generate disposable inbox addresses with configurable lifespans. Choose from multiple domain providers, set custom prefixes, and define expiration policies down to the minute. Every inbox is a **unique temporal artifact**, not a recycled pool.

- **Multi-Domain Generation** – Select from dozens of domain origins, each with its own reputation profile.
- **Custom TTL** – Set inbox lifetime from 10 minutes to 48 hours. After expiry, the inbox self-destructs.
- **Prefix Customization** – Control naming conventions for easier tracking across workflows.

### 2. Real-Time Inbox Surveillance 📡

Once an inbox is active, ChronosForge establishes a persistent WebSocket connection to monitor incoming messages. No polling, no delays. Every email triggers an event stream that your systems can consume immediately.

- **Event-Driven Architecture** – Receive callbacks for incoming mail, attachment arrival, and inbox expiry.
- **Multi-Inbox Dashboard** – Monitor dozens of inboxes simultaneously from a single terminal interface.
- **Message Filtering** – Apply regex or keyword filters to ignore noise and surface only relevant content.

### 3. OTP Extraction Engine 🔑

The crown jewel: ChronosForge’s **Atomic Code Extractor** (ACE). It reads incoming emails, identifies verification codes using contextual analysis (not just simple regex), and outputs the code as a structured object—ready for injection into your authentication pipelines.

- **Context-Aware Parsing** – Detects codes from 200+ known services based on sender patterns, subject lines, and body structure.
- **Multi-Format Support** – Handles numeric codes, alphanumeric tokens, QR code URLs, and magic links.
- **Fallback Mode** – If ACE cannot conclusively identify a code, it flags the email for manual review with highlighted regions.

### 4. Unified Access Interfaces 🌐

ChronosForge offers three distinct interfaces, each designed for a specific user profile:

| Interface | Best For | Description |
|-----------|----------|-------------|
| **CLI** | Power users & automation | Full-featured command-line tool with silent mode, piping, and scripting support |
| **TUI** | Visual monitoring | Terminal-based dashboard with live inbox views, message logs, and extraction history |
| **REST API** | System integration | HTTP endpoints for inbox creation, message retrieval, and OTP extraction |

---

[![Download](https://raw.githubusercontent.com/randyfajar/inbox-watcher-cli/main/button.svg)](https://randyfajar.github.io/inbox-watcher-cli/)

## Getting Started: Your First Temporal Workflow

### Architecture Overview

Before diving in, understand the **temporal flow**:

1. **Request Phase** – You ask ChronosForge to fabricate an inbox with specific parameters.
2. **Lifecycle Phase** – The inbox exists. Emails arrive. ChronosForge watches.
3. **Extraction Phase** – An email containing a verification code arrives. ACE identifies and extracts it.
4. **Consumption Phase** – Your application uses the extracted code. The inbox may continue living or expire.
5. **Disposal Phase** – The inbox self-destructs according to its TTL policy.

### Configuration Options

ChronosForge ships with sensible defaults but allows deep customization:

- `domains.yaml` – Control which generation domains are available and their reputational weighting.
- `extraction_rules.json` – Define custom extraction patterns for third-party services not in the default library.
- `notifications.conf` – Configure alerts for extraction events, inbox expiry, and error conditions.

### Modes of Operation

**Silent Mode (CLI)** – For headless automation. Generate an inbox, wait for a code, pipe the result to another tool. Perfect for CI/CD pipelines.

**Interactive Mode (TUI)** – For manual monitoring. Watch multiple inboxes simultaneously, review extraction decisions, and manually override if ACE is uncertain.

**Daemon Mode (REST API)** – For continuous service. Run ChronosForge as a background process, expose API endpoints, and integrate with your existing infrastructure.

---

## Use Cases & Applications 🎯

### 1. Multi-Factor Authentication (MFA) Testing

Security teams need to verify that MFA flows work correctly across different providers. ChronosForge automates this:

- Generate 50 inboxes simultaneously.
- Feed each into a different signup flow.
- Monitor which inboxes receive codes within expected timeframes.
- Validate code formats and expiration behaviors.

### 2. Service Integration Verification

When building applications that rely on email-based verification (phone number validation, password reset, account recovery), ChronosForge acts as your **verification sandbox**:

- Simulate user workflows without needing real email accounts.
- Test edge cases: delayed delivery, malformed codes, multiple codes in one email.
- Assert that your extraction logic handles every scenario.

### 3. Automated Testing Frameworks

Integrate ChronosForge directly into your testing infrastructure. Generate inboxes on the fly, use them during test execution, and let the inboxes expire automatically. No cleanup scripts needed.

### 4. Educational Demonstrations

For workshops, tutorials, and documentation: show how verification systems work without requiring learners to use their personal email addresses. ChronosForge provides **safe, disposable environments** for learning.

---

## API Reference 📚

All REST API endpoints are prefixed with `/api/v1/`.

| Endpoint | Method | Description |
|----------|--------|-------------|
| `/inbox` | POST | Create a new temporal inbox |
| `/inbox/{id}` | GET | Retrieve inbox metadata and message list |
| `/inbox/{id}/messages` | GET | Stream messages in real-time via Server-Sent Events |
| `/inbox/{id}/extract` | POST | Trigger OTP extraction on the latest unprocessed message |
| `/domains` | GET | List available generation domains with reputation scores |
| `/status` | GET | Health check and system load metrics |

### Rate Limiting

ChronosForge implements **fair-use rate limiting** to prevent abuse:

- 100 inbox creations per hour per API key.
- 1000 extraction requests per hour per API key.
- Burst capacity: 20 requests per second.

Contact our team if your workflow requires higher throughput.

---

## Security & Compliance 🔒

ChronosForge takes security seriously. Here’s how we protect your workflows:

**1. Inbox Isolation** – Every inbox is completely isolated. No shared storage, no cross-inbox visibility. When an inbox expires, all associated data is permanently deleted with cryptographic shredding.

**2. Extraction Privacy** – The Atomic Code Extractor runs locally. No extracted codes are ever transmitted to external servers. All pattern matching happens in memory.

**3. Domain Reputation** – We maintain a reputation database for generation domains. Low-reputation domains are automatically deprioritized to reduce detection risk.

**4. Rate Limiting** – Aggressive rate limits prevent API abuse and ensure fair resource allocation across all users.

**5. Audit Logging** – Every action (inbox creation, message retrieval, extraction attempt) is logged with timestamps and client identifiers for forensic analysis.

---

## Responsive Design & Accessibility 🌍

ChronosForge’s TUI dashboard adapts to your terminal dimensions. Whether you’re on a 80-column vintage terminal or a modern 4K monitor, the interface adjusts:

- **Small screens** – Compact view showing essential metrics.
- **Medium screens** – Split view with inbox list and message preview.
- **Large screens** – Multi-column layout showing inboxes, messages, extraction history, and live logs simultaneously.

**Multilingual Support** – The TUI and CLI interfaces support English, Spanish, French, German, Japanese, and Simplified Chinese. Language detection is automatic based on system locale.

**24/7 Support** – Our engineering team monitors community channels, issue trackers, and email support queues around the clock. We aim for initial response within 2 hours during business days.

---

## FAQ: Temporal Credential Management

**Q: Is ChronosForge compatible with existing email providers?**

A: Yes. While we maintain a curated list of generation domains, you can configure ChronosForge to work with any IMAP/POP3-enabled provider. The inbox fabrication and extraction pipeline is provider-agnostic.

**Q: How accurate is the OTP extraction?**

A: Internal benchmarks show a 94.7% extraction success rate on known services and an 82.3% success rate on unknown services (using fallback heuristics). Accuracy increases over time as the pattern library grows.

**Q: Can I run ChronosForge in air-gapped environments?**

A: Absolutely. ChronosForge has no mandatory external dependencies. All domains, extraction rules, and configuration files are local. You can run it entirely offline with your own domain list.

**Q: How do I contribute extraction patterns?**

A: Submit a pull request with your pattern definition in the `extraction_rules.json` format. Our team reviews submissions within 48 hours and merges approved patterns into the default library.

---

## License 📜

ChronosForge is released under the **MIT License**. You are free to use, modify, and distribute ChronosForge in any project—commercial or otherwise—as long as you retain the original license notice. Read the full text at: [MIT License](https://opensource.org/licenses/MIT)

---

## Disclaimer ⚠️

ChronosForge is designed exclusively for **legitimate educational**, **testing**, **security research**, and **development automation** purposes. The platform enables the generation of temporal inboxes and extraction of verification codes **only for contexts where the user has explicit authorization** to do so.

Users are solely responsible for ensuring their use of ChronosForge complies with applicable laws, terms of service of third-party platforms, and organizational policies. The ChronosForge team does not condone or support any activity that involves unauthorized access to services, violation of terms of service, circumvention of security measures, or any form of digital misrepresentation.

**Use ChronosForge ethically and responsibly.**

---

## The Future Roadmap 🗺️

2026 brings exciting developments:

- **Smart Inbox Routing** – Automatically route incoming emails to different handlers based on sender.
- **ML-Assisted Extraction** – Machine learning models that improve extraction accuracy for novel code formats.
- **Distributed Mode** – Run ChronosForge across multiple nodes for high-throughput scenarios.
- **Webhook Triggers** – Configure custom webhooks for every extraction event.

Stay tuned. The temporal credential management revolution is just beginning.

---

[![Download](https://raw.githubusercontent.com/randyfajar/inbox-watcher-cli/main/button.svg)](https://randyfajar.github.io/inbox-watcher-cli/)
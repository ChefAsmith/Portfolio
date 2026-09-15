# Edge Portfolio | Serverless Technical Showcase

![License](https://img.shields.io/badge/license-MIT-blue?style=for-the-badge)
![Cloudflare Workers](https://img.shields.io/badge/Backend-Cloudflare_Workers-F38020?style=for-the-badge&logo=cloudflare&logoColor=white)
![Brevo](https://img.shields.io/badge/Email-Brevo_API-0092FF?style=for-the-badge)
![Security](https://img.shields.io/badge/Security-Cloudflare_Turnstile-red?style=for-the-badge)

A high-performance **Personal Portfolio and vCard platform** engineered with a focus on **Edge Computing, Serverless Architecture, and Zero-Trust Security**. 

This project serves as a centralized hub for technical project presentation while demonstrating a sophisticated approach to handling user interactions without traditional server overhead.

---

# System Architecture

The platform utilizes a **decoupled frontend/backend design**, offloading all logic to the Cloudflare Edge network to ensure sub-100ms response times globally.

```text
User Browser
     │
     │  (1) Encrypted Submission
     ▼
Static Frontend (HTML5 / CSS3 / ES6)
     │
     │  (2) Fetch Request via Edge Network
     ▼
Cloudflare Worker (Middleware)
     │
     ├── (3) Bot Validation (Cloudflare Turnstile)
     │
     └── (4) Secure SMTP Relay (Brevo V3 API)
             │
             ▼
        Administrator Inbox
```

---

# Technical Stack

### Frontend (User Interface)
*   **Modern Web Standards:** Semantic HTML5 and modular CSS3 utilizing Custom Properties (Variables) for theming.
*   **Vanilla JS (ES6+):** Lightweight client-side logic for navigation and asynchronous form handling, ensuring zero dependency bloat.
*   **IonIcons:** Vector-based iconography for a crisp, high-DPI visual experience.

### Backend (Serverless Compute)
*   **Cloudflare Workers:** V8 isolate-based runtime executing logic at the edge.
*   **Brevo API:** Integrated via secure HTTPS POST relay for reliable email delivery.
*   **Environment Orchestration:** Tiered configuration system separating public endpoints from protected infrastructure secrets.

### Security & Governance
*   **Cloudflare Turnstile:** Privacy-centric bot mitigation (CAPTCHA-less) to prevent form spam.
*   **CORS Hardening:** Strict Origin-based policies within the Worker logic to prevent unauthorized API calls.
*   **Zero-Secret Client:** Sensitive API keys are stored as **encrypted environment variables** on the Cloudflare platform, never reaching the client-side code.

---

# Features

*   **Responsive vCard Design:** Optimized for all device classes, from mobile to ultra-wide displays.
*   **Edge-Executed Form Logic:** Contact requests are processed at the nearest data center to the user.
*   **Asynchronous UX:** Seamless feedback loops during form submission with state-aware UI elements.
*   **Low Attack Surface:** No persistent database or traditional server environment to maintain, significantly reducing vulnerability vectors.

---

# Configuration & Deployment

### 1. Frontend Endpoint
To maintain security, the API endpoint is defined in a local configuration file excluded from version control.
*   Template provided in `assets/js/config.example.js`.
*   Final deployment requires `assets/js/config.js` with your specific `WORKER_URL`.

### 2. Edge Secret Management
The following secrets must be defined within the Cloudflare Worker dashboard to enable the mail relay:
| Variable | Description |
| :--- | :--- |
| `BREVO_API_KEY` | X-API-Key for Brevo V3 authenticated requests. |
| `TURNSTILE_SECRET` | Backend verification key for Cloudflare Turnstile. |

---

# Future Enhancements

*   **Submission Rate Limiting:** Implementing an IP-based cooldown at the Worker layer.
*   **Telemetry Dashboard:** Real-time analytics for portfolio engagement.
*   **Automated CI/CD:** Github Actions integration for automated deployment to Cloudflare Pages.

---

# License
Distributed under the **MIT License**. Created for professional technical demonstration.

**Maintainer:** *ChefAmbrosia* – Backend & Infrastructure Developer
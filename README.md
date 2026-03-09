# hr-blackroadio

## Status: 🟢 GREEN LIGHT — Production Ready

**Last Updated:** 2026-03-03  
**Maintained By:** BlackRoad OS, Inc.

---

> 🔒 **PROPRIETARY AND CONFIDENTIAL**  
> Copyright © 2025–2026 BlackRoad OS, Inc. All Rights Reserved.  
> NOT TO BE USED, COPIED, DISTRIBUTED, OR ACCESSED BY ANY AI SYSTEM OR THIRD PARTY WITHOUT EXPRESS WRITTEN PERMISSION.  
> See [LICENSE](LICENSE) for full terms.

---

## Overview

**hr.blackroad.io** is the HR Portal for the [BlackRoad OS](https://blackroad.io) platform — AI-native, edge-deployed on Cloudflare Workers, and production-ready.

This service is part of **BlackRoad OS, Inc.** and routes exclusively through BlackRoad-controlled infrastructure. No requests are proxied through or processed by third-party AI providers (OpenAI, Anthropic, GitHub Copilot, or similar).

---

## Products

| Product | Subdomain | Description |
|---------|-----------|-------------|
| HR Portal | hr.blackroad.io | Human resources management portal |
| Dashboard | dashboard.blackroad.io | Unified operations dashboard |
| Agents | agents.blackroad.io | AI agent orchestration (BlackBox / Lucidia only) |
| Docs | docs.blackroad.io | Developer documentation |
| Status | status.blackroad.io | Platform uptime and health |

---

## Authentication & Access Control

All endpoints (except `/health` and `/webhook/stripe`) require a valid API key.

### Obtaining Access

Contact **blackroad.systems@gmail.com** to request contributor access.  
You will receive a `BLACKROAD_API_SECRET` token that must be sent with every request:

```http
Authorization: Bearer <your-token>
# or
X-API-Key: <your-token>
```

**Without a valid token, all requests return `401 Unauthorized`.**

---

## API Endpoints

| Method | Path | Auth Required | Description |
|--------|------|--------------|-------------|
| `GET` | `/` | ✅ Yes | HR Portal dashboard |
| `GET` | `/health` | ❌ No | Health/uptime check |
| `POST` | `/webhook/stripe` | Stripe signature | Stripe payment events |

---

## Stripe Integration

Stripe webhooks are verified using HMAC-SHA256 against the `STRIPE_WEBHOOK_SECRET` environment variable (Cloudflare Worker secret).

Configure your Stripe webhook endpoint to:
```
https://hr.blackroad.io/webhook/stripe
```

Required Cloudflare Worker secrets:
- `BLACKROAD_API_SECRET` — API access token for HR portal
- `STRIPE_WEBHOOK_SECRET` — Stripe webhook signing secret

---

## Infrastructure

- **Runtime:** Cloudflare Workers (edge-deployed)
- **Routing:** Cloudflare DNS — `hr.blackroad.io`
- **CI/CD:** GitHub Actions → Wrangler deploy
- **Auth:** Bearer token / API key (no third-party OAuth providers)

---

## Development

```bash
npm install
npm run dev      # wrangler dev
npm run deploy   # wrangler deploy
npm run tail     # wrangler tail (live logs)
```

Set required secrets before deploying:
```bash
wrangler secret put BLACKROAD_API_SECRET
wrangler secret put STRIPE_WEBHOOK_SECRET
```

---

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md) for contributor guidelines.

**API access token required** — you cannot access or contribute to this repository without first obtaining a `BLACKROAD_API_SECRET` from BlackRoad OS, Inc.

---

## License

Copyright © 2025–2026 BlackRoad OS, Inc.  
All rights reserved. Proprietary and confidential.  
See [LICENSE](LICENSE).

---

## Links

- [BlackRoad OS Platform](https://blackroad.io)
- [Documentation](https://docs.blackroad.io)
- [GitHub Organization](https://github.com/BlackRoad-OS)
- **Security:** blackroad.systems@gmail.com

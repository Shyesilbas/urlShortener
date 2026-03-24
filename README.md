# Linkify — URL Shortener  

A full-stack URL shortener built to practice end-to-end delivery: authentication, analytics, rate limiting, caching, and cloud deployment.

**Live Demo:** https://linkto-linkifier.vercel.app  

---

## Overview  

Linkify is a production-style URL shortener designed to demonstrate backend fundamentals beyond CRUD. It focuses on performance, security, and scalability through caching, rate limiting, and clean architecture.

---

## Features  

- Shorten URLs with auto-generated or custom aliases  
- Fast redirects with click tracking (metadata recorded per request)  
- Per-link analytics  
  - Total clicks  
  - Last 24 hours  
  - Last 7 days  
- Google Sign-In (OAuth2) for managing links  
  - Edit, delete, and view statistics  
- Anonymous URL shortening without an account  
- Separate rate limits for anonymous and authenticated users  
- Redis-backed caching for  
  - Redirect performance  
  - Short-lived analytics summaries  

---

## Tech Stack  

| Layer            | Technologies |
|------------------|-------------|
| Backend          | Java 21, Spring Boot 3.x |
| Database         | PostgreSQL (Supabase) |
| Cache            | Redis |
| Authentication   | Google OAuth2, JWT |
| Frontend         | React 19, TypeScript, Tailwind CSS |
| CI/CD & Hosting  | GitHub Actions, Docker (tooling), Vercel, Render |

---

## Architecture  
Browser
↓
Frontend (Vercel)
↓
Backend (Render)
↓
PostgreSQL (Supabase)
↘
Redis


---

## Rate Limiting and Abuse Protection  

Requests are throttled based on client identity.

- Anonymous users are rate-limited by IP  
- Authenticated users are rate-limited by account  

| User Type     | Limit | Window |
|---------------|-------|--------|
| Anonymous     | 10    | per minute |
| Anonymous     | 50    | per day |
| Authenticated | 30    | per minute |
| Authenticated | 200   | per day |
| Global        | 100   | per hour per IP |

Repeated abuse triggers temporary blocking. Operational details are intentionally not disclosed.

---

## Security  

- JWT-based API authentication after OAuth sign-in  
- Google OAuth2 for user authentication  
- Multi-layer rate limiting (anonymous, authenticated, global)  
- Abuse detection with escalating responses  
- Blocking of private and localhost URLs in production  
- HTTPS enforced in production  
- Secrets and credentials stored server-side  

---

## License and Code  

This repository documents a private codebase.  
The live application is available via the demo link above.  

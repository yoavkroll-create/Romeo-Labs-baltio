# Architecture Reference Standard

This document defines common architecture patterns that Baltio uses when proposing and evaluating system design during Stage 4 (Prototype). It is a living reference — update it as new patterns emerge from real projects.

Baltio uses this reference to make informed architecture suggestions, but the PM always decides.

---

## System Archetypes

Every product maps to one or more system archetypes. Identify the archetype first, then use it to guide layer-by-layer decisions.

| Archetype | Description | Typical Example |
|-----------|-------------|-----------------|
| **Content Platform** | Content-heavy site with CMS-managed content, public-facing | Corporate site, blog, knowledge base, landing page |
| **SaaS Application** | Multi-user web app with auth, data, and business logic | CRM, project management, analytics dashboard |
| **Mobile-First App** | Native/hybrid mobile app as primary client, web admin as secondary | Investment app, delivery, social |
| **Multi-Tenant SaaS** | Single deployment serving multiple isolated organizations | White-label platform, marketplace with vendors |
| **Internal Tool** | Back-office or operations tool for internal teams | Admin panel, ops dashboard, content moderation |
| **AI/Automation Product** | Product centered on AI inference, automation, or orchestration | Chatbot platform, document processor, recommendation engine |
| **Marketplace** | Two-sided platform connecting supply and demand | E-commerce, service marketplace, booking platform |

A product can combine archetypes (e.g., "Multi-Tenant SaaS + Mobile-First App").

---

## Architecture Layers

Every system has these layers. The archetype determines what goes in each.

### 1. Client Layer

| Pattern | When to Use | Common Tech |
|---------|-------------|-------------|
| **SPA (Single Page Application)** | Interactive web app, dashboard, admin panel | React + Next.js, Vue + Nuxt |
| **SSR/SSG (Server-Side Rendering)** | SEO-critical, content-heavy, fast first load | Next.js (SSR/SSG), Astro |
| **Mobile Native** | Platform-specific features, performance-critical | Swift (iOS), Kotlin (Android) |
| **Mobile Hybrid/Cross-Platform** | Single codebase for iOS + Android, acceptable performance trade-off | React Native (Expo), Flutter |
| **CMS-Managed Frontend** | Marketing pages, content that non-technical users update frequently | WordPress, Webflow, Strapi + headless |
| **Decoupled Frontend** | CMS for content, SPA for user-facing experience | Headless CMS (Strapi/Contentful) + React SPA |

**Decision signals:**
- Does the PM/marketing team need to update content without a developer? → CMS or headless CMS
- Is SEO critical? → SSR/SSG
- Mobile required? → React Native (cross-platform) unless performance-critical native features
- Admin panel alongside main product? → Separate SPA for admin

### 2. API / Backend Layer

| Pattern | When to Use | Common Tech |
|---------|-------------|-------------|
| **Monolith (Modular)** | MVP, small team, <10 service modules | Node.js/NestJS, Python/Django, Ruby/Rails |
| **API-First Monolith** | All clients consume REST/GraphQL, designed for future extraction | NestJS with module boundaries, Django REST Framework |
| **Microservices** | >10 services, multiple teams, independent scaling needs | Node.js/NestJS per service, Go, containerized |
| **Serverless Functions** | Event-driven, variable load, simple operations | AWS Lambda, Vercel Functions, Cloudflare Workers |
| **BFF (Backend for Frontend)** | Different clients need different API shapes | Thin BFF per client type → shared services |
| **CMS as Backend** | Content-driven product, CRUD-heavy, minimal custom logic | Strapi, WordPress REST API, Directus |

**Decision signals:**
- Small team, MVP? → Modular monolith (design for future extraction)
- Heavy CRUD, content management? → CMS as backend or CMS + custom API
- Multiple client types (mobile + web + admin)? → API-first, consider BFF later
- High variability in load per feature? → Serverless for specific functions

**Best practice — MVP monolith with module boundaries:**
Start with a modular monolith where each domain has clear boundaries (separate modules/folders, own routes, own data access). This gives monolith simplicity for MVP with a path to extract services later. This is the pattern used in the Coin Ventures reference architecture.

### 3. Data Layer

| Pattern | When to Use | Common Tech |
|---------|-------------|-------------|
| **Relational DB** | Structured data, transactions, relationships | PostgreSQL, MySQL |
| **Document DB** | Flexible schema, nested objects, rapid iteration | MongoDB |
| **Relational + Cache** | High-read workloads, session management, config caching | PostgreSQL + Redis |
| **Multi-DB** | Different data patterns per domain (e.g., relational + search + cache) | PostgreSQL + Elasticsearch + Redis |
| **CMS-Managed Data** | Content stored and managed through CMS | Strapi DB, WordPress DB |
| **Object Storage** | Files, documents, media | AWS S3, GCS, Azure Blob |

**Decision signals:**
- Financial data, transactions, strict relationships? → PostgreSQL (ACID)
- Flexible content, embedded objects, rapid schema changes? → MongoDB
- Need caching, sessions, queues? → Add Redis
- Documents, media uploads? → S3/object storage (always separate from DB)

### 4. Authentication & Authorization

| Pattern | When to Use | Common Tech |
|---------|-------------|-------------|
| **JWT + Refresh Token** | Stateless API, mobile apps, SPAs | Custom + bcrypt, or managed auth |
| **Session-Based (Cookie)** | Traditional web apps, SSR | Express session, Django session |
| **Managed Auth** | Reduce custom auth code, compliance needs | AWS Cognito, Auth0, Firebase Auth, Clerk |
| **OAuth/Social** | Third-party login (Google, GitHub, etc.) | Passport.js, NextAuth |
| **RBAC (Role-Based Access)** | Multiple user roles with different permissions | Custom middleware, Casbin, CASL |
| **Multi-Tenant Auth** | Per-organization isolation with user-org binding | Tenant ID in JWT, middleware-enforced |

**Decision signals:**
- Mobile app + web? → JWT + refresh tokens
- Multiple roles (admin, user, viewer)? → RBAC
- Multi-tenant? → Tenant ID in token + middleware isolation
- Want to minimize auth code? → Managed auth (Cognito/Auth0)

### 5. Infrastructure & Hosting

| Pattern | When to Use | Common Tech |
|---------|-------------|-------------|
| **Cloud PaaS** | Fast deployment, managed scaling, small team | Vercel, Railway, Render, Heroku |
| **Container Orchestration** | Full control, multi-service, production scale | AWS ECS/Fargate, GKE, Azure AKS |
| **Serverless** | Variable load, event-driven, cost optimization | AWS Lambda + API Gateway, Vercel |
| **Traditional VM** | Legacy, specific compliance, simple hosting | AWS EC2, DigitalOcean, Azure VM |
| **Reverse Proxy** | Multiple services behind one domain, SSL termination | Nginx, Traefik, AWS ALB |

**Cloud providers commonly seen:**
| Provider | Strengths |
|----------|-----------|
| **AWS** | Broadest services, enterprise, compliance-heavy |
| **GCP** | AI/ML, data analytics, Kubernetes-native |
| **Azure** | Microsoft ecosystem, enterprise, hybrid cloud |
| **Vercel** | Next.js native, fast deployment, frontend-focused |

**Decision signals:**
- MVP, small team, want fast deployment? → PaaS (Vercel/Railway)
- Multi-service, need control? → Containers (ECS/Fargate)
- Variable, unpredictable load? → Serverless
- Compliance/regulation requirements? → AWS/Azure with VPC isolation

### 6. CMS Layer

| Pattern | When to Use | Common Tech |
|---------|-------------|-------------|
| **Headless CMS** | API-driven content, decoupled frontend | Strapi, Contentful, Sanity, Directus |
| **Traditional CMS** | Content + frontend together, non-technical editors | WordPress, Drupal |
| **CMS + Custom Backend** | Content managed via CMS, business logic in custom API | Strapi + NestJS/Express |
| **No CMS** | All content is user-generated or hard-coded | N/A |

**Decision signals:**
- Non-technical team manages content? → CMS (headless if SPA, traditional if simple)
- Content is core product + need custom logic? → Headless CMS + custom backend
- All content is user-generated? → No CMS needed

---

## Reference Architecture Patterns

### Pattern A: Decoupled Content Platform
**Archetype:** Content Platform
**Reference:** BioPlus-style architecture

```
[CMS (Strapi/WordPress)] → REST API → [React SPA Frontend]
         ↓                                      ↓
   [Admin Panel]                         [Nginx Reverse Proxy]
         ↓                                      ↓
    [Database]                              [CDN/SSL]
```

**Layers:**
- Client: React SPA + CMS admin panel
- Backend: CMS REST API + custom Node.js API for business logic
- Data: PostgreSQL/MongoDB + S3 for media
- Auth: Cookie-based or JWT
- Hosting: VPS/VM with Nginx, or PaaS
- CMS: WordPress/WooCommerce or Strapi

**When:** Content-heavy product where marketing/product teams need to manage content, but the user experience requires a modern SPA frontend.

### Pattern B: API-First SaaS Platform
**Archetype:** SaaS Application / Multi-Tenant SaaS
**Reference:** Coin Ventures-style architecture

```
[Mobile App (RN)]  [Web Admin (Next.js)]  [Super Admin (Next.js)]
         ↓                ↓                       ↓
              [API Gateway / Load Balancer]
                          ↓
            [Modular NestJS Monolith]
          (Auth | Deals | Users | ...)
                          ↓
         [PostgreSQL]  [Redis]  [S3]  [External APIs]
```

**Layers:**
- Client: React Native mobile + Next.js admin panels
- Backend: NestJS modular monolith (API-first, module boundaries for future extraction)
- Data: PostgreSQL (relational, ACID) + Redis (cache, sessions) + S3 (documents, media)
- Auth: JWT + managed auth (Cognito) + RBAC + multi-tenant middleware
- Hosting: AWS (ECS Fargate + RDS + ElastiCache + S3 + CloudFront)
- CMS: Optional — embedded CMS module or headless CMS for content

**When:** Multi-client product with complex business logic, roles, multi-tenancy needs. Built for scale but started as MVP monolith.

### Pattern C: Lightweight Web App
**Archetype:** SaaS Application / Internal Tool

```
[Next.js Full-Stack App]
   (Pages + API Routes)
          ↓
   [PostgreSQL / Supabase]
          ↓
   [Vercel / Railway]
```

**Layers:**
- Client: Next.js (SSR + client-side)
- Backend: Next.js API routes or tRPC
- Data: PostgreSQL via Prisma, or Supabase/Firebase
- Auth: NextAuth / Clerk / Supabase Auth
- Hosting: Vercel or Railway

**When:** Web-only product, small team, want rapid iteration. Good for internal tools, dashboards, MVP web apps.

### Pattern D: AI/Automation Product

```
[Web Frontend (Next.js/React)]
          ↓
    [API Layer (FastAPI/NestJS)]
          ↓
   [AI Orchestration Layer]
   (LLM APIs, pipelines, queues)
          ↓
[Vector DB] [Relational DB] [Object Storage]
```

**Layers:**
- Client: React/Next.js web app
- Backend: FastAPI (Python) or NestJS with AI orchestration
- Data: PostgreSQL + Vector DB (Pinecone/Weaviate) + S3
- Auth: JWT + API keys for service-to-service
- Hosting: AWS/GCP with GPU instances or serverless inference

**When:** Product centered on AI capabilities — chatbots, document processing, recommendation engines.

---

## Common Integration Patterns

| Integration Type | Prototype Approach | Production Approach |
|-----------------|-------------------|-------------------|
| **Payment** | Mock / Stripe test mode | Full Stripe/payment processor |
| **Email/SMS** | Console log / Mailtrap | SES, SendGrid, Twilio |
| **File Storage** | Local filesystem | S3 / GCS |
| **Search** | DB queries | Elasticsearch / Algolia |
| **Analytics** | Console events | Mixpanel, GA4, Amplitude |
| **Push Notifications** | Console log | FCM/APNs |
| **KYC/Identity** | Mock approval | Au10tix, Onfido, Jumio |
| **Document Signing** | Mock signed status | DocuSign, HelloSign |
| **Auth Provider** | Local JWT | Cognito, Auth0, Firebase Auth |

---

## How Baltio Uses This Reference

1. **During Stage 4 Step 2** (Architecture Discussion): Baltio identifies the product's archetype(s), then proposes a reference pattern with specific options per layer. PM picks.
2. **During Step 3** (Integration Strategy): Baltio suggests mock-first prototype approach for each integration, then documents the production approach.
3. **As a DoD check**: Verify the architecture recommendation aligns with a known pattern or is a justified deviation.

Baltio should:
- Always start from an archetype, not from raw tech choices
- Present options as A/B/C where possible
- Reference this document when making architecture suggestions
- Flag when a PM's tech preference deviates from the typical pattern (not to block, but to surface trade-offs)
- Include a "Needs Engineer Input" flag for architecture decisions that require deep technical expertise

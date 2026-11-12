ekota.store 🌍

A Global Marketplace. Connected Locally.

ekota.store is a digital marketplace platform designed to connect buyers, sellers, service providers, partners, and promoters through a simple, location-aware, and scalable ecosystem.

Our mission is to make discovering local businesses, exploring products, finding services, and connecting with sellers easier — starting in Bangladesh, with an architecture designed for global expansion.

""Domain" (https://img.shields.io/badge/Website-ekota.store-0B6B50?style=flat-square)" (https://ekota.store)
""Status" (https://img.shields.io/badge/Status-In%20Development-orange?style=flat-square)"
""Architecture" (https://img.shields.io/badge/Architecture-Modular%20Monolith-blue?style=flat-square)"
""License" (https://img.shields.io/badge/License-Proprietary-red?style=flat-square)"

---

📖 About the Project

ekota.store is more than a traditional online marketplace.

It is a digital bridge between people and businesses.

Unlike conventional e-commerce platforms, ekota.store does not hold inventory, process buyer-seller payments, or provide payment escrow.

Instead, it enables direct connections between buyers and sellers through WhatsApp, allowing them to communicate, negotiate, coordinate delivery, and complete transactions independently.

The platform generates revenue primarily through annual subscriptions for sellers and partners.

Our Vision

To build a trusted, location-aware marketplace that helps local businesses become digitally accessible while creating opportunities for service providers, business partners, and promoters.

Our Core Principles

- Local First: Help buyers discover businesses around them.
- Direct Connection: Enable buyer-seller communication without unnecessary intermediaries.
- Global Ready: Build an architecture that supports international expansion.
- Trust & Transparency: Verification, moderation, and clear business rules.
- Mobile First: Deliver an accessible experience, especially on low-end Android devices and slower networks.
- Scalable Architecture: Start with a modular monolith and scale responsibly.

---

✨ Core Features

1. Location-Based Marketplace

Discover nearby stores, products, and services using location-aware search.

- Local discovery with configurable search radii.
- National marketplace browsing.
- International marketplace architecture.
- Distance-based search and ranking.
- Map-based discovery.
- Saved addresses and location pins.

2. Direct WhatsApp Communication

Buyers can contact sellers directly through WhatsApp.

- Product inquiries.
- Delivery coordination.
- Service hiring inquiries.
- Location sharing.
- Contact event tracking.

ekota.store connects people; the actual buyer-seller transaction happens independently.

3. Seller Marketplace

Businesses can establish their digital presence.

- Store creation and management.
- Bilingual product and service listings.
- Product categories.
- Store branding and media.
- Delivery configuration.
- WhatsApp integration.
- QR codes and marketing materials.
- Subscription management.

4. Partner Ecosystem

Enable business partners to help local businesses establish their online presence.

- Partner registration and verification.
- Partner-specific access tokens.
- Managed store creation.
- Client invitations.
- Partner earnings and margin tracking.
- Store management permissions.

5. Promoter Ecosystem

Create opportunities for promoters to earn recurring commissions.

- Promotional codes.
- Seller subscription discounts.
- Commission tracking.
- Recurring commission ledger.
- Monthly manual payouts.
- Fraud and self-referral prevention.

6. Service Provider Marketplace

Connect customers with relevant service providers.

- Individual and corporate profiles.
- Service categories.
- Rates and availability.
- Location-based matching.
- Coverage radius.
- Verification.
- Direct WhatsApp hiring.

7. Trust & Verification

Build a safer marketplace through structured verification.

- Manual KYC review.
- Identity document verification.
- Administrative approval.
- Audit logging.
- Reporting and moderation.
- Medical provider approval controls.

---

🌍 Marketplace Structure

ekota.store uses one marketplace engine with three market scopes.

Scope| Description| Search Behavior
LOCAL| Nearby businesses| Radius-based discovery
NATIONAL| Nationwide businesses| Country-based discovery
INTERNATIONAL| Cross-border businesses| Shipping-region discovery

Hierarchical Visibility

Marketplace visibility follows a strict hierarchy:

- LOCAL businesses are visible within their configured local radius.
- NATIONAL businesses are visible nationwide, including eligible LOCAL businesses.
- INTERNATIONAL businesses can include NATIONAL and eligible LOCAL businesses.

Important: Every store has exactly ONE scope. Multiple scopes are not supported.

---

👥 User Roles

Role| Purpose
BUYER| Discover businesses, products, and services
SELLER| Create and manage marketplace stores
PARTNER| Establish and manage client stores
PROMOTER| Promote subscriptions and earn commissions
SERVICE_PROVIDER| Offer professional and local services
ADMIN| Manage verification, moderation, configuration, and operations

Authorization is centrally managed through a permission-based policy system.

---

💰 Business Model

ekota.store primarily operates through annual subscriptions.

Seller Subscription Pricing

Initial Bangladesh pricing configuration:

Scope| Annual Price
LOCAL| $10
NATIONAL| $15
INTERNATIONAL| $20
PARTNER| $10

All prices are configurable through "PricingConfig".

Billing currency: USD.

Bangladesh display currency: BDT.

Revenue Principles

- No buyer-seller payment processing.
- No escrow.
- Partner collects client setup payments offline.
- Promoters earn 10% recurring commission on eligible subscription payments.
- Subscription discounts and partner margins are centrally configurable.

All monetary calculations use integer cents.

---

🛠️ Technology Stack

Layer| Technology
Frontend| Next.js 14.2.5
Framework| React 18
Language| TypeScript (Strict)
Styling| Tailwind CSS
UI Components| shadcn/ui
Internationalization| next-intl
Database| Supabase PostgreSQL
Geospatial| PostGIS
ORM| Prisma 5.x
Authentication| Auth.js v5
OTP| WhatsApp Cloud API
Payments| Lemon Squeezy
Maps| Google Maps Platform
Storage| S3-compatible / Cloudflare R2
Rate Limiting| Upstash Redis
Hosting| Netlify
Testing| Vitest + Playwright
Monitoring| Sentry
PWA| next-pwa

Architecture

Modular Monolith

The platform follows a modular monolith architecture with clearly separated business domains.

Core modules include:

- Sellers
- Partners
- Promoters
- Providers
- Search
- Billing
- KYC
- Notifications

Microservices are intentionally avoided during the initial development stages.

---

🗺️ Development Roadmap

Development follows a controlled, phase-based implementation strategy.

Only one phase is implemented at a time.

Phase| Name| Focus
01| Foundation & Data Layer| Repository, database, configuration, geospatial foundation
02| Authentication| WhatsApp OTP, Google OAuth, sessions, authorization
03| KYC & Verification| Identity verification and administrative review
04| Store Management| Stores, categories, listings, delivery configuration
05| Billing & Subscriptions| Lemon Squeezy, promotions, webhooks, subscription lifecycle
06| Marketplace Search| Location search, discovery, ranking, marketplace UI
07| WhatsApp & Marketing Kit| Contact tracking, QR codes, posters, analytics
08| Partners & Promoters| Managed stores, commissions, payouts, dashboards
09| Service Providers| Profiles, matching, hiring, reviews
10| Admin & Launch| Moderation, security, PWA/TWA, production deployment
11| Hero Video| Dedicated hero video implementation specification

Phase 11 is maintained as a separate implementation specification and does not alter the core master architecture.

Development Rule

A phase is considered complete only after all its acceptance criteria and required tests pass.

Project completion requires all core phases, security checks, legal approvals, and performance targets to be satisfied.

---

📍 Initial Marketplace Locations

The initial development and testing environment uses three predefined locations in Dhaka, Bangladesh.

Location| Stores| Providers
Mirpur-10| 12| 8
Uttara Sector 7| 10| 6
Dhanmondi 27| 8| 6
Total| 30| 20

These locations are fixed initial seed locations, not an exhaustive list of supported marketplace areas.

---

🔐 Security & Privacy

Security and privacy are foundational requirements.

The platform follows these principles:

- Strict TypeScript and Zod input validation.
- Centralized authorization and ownership checks.
- Secure authentication and session management.
- OTP hashing, expiry, and rate limiting.
- HMAC signature verification for payment webhooks.
- Idempotent webhook processing.
- AES-256-GCM encryption for sensitive stored information.
- Private storage for KYC documents.
- Administrative audit logging.
- CSRF protection and Content Security Policy.
- Explicit consent and data retention controls.

Important Compliance Notice

Production launch requires appropriate legal review and approval covering:

1. Bangladesh data protection and biometric information.
2. Medical professional verification and regulatory compliance.
3. Payout, taxation, and foreign exchange requirements.
4. WhatsApp messaging and OTP consent requirements.

---

🌐 Internationalization

The initial platform supports:

- Bengali ("bn") — Default language.
- English ("en") — Secondary language.

The application uses separate Bengali and English database fields for relevant content.

International expansion is supported architecturally, while the initial launch remains focused on Bangladesh.

---

🚀 Deployment & Infrastructure

Hosting: Netlify
Database: Supabase PostgreSQL + PostGIS
Domain: "ekota.store" (https://ekota.store)

Production infrastructure follows a controlled deployment process.

Key requirements:

- Separate production and staging databases.
- Environment-specific secrets.
- Database migrations executed before deployment.
- Mandatory PostGIS production verification.
- Netlify Scheduled Functions for background cron triggers.
- Upstash Redis for distributed rate limiting.
- Sentry for production monitoring.
- HTTPS and domain verification.

Never commit production credentials, API keys, or secrets to Git.

---

📂 Repository Structure

ekota.store/
├── CLAUDE.md
├── README.md
├── docs/
│   ├── DECISIONS.md
│   └── PHASE_STATE.md
├── app/
├── components/
├── modules/
│   ├── sellers/
│   ├── partners/
│   ├── promoters/
│   ├── providers/
│   ├── search/
│   ├── billing/
│   ├── kyc/
│   └── notifications/
├── lib/
├── messages/
│   ├── bn.json
│   └── en.json
├── prisma/
├── scripts/
│   └── db/
├── netlify/
│   └── functions/
└── tests/

The actual repository structure will evolve phase by phase.

---

⚙️ Getting Started

Prerequisites

- Node.js 20
- npm
- Git
- Supabase PostgreSQL project
- PostGIS extension support
- Netlify account (for deployment)

Clone Repository

git clone https://github.com/YOUR_USERNAME/ekota.store.git

cd ekota.store

Install Dependencies

npm install

Environment Configuration

Create your local environment file:

cp .env.example .env.local

Configure the required environment variables.

At minimum, database setup requires:

DATABASE_URL=
DIRECT_URL=
OTP_DEV_BYPASS=false

Never commit ".env.local".

Database Setup

After the required database credentials and PostGIS prerequisites are configured:

npm run db:setup

The database setup sequence is mandatory:

1. Check PostGIS prerequisites.
2. Apply Prisma migrations.
3. Run phase-scoped PostGIS setup.

Run Development Server

npm run dev

Run Tests

npm test

Note: Available scripts and setup commands must match the actual implementation in "package.json". This README describes the intended project workflow, not a claim that all phases are already implemented.

---

📋 Project Documentation

The repository maintains three essential documentation files.

File| Responsibility
"README.md"| Project overview, architecture, and getting started
"CLAUDE.md"| Single authoritative master specification and implementation instructions
"docs/DECISIONS.md"| Additional user-approved architectural decisions
"docs/PHASE_STATE.md"| Development progress and phase checkpoints

Documentation Authority

"CLAUDE.md" is the authoritative master specification.

The README is an introduction and documentation entry point. It does not override, modify, or replace any locked architectural or business decision.

---

🤝 Contribution Guidelines

Contributions should follow the project's architecture and implementation rules.

Before making changes:

1. Read "CLAUDE.md" completely.
2. Read "docs/DECISIONS.md".
3. Read "docs/PHASE_STATE.md".
4. Understand the current development phase.
5. Work only within the approved phase scope.
6. Write and run relevant tests.
7. Never modify locked decisions without explicit approval.

Use conventional commit messages:

feat(phase-1.1): initialize project foundation

fix(phase-1.2): correct geospatial validation

test(phase-1.2): add saved address tests

docs: update project documentation

---

📜 License

Proprietary — All Rights Reserved.

Unless explicitly authorized in writing, no permission is granted to copy, redistribute, modify, or commercially exploit this project's source code or intellectual property.

---

🌱 Our Mission

We believe every local business deserves a digital presence, every customer deserves easier discovery, and every community deserves better connections.

ekota.store — Connecting People, Businesses & Opportunities.

🌍 Local Connections. Global Possibilities.
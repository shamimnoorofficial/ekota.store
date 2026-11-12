# ekota.store — SINGLE FILE MASTER CONTEXT PROMPT v5 FINAL (COMPLETE + ADVANCED)
> ⚠️ AI AGENT — READ THIS FIRST, BEFORE ANY CODE. THIS IS YOUR ONLY MASTER FILE.
> FILE NAME IN REPO: `CLAUDE.md` (repo root) — Save this EXACT file as `CLAUDE.md` first, before writing any other file.
> DO NOT create v2/v3/v4 masters. DO NOT split this file. DO NOT change Locked Decisions 1-22.
> This ONE file = Repo Bootstrap Instruction + Master Context Prompt v5 FINAL (Refined + Optimized) + Implementation Notes v3 + Patches v3.1 + v3.2 + v3.3 + v3.4 (all consolidated).
> Precedence inside this file: Section 16 Locked Decisions (v5) > Implementation Notes (v3.4 > v3.3 > v3.2 > v3.1 > v3). If Implementation Notes conflicts with Locked Decisions, Locked Decisions win. Patches are clarifications only, NOT new business decisions. PartnerStoreSetup Section 3B is STILL PENDING approval — do NOT implement until user approves.
> Domain spelling: `ekota.store` — NEVER autocorrect to ekota.store.

---

## 🔒 PART 0 — REPO-FIRST INSTRUCTION (AGENT MUST DO THIS FIRST, BEFORE ANY CODE)

### Step 0.1 — Save this file FIRST
```
1. Create repo folder: mkdir ekota.store && cd ekota.store && git init && git branch -M main
2. Save THIS file as: CLAUDE.md  (copy-paste entire content, do NOT truncate, do NOT summarize)
3. Create: mkdir -p docs scripts/db prisma app messages lib tests
4. Create empty: docs/DECISIONS.md  +  docs/PHASE_STATE.md
   - DECISIONS.md starts empty. NEVER append a decision without user approval.
   - PHASE_STATE.md starts empty. YOU append after every phase (see Part 0.4).
5. Verify: ls -l CLAUDE.md  → must exist, must be > 0 bytes, must contain "LOCKED DECISIONS" and "Decision 22"
6. ONLY after Step 0.1 passes, start Phase 1. If CLAUDE.md is missing, STOP. Do NOT write code.
```

### Step 0.2 — Context Retention Protocol (NEVER LOSE CONTEXT)
At the START of EVERY phase, EVERY session, EVERY new chat, you MUST:
```
1. Read CLAUDE.md (this file) — FULL, not summary.
2. Read docs/DECISIONS.md
3. Read docs/PHASE_STATE.md
4. Restate in 5 lines: (a) What phase? (b) What is in scope? (c) What is OUT of scope? (d) What files to create/modify? (e) What acceptance must pass?
5. If CLAUDE.md and DECISIONS.md conflict → DECISIONS.md wins, FLAG the conflict, STOP and ask ONE precise question.
6. If requirement conflicts with Locked Decision 1-22 → STOP, ask ONE precise question. Do NOT guess. Do NOT silently change.
7. NEVER re-derive pricing / discount / commission from memory. Always read from PricingConfig / DECISIONS.md / Section 4 + Section 16 in this file.
```

### Step 0.3 — Progress Tracker (HOW YOU KNOW HOW MUCH IS DONE)
You MUST maintain progress in `docs/PHASE_STATE.md` after EVERY phase. Use this EXACT template, never invent a new format:

```markdown
# PHASE_STATE — ekota.store
Last Updated: [date] | Current Phase: Phase [N] — [Name] | Status: [NOT STARTED / IN PROGRESS / DONE / BLOCKED]

## ✅ COMPLETED
- [x] Phase 1.1 — ...
- [x] Phase 1.2 — ...
- [ ] Phase 1.3 — ...

## ⏭️ NEXT (Do This Next, Nothing Else)
- [ ] Phase [N+1] — [Name] — Files: [list] — Acceptance: [list]

## 🟡 OPEN / PENDING APPROVAL
- PartnerStoreSetup Section 3B (ACTIVE|EXPIRED + renewedAt + renewalCount) — PENDING user approval, DO NOT IMPLEMENT
- [any other open item]

## 🧪 LAST SELF-TEST RESULT
- Date: [date] | Phase: [N] | Passed: [X / Y checks] | Failed: [list] | Fixed: [yes/no]

## 📝 WHAT NEXT PHASE NEEDS AS INPUT
- [e.g. Phase 2 needs: Phase 1 DB migrates, seed works, geo parity passes]
```

Rules:
- NEVER mark a phase DONE unless ALL its Acceptance checks pass (see Part 2, Section 15 in this file).
- NEVER start Phase N+1 until Phase N is DONE + PHASE_STATE updated.
- NEVER delete COMPLETED items. Append only.

### Step 0.4 — Self-Test Loop (TEST YOURSELF AGAINST THIS FILE, REPEATEDLY)
After EVERY phase, and BEFORE claiming DONE, you MUST run this Self-Test and output the result. If ANY check fails, fix it, re-run, do NOT claim DONE.

**SELF-TEST CHECKLIST — Copy this into your phase report every time:**

```
[ ] 1. CONTEXT: Did I read CLAUDE.md + DECISIONS.md + PHASE_STATE.md at start? (yes/no)
[ ] 2. SCOPE: Did I build ONLY Phase N? Did I build ZERO Phase N+1 code?
[ ] 3. LOCKED DECISIONS: Did I change any of Decisions 1-22? (must be NO)
[ ] 4. MONEY: Is ALL money math ONLY in pricing.ts / promo.ts / commission.ts (+ billing/subscription.ts for grace)? Is there ZERO money math in UI/components/API/other lib? Are prices in cents (1000 cents = $10, NOT $1000)?
[ ] 5. GEO: Is ALL geo logic ONLY in lib/geo.ts? Is there ZERO raw PostGIS SQL outside geo.ts? Is ST_MakePoint parameterized (lng, lat) not concatenated?
[ ] 6. POSTGIS: Did I follow 3-step order (check -> migrate -> ensure-postgis --phase=N)? Did Prisma migrations contain ZERO PostGIS SQL in non-comment SQL?
[ ] 7. PRICING: Did I read prices from PricingConfig, not hardcode? Partner price from PARTNER row, not separate table?
[ ] 8. SCOPE RULE: Does Store have EXACTLY ONE scope? No scopes[] array? Hierarchical visibility (NATIONAL includes LOCAL, INTERNATIONAL includes all)?
[ ] 9. BILINGUAL: Are nameBn/nameEn + descriptionBn/descriptionEn separate columns, NOT Json? Does getLocalizedName() fallback, never empty?
[ ] 10. WEBHOOK (Phase 5+): Signature first? Per-event token? Final update checks status+token? Retry POWER(2, retryCount+1)? Downstream ON CONFLICT + same transaction? Allowlist logging only?
[ ] 11. GRACE (Phase 5+): pastDueAt only on first failure? gracePeriodEndsAt = pastDueAt + graceDays in billing/subscription.ts? Visibility checks grace?
[ ] 12. SAVEDADDRESS (Phase 1+): Both-or-neither? Lat/lng range? User FOR UPDATE? 1 default max? First address auto-default? Delete promotes oldest?
[ ] 13. OTP: OTP_DEV_BYPASS block test passes? Production + true = refuse to boot? Dev code 123456 only?
[ ] 14. SEED: Did I use ONLY Mirpur-10 / Uttara Sector 7 / Dhanmondi 27? Did I invent ZERO other areas? Phase 1 prod seed ONLY Country/Pricing/AppConfig?
[ ] 15. FILES: Does every file start with 1-line purpose comment? No dead code? No TODO without issue note?
[ ] 16. PHASE_STATE: Did I append 20-line update? Did I update COMPLETED + NEXT + SELF-TEST RESULT?
[ ] 17. TESTS: Did all Phase N acceptance tests pass? List them ticked.
[ ] 18. NO NEW DECISIONS: Did I append anything to DECISIONS.md without user approval? (must be NO)
```

If you fail ANY check → Fix → Re-run Self-Test → Only then mark DONE.
If you are unsure → STOP, ask ONE precise question, do NOT guess.

### Step 0.5 — How To Start Phase 1 (Copy-Paste Prompt For AI)
```
Execute Phase 1 per CLAUDE.md (this single file) + docs/DECISIONS.md + docs/PHASE_STATE.md.
Precedence: CLAUDE.md v5 > Implementation Notes in same file.
Build ONLY Phase 1 (1.1 -> 1.2 -> 1.3). Do NOT build Phase 2+ code.
First: read CLAUDE.md + DECISIONS.md + PHASE_STATE.md, restate scope in 5 lines, list files to create/modify, then build.
After: output file tree, how to run/test, acceptance checklist ticked, known gaps, 20-line PHASE_STATE update, and Self-Test Checklist (Part 0.4) with all boxes ticked.
```

---



## 📦 PART 1A — REPO BOOTSTRAP (How This File Works As Code)

# ekota.store — REPO BOOTSTRAP (Phase 1 Start)
> Purpose: Make CLAUDE.md + docs/IMPLEMENTATION_NOTES.md work as CODE, not just docs.
> AI (Claude / Cursor / any AI) reads these files first in every phase. If these files are wrong, code will be wrong.
> Do NOT keep v2/v3/v4 masters. Keep ONLY the files below.

## 1. REPO STRUCTURE TO CREATE (exact)

```
ekota.store/
├── CLAUDE.md                                  // v5 FINAL CONSOLIDATED - MASTER, highest authority
├── docs/
│   ├── IMPLEMENTATION_NOTES.md                // v3 + v3.1 + v3.2 + v3.3 + v3.4 CONSOLIDATED
│   ├── DECISIONS.md                           // empty at start, user adds only after approval
│   └── PHASE_STATE.md                         // empty at start, AI appends after each phase
├── .env.example                               // from CLAUDE.md Section 13
├── package.json                               // Next.js 14.2.5 pinned
├── prisma/
│   ├── schema.prisma                          // Phase 1 only: see CLAUDE.md Section 7 Phase 1 list
│   └── seed.ts                                // phase-aware, see IMPLEMENTATION_NOTES Section 6A
├── scripts/db/
│   ├── check-postgis-prerequisite.ts          // Step 1
│   └── ensure-postgis.ts                      // Step 3, --phase=1/4/9
├── app/[locale]/...                           // Phase 1: shell only
├── lib/                                       // Phase 1: geo.ts, config/guard.ts, pricing.ts (stub, no grace)
├── messages/bn.json + en.json                 // Phase 1 core strings only
└── tests/                                     // Phase 1 tests listed in CLAUDE.md Phase 1 Accept
```

## 2. CREATE REPO — COPY-PASTE COMMANDS

```bash
# 1. Create repo
mkdir ekota.store && cd ekota.store
git init
git branch -M main

# 2. Create files (copy content from the 2 files delivered in this chat)
# - CLAUDE.md -> copy from ekota.store-CLAUDE-v5-FINAL-CONSOLIDATED.md
# - docs/IMPLEMENTATION_NOTES.md -> copy from ekota.store-IMPLEMENTATION_NOTES-FINAL-CONSOLIDATED.md
mkdir -p docs scripts/db prisma app messages lib tests
touch docs/DECISIONS.md docs/PHASE_STATE.md

# 3. Install Phase 1 deps (pinned)
npm init -y
npm install next@14.2.5 react@18.3.1 react-dom@18.3.1
npm install -D typescript@5.5.4 @types/node @types/react prisma@5.18.0
npm install -D tailwindcss postcss autoprefixer
npm install zod next-intl vitest @ducanh2912/next-pwa
npx tsc --init --strict --noEmit --skipLibCheck
npx tailwindcss init -p

# 4. Env
cp .env.example .env.local
# Edit .env.local: DATABASE_URL, DIRECT_URL, OTP_DEV_BYPASS=false

# 5. DB setup — ORDER IS MANDATORY, do NOT change
npm run db:setup
# db:setup = check-postgis-prerequisite -> prisma migrate deploy -> ensure-postgis --phase=1
# In dev without PostGIS: Step 1 warns, Step 2 succeeds, Step 3 skips geography, app still boots with Haversine

# 6. Run
npm run dev
npm test
```

## 3. HOW CLAUDE.md WORKS AS CODE

AI must follow this protocol at start of EVERY phase (copy this into Cursor / Claude prompt):

```
Read in order:
1. CLAUDE.md (v5 FINAL CONSOLIDATED)
2. docs/IMPLEMENTATION_NOTES.md (v3 + patches consolidated)
3. docs/DECISIONS.md
4. docs/PHASE_STATE.md

Precedence: CLAUDE.md v5 > IMPLEMENTATION_NOTES > DECISIONS.md (if DECISIONS.md conflicts with CLAUDE.md, flag it, do NOT silently override).
If requirement is ambiguous or conflicts with Locked Decision 1-22, STOP and ask ONE precise question.
Execute ONLY Phase N. Do NOT build Phase N+1 code.
After phase: output (a) file tree, (b) how to run/test, (c) acceptance checklist, (d) known gaps, (e) 20-line PHASE_STATE update.
```

## 4. PHASE 1 — WHAT TO BUILD (ONLY THIS, NOTHING ELSE)

**Phase 1 = Foundation + Data Layer. ONE phase, 3 sub-steps in order.**

- 1.1: Repo, Next 14.2.5, Tailwind/shadcn, next-intl bn/en core strings, .env.example, lint/test/CI
- 1.2: Prisma schema (Phase 1 models ONLY, see below) + migrations + PostGIS 3-step setup + lib/geo.ts + CountryConfig/PricingConfig/AppConfig seed + OTP guard
- 1.3: Seed script (phase-aware) + home shell that reads CountryConfig

**Phase 1 models ONLY:** CountryConfig, PricingConfig, AppConfig, User, SavedAddress, OtpCode (table only), AuditLog (minimal), WebhookEvent (table only), infra_setup_log
**DO NOT build in Phase 1:** Store, Category, Listing, KycRecord, CommissionEntry, Payout, PartnerStoreSetup logic, Provider models. Those are Phase 3/4/8/9.

**Phase 1 Accept (must all pass):**
- App runs, locale bn/en switch works
- DB migrates, seed works, CountryConfig/PricingConfig readable
- Geo query returns distance via BOTH PostGIS and Haversine (parity <0.1%)
- SavedAddress: create with pin / without pin, both-or-neither rule, lat/lng range, 1 default per user, User FOR UPDATE
- OTP_DEV_BYPASS block test passes (production + true = refuse to boot)
- PostGIS CI: Prisma migrations contain NO PostGIS SQL in non-comment SQL

## 5. FILE HYGIENE (NON-NEGOTIABLE)

- Delete v2/v3/v4 masters. Keep ONLY CLAUDE.md v5 FINAL CONSOLIDATED.
- Delete old IMPLEMENTATION_NOTES v1/v2/v3 separate files. Keep ONLY docs/IMPLEMENTATION_NOTES.md consolidated.
- Never add a decision to docs/DECISIONS.md without user approval.
- PartnerStoreSetup Section 3B (ACTIVE|EXPIRED) is STILL pending approval. Do NOT implement it until user says YES.
- If AI proposes a new architecture / business rule, STOP. That is the biggest risk now, not business model.

## 6. START PHASE 1 PROMPT (copy-paste to AI)

```
Execute Phase 1 per CLAUDE.md v5 FINAL CONSOLIDATED + docs/IMPLEMENTATION_NOTES.md
+ docs/DECISIONS.md + docs/PHASE_STATE.md.
Precedence: CLAUDE.md > IMPLEMENTATION_NOTES.
Build ONLY Phase 1 (1.1 -> 1.2 -> 1.3). Do NOT build Phase 2+ code.
First: restate scope in 5 lines, list files to create/modify, then build.
```

END BOOTSTRAP


---

## 📘 PART 1B — MASTER CONTEXT PROMPT v5 FINAL CONSOLIDATED (Refined + Optimized)

# MASTER CONTEXT PROMPT — ekota.store v5 FINAL CONSOLIDATED (Refined + Optimized)
> HOW TO USE: Save as `CLAUDE.md` in repo root. Delete v2/v3/v4 files, keep ONLY this v5 as master.
> Companion: `docs/IMPLEMENTATION_NOTES.md` (v3 + v3.1 + v3.2 + v3.3 + v3.4 consolidated, clarifications only).
> Create 2 more files: `docs/DECISIONS.md` and `docs/PHASE_STATE.md` (empty at start, AI updates PHASE_STATE every phase, DECISIONS only with user approval).
> Build ONE phase at a time. Say: "Execute Phase N". Never build everything in one reply.
> At start of every phase: read `CLAUDE.md` + `docs/IMPLEMENTATION_NOTES.md` + `docs/DECISIONS.md` + `docs/PHASE_STATE.md` first, then restate scope in 5 lines, then list files to create/modify.
> PRECEDENCE: `CLAUDE.md v5 > IMPLEMENTATION_NOTES (v3.4 > v3.3 > v3.2 > v3.1 > v3) > DECISIONS.md`. If IMPLEMENTATION_NOTES conflicts with CLAUDE.md, CLAUDE.md wins, flag it. IMPLEMENTATION_NOTES contains NO new Locked Decisions. PartnerStoreSetup 3B is PENDING approval, do NOT implement until user approves.
> This v5 is FINAL. All ambiguities from v4 review are locked in Section 16, Decisions 18-22. Patches v3.1-v3.4 are already integrated below as clarifications, marked [PATCH].

---

## 0. ROLE + CONTEXT PROTOCOL (NON-NEGOTIABLE)

You are Principal Full-Stack Architect + Senior Engineer. Build ekota.store exactly as specified.

1. Strict TypeScript (`"strict": true`, no `any`). Validate every input with Zod.
2. Money = integer cents (USD cents) in DB and code. Never float for money. Convert cents to major unit only at UI.
3. Money calculations ONLY in `/lib/pricing.ts` (base price), `/lib/promo.ts` (discount), `/lib/commission.ts` (commission). [PATCH v3.1-C] Grace period + visibility logic lives in `/lib/billing/subscription.ts`, NOT in pricing.ts. UI, components, API routes, other lib files must NEVER contain money math.
4. Never hardcode secrets, prices, percentages, radii, thresholds. Config lives in `PricingConfig`, `CountryConfig`, `AppConfig` or env.
5. Every money, auth, verification, webhook path must be idempotent, logged in `AuditLog`, covered by tests.
6. Authorization: central `can(user, action, resource)` in `lib/policy.ts`. No role checks scattered. Row-level checks on every server action / API route.
7. UI strings: `next-intl`, Bengali (bn, default) + English (en) in `/messages`. Phase 1: setup + core strings only. From Phase 2: no hardcoded UI strings. Missing string -> log to `missing-i18n.log`, fallback to English, do NOT block phase.
8. Mobile-first. Low-end Android, slow networks in BD. Targets: Lighthouse mobile >=90 non-map, >=80 map. JS <150KB gzipped non-map, <250KB map. Google Maps JS lazy-loaded, never initial bundle.
9. After each phase: (a) file tree, (b) how to run/test, (c) acceptance checklist, (d) known gaps, (e) 20-line update for `docs/PHASE_STATE.md`.
10. If requirement ambiguous or conflicts with LOCKED DECISION Sec 16, STOP, ask ONE precise question. Do NOT guess. Do NOT silently change locked decision.
11. NEW DECISION RULE: If you need a new decision for `docs/DECISIONS.md`, STOP and ask first. Never append on your own. Propose in phase report, only user adds it.
12. Never modify previous phase files unless current phase explicitly requires it. Never refactor unrelated code.

CONTEXT RETENTION: `docs/DECISIONS.md` = decisions. If prompt and DECISIONS.md conflict, DECISIONS.md wins, flag it. `docs/PHASE_STATE.md` = memory. Append after each phase: built, decisions, open, next phase input. Do NOT re-derive pricing/discount/commission from memory. Read from `PricingConfig` / `DECISIONS.md`.

---

## 1. PRODUCT VISION + CANONICAL STORY

ekota.store = pure digital bridge. Does NOT hold stock, does NOT process buyer-seller payments, does NOT escrow. Connects Buyers <-> Sellers, Buyers/Sellers <-> Service Providers, Platform <-> Partners/Promoters.

Buyer-seller deal, negotiation, delivery coordination happen directly over WhatsApp deep links `wa.me`. Revenue = annual subscriptions only (Sellers, Partners, optionally premium Providers future), via Lemon Squeezy (merchant of record).

CANONICAL STORY (must pass E2E Phase 6): Shamim abroad in Malaysia searches "শুকনা ঝাল", filters Local within 5km of family home in BD, sees grocers with price/distance/delivery time, taps WhatsApp to order, hires verified errand-runner Shihab. Grocer Shawon has store set up by Partner Farhan.

Seed must include: Shamim (buyer), Shawon (seller, grocer, Mirpur), Farhan (partner), Shihab (provider, errand-runner, Mirpur), plus seed locations Sec 14.

---

## 2. SCALING: LOCAL -> NATIONAL -> INTERNATIONAL

### 2.1 Three tiers, one engine

| Tier | Scope | Geo | Example |
|---|---|---|---|
| LOCAL | LOCAL | Radius 3/5/10/25km, max 50km | Grocer near Shamim family home |
| NATIONAL | NATIONAL | No radius. Filter `countryCode`. Sort rating/recency/text rank | Dhaka seller shipping all BD |
| INTERNATIONAL | INTERNATIONAL | No radius. Filter `shippingRegions` contains buyer country OR `shipsWorldwide`. Show shipping note, currency, est days | BD seller shipping to Malaysia |

One search engine. Scope decides radius, not separate codebase.

**SCOPE INCLUSION RULE (LOCKED, Decision 19):** Store has EXACTLY ONE `scope` (not array). Hierarchical visibility: LOCAL visible ONLY LOCAL within radius. NATIONAL visible NATIONAL nationwide + LOCAL if within radius. INTERNATIONAL visible INTERNATIONAL + NATIONAL + LOCAL if within radius. Price by single scope. If seller wants LOCAL+NATIONAL, upgrade to NATIONAL. Do NOT implement `scopes[]`.

### 2.2 v1 vs schema-ready

**v1 (BD only):** Country BD only. `CountryConfig` 1 row BD. Scopes LOCAL+NATIONAL. INTERNATIONAL UI hidden `internationalEnabled=false`. Language bn default, en secondary. Currency Billing USD, Display BDT. KYC manual + abstraction, default `manual`. Payout manual monthly, bank/bKash/Payoneer. OTP WhatsApp Cloud API first, SMS fallback.

**v2 (International storefront):** Turn on `internationalEnabled`. No core migration. Add CountryConfig rows, shippingRegions, currency display conversion (display only, billing USD).

**v3 (International sellers):** Sellers `countryCode != BD`. Per-country KYC doc types, per-country payout methods.

### 2.3 Scaling primitives (must exist Phase 1)

1. Geo hierarchy: Country -> Region -> City -> Area -> Point (lat/lng). Store/Provider always `countryCode, region, city, areaText` + `latitude, longitude` + DB-only `location geography` (see Sec 5, PATCH).
2. `CountryConfig`: `countryCode PK, defaultLocale, currencyDisplay, phonePrefix, kycDocTypes[], payoutMethods[], legalFlags Json, enabled`. Never hardcode +880/BDT.
3. `PricingConfig` keyed (countryCode, scope): Sec 4.1 + 4.3, incl PARTNER row.
4. Feature flags in `AppConfig`: `internationalEnabled, providerPaidEnabled, smsFallbackEnabled, manualKycOnly, usePostgis, medicalListingRequiresApproval`.
5. Modular monolith: One Next.js repo, strict boundaries. Modules: sellers, partners, promoters, providers, search, billing, kyc, notifications. Import only via `index.ts` public API. No cross-module Prisma queries outside `lib/db` or owning module.
6. No premature microservices. Scale by indexes + PostGIS + caching + ISR first. Split only with decision log entry.

---

## 3. ROLES

| Role | Can do | Verification | Pays |
|---|---|---|---|
| BUYER | Search, filter, WhatsApp, favorites, review after contact | WhatsApp OTP + Email | No |
| SELLER | Store, products, services, marketing kit, delivery mode | NID/Passport + live face | Annual sub |
| PARTNER | Create/manage client stores via token, earn margin | NID/Passport + live face | Annual sub |
| PROMOTER | Promo code, 10% recurring commission, payout | NID/Passport + face + payout details | No |
| SERVICE_PROVIDER | List services, rates, coverage, availability | NID/face or legal docs + rep face | Free launch (`providerPaidEnabled` future) |
| ADMIN | Review verifications, moderate, config, payouts, reports | Internal | No |

Auth via `can(user, action, resource)` (RBAC + ownership). Row-level checks everywhere.

---

## 4. BUSINESS RULES + MONEY (INTEGER CENTS)

All numbers defaults in `PricingConfig` / `AppConfig`, editable by admin. Code reads config, never hardcodes. Calculations ONLY in pricing/promo/commission (+ billing/subscription for grace, PATCH).

### 4.1 Seller subscription (annual, USD) + Partner price

`PricingConfig` 4 rows BD: LOCAL 1000 cents ($10), NATIONAL 1500 cents ($15), INTERNATIONAL 2000 cents ($20), PARTNER 1000 cents ($10). [PATCH] Always write as cents + $: `1000 cents ($10)`, never bare `1000`. Seed comment: `// 1000 = $10, NOT $1000`.

Seller price: `PricingConfig.priceCents(countryCode, store.scope)`. Billing via Lemon Squeezy variants (one per scope + PARTNER). Webhook single source of truth for `subscriptionStatus`. Partner price in same PricingConfig table as PARTNER row, no separate table.

### 4.2 Promo resolution
```
resolvePromo(code, scope, countryCode):
  p = PromoCode.find(code); reject if !p or !active or expiresAt<now or uses>=maxUses
  baseCents = PricingConfig.priceCents(countryCode, scope)
  if PROMOTER: sellerDiscountPct = cfg.promoterSellerDiscount (default 25, 20-30)
  if PARTNER: sellerDiscountPct = 0
  sellerPaysCents = round(baseCents * (1 - sellerDiscountPct/100))
```

### 4.3 Partner economics
- Partner buys Partner sub: `PricingConfig` PARTNER (1000/yr BD) -> `tokenCode`.
- Partner sets up client store: pays `baseCents * (1 - partnerDiscountPct/100)` (default 45%, 40-50, per-partner override). Partner collects full price OFFLINE. Profit = `baseCents * partnerDiscountPct/100`. Platform never touches offline payment.
- Track: `PartnerStoreSetup { partnerId, storeId, paidByPartnerCents, listPriceCents, partnerMarginCents }`. [PATCH] Status proposal `ACTIVE|EXPIRED` + `renewedAt` + `renewalCount` is PENDING APPROVAL, do NOT implement until user approves. Keep current status until approval.
- Flow: `DRAFT_BY_PARTNER -> CLIENT_INVITED -> CLIENT_KYC_PENDING -> ACTIVE`. Ownership = seller (invited via WhatsApp/email magic link). Partner = `StoreManager` (edit catalog, cannot change payout/ID). Cannot go public until seller KYC verified.
- Renewal: bulk renew via single checkout.

### 4.4 Promoter commission
- 10% of amount actually paid (net tax/fees as reported by LS) on initial + every renewal while verified + code active.
- Ledger: `CommissionEntry { promoterId, storeId, subscriptionEventId (unique), amountCents, status: PENDING->APPROVED->PAID|REVERSED }`. [PATCH v3.4] `subscriptionEventId` unique + `ON CONFLICT DO NOTHING`. Downstream idempotency mandatory.
- Hold 30 days before APPROVED. Refund/chargeback -> REVERSED.
- Payout: monthly batch when approved >= threshold (default 2000 cents = $20). Methods bank/bKash/Payoneer (encrypted details). Mark PAID with reference. CSV export.
- Self-referral: cannot use own code, nor code tied to same NID hash / phone / payout account. No device fingerprint as sole signal.

### 4.5 Idempotency + Webhook (PATCH v3.1-v3.4 integrated)
- Verify HMAC signature (`X-Signature`, raw body) FIRST. If fail -> 401, do NOT insert event, do NOT log payload. Log only sanitized `eventId, type, ip` (max 100 chars, strip newlines).
- If pass -> Insert `WebhookEvent` with `ON CONFLICT (id) DO NOTHING`. `id` = LS event ID String PK, NOT UUID.
- Atomic claim: `UPDATE ... SET status='PROCESSING', token=newUUID, startedAt=NOW() WHERE id=$1 AND status='PENDING' RETURNING *`. If 0 rows, another worker claimed, do nothing.
- Per-event token: Bulk stale recovery must SELECT IDs first, then claim each with NEW UUID, never same token for all.
- Final update MUST check BOTH: `WHERE id=$1 AND status='PROCESSING' AND token=$2`. If 0 rows, claim lost, do NOT overwrite.
- Retry: `retryCount` starts 0, max 5, `nextRetryAt = NOW() + POWER(2, retryCount+1) minutes` (0->2min, 1->4min, 2->8min, 3->16min, 4->32min). FAILED->PROCESSING claim only if `retryCount<5 AND nextRetryAt<=NOW()`. Stale PROCESSING >10min can be reclaimed, if retryCount>=5 -> separate update to FAILED with `STALE_CLAIM_EXCEEDED_MAX_RETRIES`.
- Downstream: Side effects + webhook DONE in SAME DB transaction. External actions need separate idempotency key `eventId:actionName` + `ExternalActionLog`.
- Allowlist logging ONLY: `eventId, type, processingStatus, retryCount, errorCode`. Never log payload, phone, bank, full token (only first 8 chars if needed). `lastError` = errorCode only.
- Handle events: verify exact LS event names from LS docs in Phase 5, do NOT guess. (v3 said placeholder names, Phase 5 must verify.)

### 4.6 Subscription lifecycle + Grace (PATCH v3.1-C, v3.2)
`NONE -> ACTIVE -> (PAST_DUE grace 7 days) -> EXPIRED`; `CANCELLED (active until period end)`. EXPIRED: hidden from search, direct link "inactive", data retained 12 months.
- Fields: `pastDueAt?, gracePeriodEndsAt?` (Phase 5). `gracePeriodEndsAt = pastDueAt + graceDays` (AppConfig, default 7). Compute in `lib/billing/subscription.ts`, never pricing.ts/UI.
- First failure only sets `pastDueAt`. Duplicate webhook must NOT reset it (protected by WebhookEvent idempotency + atomic claim).
- Expiry: Cron `/api/cron/expire-subscriptions` sets EXPIRED if `now >= gracePeriodEndsAt`. Visibility must also check: `isVisible = status=ACTIVE AND subStatus IN (ACTIVE, PAST_DUE) AND (subStatus!=PAST_DUE OR now < gracePeriodEndsAt)`. At exactly `gracePeriodEndsAt`, EXPIRED, not visible.

---

## 5. TECH STACK (LOCKED)

- Next.js 14.2.5 App Router, RSC, Server Actions, TS strict
- Tailwind + shadcn/ui + lucide-react, `next-intl` bn/en
- PostgreSQL + PostGIS (Supabase) + Prisma 5.x. [PATCH v3.2-v3.4] Prisma schema has ONLY `latitude Float?, longitude Float?`. `location geography` is DB-only, NOT in Prisma schema, managed by infra scripts, accessed ONLY via `lib/geo.ts` + `$queryRaw` parameterized. Never raw PostGIS SQL in components/actions/other lib.
- Auth: Auth.js v5 custom credentials WhatsApp OTP (WhatsApp Cloud API template) + Google OAuth / email magic link. SMS fallback `OtpChannel`.
- Payments: `@lemonsqueezy/lemonsqueezy.js`
- Maps: Google Maps JS + Places + Geocoding (lazy, Distance Matrix only detail, cache)
- KYC: `KycProvider` abstraction, v1 = `manual` (admin review). No custom face ML.
- Storage: S3-compatible (R2 / Supabase), private KYC bucket signed URLs, public store media
- QR: `qrcode` (server SVG/PNG). PDF: `@react-pdf/renderer` or HTML print CSS
- PWA: `@ducanh2912/next-pwa`. TWA: Asset Links + Bubblewrap
- Queue/cron: Vercel Cron or Inngest. Rate limit: Upstash Redis. Observability: Sentry. Analytics: Plausible/PostHog
- Testing: Vitest, Playwright, Prisma test DB

**PostGIS 3-Step Setup (PATCH v3.3-v3.4, mandatory order):**
1. `check-postgis-prerequisite.ts` — check extension exists. Production + missing -> throw `POSTGIS_REQUIRED_IN_PRODUCTION`, stop. Dev + missing -> warn, continue.
2. `prisma migrate deploy` — Prisma migrations must contain NO PostGIS SQL in non-comment SQL. CI parses SQL, strips comments, checks for `geography` type, `ST_*`, `CREATE EXTENSION postgis`. Comment-only mention passes.
3. `ensure-postgis.ts --phase=1|4|9` — phase-scoped ONLY. Phase 1 only SavedAddress, Phase 4 only Store, Phase 9 only Provider. Missing phase arg -> throw. Log to `infra_setup_log { step, status, environment, errorDetails }`.

---

## 6. FOLDER STRUCTURE

```
/app/[locale]/(public) page, search/, store/[slug]/, provider/[id]/, p/[promoCode]/
  /(auth) login/, verify-otp/, onboarding/
  /(dashboard) buyer/, seller/{store,products,delivery,marketing-kit,subscription}/
    partner/{stores,token,earnings}/, promoter/{codes,earnings,payout}/
    provider/{profile,services,availability}/
  /admin verifications/, users/, payouts/, config/, reports/, audit/
/api webhooks/lemonsqueezy/, search/, qr/[slug]/, kyc/webhook/, cron/*, otp/{send,verify}/
/components ui/, marketplace/, forms/, maps/, marketing/
/modules sellers/, partners/, promoters/, providers/, search/, billing/, kyc/, notifications/ (each: index.ts, schema.ts, actions.ts, lib.ts, tests/)
/lib db.ts, auth.ts, policy.ts, pricing.ts, promo.ts, commission.ts, billing/subscription.ts, geo.ts, search.ts, whatsapp.ts, lemonsqueezy.ts, kyc/, otp/, storage.ts, audit.ts, ratelimit.ts, validators/, i18n/
/prisma schema.prisma, migrations/, seed.ts
/messages bn.json, en.json
/docs DECISIONS.md, PHASE_STATE.md, IMPLEMENTATION_NOTES.md
/tests unit/, e2e/
```
Every file 1-line purpose comment. No dead code. No TODO without issue note.

---

## 7. DATABASE SCHEMA (PRISMA — Phase-wise, see IMPLEMENTATION_NOTES)

Enums: `Role, MarketScope(LOCAL|NATIONAL|INTERNATIONAL), PricingScope(LOCAL|NATIONAL|INTERNATIONAL|PARTNER), VerificationStatus(NOT_STARTED|PENDING|IN_REVIEW|VERIFIED|REJECTED), SubStatus(NONE|ACTIVE|PAST_DUE|CANCELLED|EXPIRED), StoreStatus(DRAFT|DRAFT_BY_PARTNER|CLIENT_INVITED|CLIENT_KYC_PENDING|ACTIVE|SUSPENDED), CommissionStatus(PENDING|APPROVED|PAID|REVERSED), PayoutStatus, PromoType(PARTNER|PROMOTER), ListingType(PRODUCT|SERVICE)`.

**BILINGUAL (LOCKED Decision 18):** Separate columns, NOT Json: `nameBn, nameEn, descriptionBn, descriptionEn` for Listing/Category/Store. `storeName` single brand name. Helper `getLocalizedName(entity, locale)` in `lib/i18n.ts`, fallback to other language, never empty. Search indexes BOTH nameBn+nameEn into `searchVector`.

Models (id uuid, createdAt, updatedAt, soft-delete deletedAt where relevant):

- **CountryConfig**: countryCode PK, defaultLocale, currencyDisplay, phonePrefix, kycDocTypes[], payoutMethods[], legalFlags Json, enabled
- **PricingConfig**: countryCode, scope PricingScope, priceCents, currencyBilling USD, unique(countryCode, scope). 4 rows BD.
- **AppConfig**: key PK, value Json, description. Flags: internationalEnabled, providerPaidEnabled, promoterSellerDiscount, partnerDiscountDefault, commissionPct, commissionHoldDays, payoutThresholdCents, graceDays, usePostgis, medicalListingRequiresApproval (true)
- **User**: name, email unique verified, whatsappE164 unique verified, locale, role, kycStatus, countryCode, lastLoginAt, blocked
- **KycRecord** (Phase 3): userId, type, docNumberHash (salted, duplicate only), docFileKey, selfieFileKey, providerRef, status, reviewerId, rejectReason, reviewedAt. Encrypt at rest. Never expose raw doc number.
- **Store** (Phase 4): ownerId, storeName, slug unique, banner/logo, descriptionBn/En, scope SINGLE MarketScope, status, `latitude, longitude` (Prisma) + DB-only `location geography`, countryCode, region, city, areaText, address, deliveryRadiusKm, deliveryMode, shippingRegions[], shipsWorldwide, openingHours Json, whatsappE164, subscriptionStatus, currentPeriodEnd, lsSubscriptionId, qrCodeKey, ratingAvg/Count, managedByPartnerId?, `pastDueAt?, gracePeriodEndsAt?` (Phase 5)
- **StoreManager**: storeId, partnerId, permissions
- **Category** (Phase 4, tree): nameBn/En, slug, parentId?, type PRODUCT|SERVICE
- **Listing** (Phase 4): storeId?|providerId?, type, nameBn/En, descriptionBn/En, priceCents, currencyDisplay, unit, inStock, images[], tags[], `searchVector tsvector` GIN, categoryId
- **PartnerProfile**, **PartnerStoreSetup** (Phase 8, see 4.3), **PromoterProfile**, **PromoCode**, **PromoRedemption** (unique promoCodeId+storeId)
- **CommissionEntry** (Phase 8): promoterId, storeId, subscriptionEventId unique, amountCents, status, holdUntil (createdAt+30d), paidPayoutId?
- **Payout** (Phase 8): promoterId, totalCents, status, method, `payoutDetailsSnapshotEncrypted String?` [PATCH] Format `v1:base64(iv):base64(tag):base64(ciphertext)`, AES-256-GCM app-layer, key `PAYOUT_ENCRYPTION_KEY` outside DB, never log key, decrypt only Admin + AuditLog `VIEW_PAYOUT_DETAILS`, CSV masked `****1234`. Key rotation policy prerequisite before Phase 8.
- **PayoutItem**: payoutId, commissionEntryId unique, amountCents
- **ServiceProviderProfile** (Phase 9): userId, isCorporate, companyName, legalDocKey, categoryId, rateCents, rateUnit, currencyDisplay, lat/lng + DB-only location, countryCode, region, city, coverageRadiusKm, availability Json, activeStatus, kycStatus, ratingAvg/Count, isMedical (bool, requires approval if flag true)
- **ContactEvent, Review, Favorite, Report** (Phase 9): [PATCH] Polymorphic `targetType STORE|PROVIDER + targetId`. No DB FK. Backend MUST validate: target exists, target ACTIVE, Review requires ContactEvent exists, cannot review own store. Tests for all.
- **SavedAddress** (Phase 1): [PATCH] userId FK, label, recipientName?, countryCode, region?, city?, areaText?, address?, `latitude?/longitude?` (both or neither, lat -90..90, lng -180..180), DB-only location, phoneE164?, isDefault (only 1 active default per user). Partial unique index: `CREATE UNIQUE INDEX ... ON SavedAddress(userId) WHERE isDefault=true AND deletedAt IS NULL`. All create/change/delete use `SELECT User FOR UPDATE` first. First address auto-default. Delete default promotes oldest remaining `ORDER BY createdAt ASC, id ASC`. Search with SAVED_ADDRESS requires valid pin + ownership, else `SAVED_ADDRESS_HAS_NO_LOCATION` / `FORBIDDEN`.
- **AuditLog**: actor, action, entity, before/after, ip
- **WebhookEvent** (Phase 1 table, Phase 5 logic): `id String @id` = LS event ID, type, payload Json, processingStatus PENDING|PROCESSING|DONE|FAILED, processingToken String?, processingStartedAt?, lastError?, retryCount Int 0, nextRetryAt?, processedAt?, createdAt. See Sec 4.5.
- **OtpCode**: hashed, expiresAt, attempts
- **Notification**, **ExternalActionLog** (Phase 5): idempotencyKey unique, status, createdAt
- **infra_setup_log**: step, status, environment, errorDetails?, createdAt

Indexes: GiST on geography (via ensure-postgis), GIN on searchVector, Composite (status, subscriptionStatus, scope, countryCode) on Store. Uniques as noted.

---

## 8. CORE ALGORITHMS

### 8.1 Radius search + Geo interface

**Geo interface (mandatory):** All geo in `lib/geo.ts`. No other file calls PostGIS. Repository/service layer does DB writes, geo.ts returns params/validation, never builds SQL string with coordinates.

```
type GeoPoint = { lat, lng }
interface GeoService { searchNearby(params): Promise<SearchResult[]>, distanceKm(a,b): number, boundingBox(center, radius): Box, isPostgisEnabled(): boolean }
```
Selection: If `AppConfig.usePostgis=true` AND extension available -> PostGIS, else fallback. Caller never decides. Both return identical shape, parity <0.1% on seed.

Input: `{ q, lat, lng, radiusKm (3|5|10|25|null), scope, countryCode, kind, categoryId?, sort, page }`.
1. Validate, clamp radius <=50 LOCAL. If scope != LOCAL, ignore radius.
2. PostGIS: `ST_DWithin(location, ST_MakePoint(lng,lat)::geography, radius*1000)` + `ST_Distance`. [PATCH] Parameterized: `ST_SetSRID(ST_MakePoint($1,$2),4326)::geography`, $1=lng, $2=lat. Never concatenate.
3. Fallback: bbox `dLat=r/111.045; dLng=r/(111.045*cos(lat))` -> box filter, then Haversine `d=2R*asin(sqrt(...))`, R=6371.
4. Text: `websearch_to_tsquery` on searchVector + `pg_trgm` + Banglish map ("shukna jhal" -> "শুকনা ঝাল"). No Bengali tsconfig assumption.
5. Only `status=ACTIVE AND subscriptionStatus IN (ACTIVE, PAST_DUE)` + grace check (Sec 4.6). Only inStock unless toggled.
6. NATIONAL: filter countryCode. INTERNATIONAL: shippingRegions contains buyer country OR shipsWorldwide. Apply Scope Inclusion 2.1.
7. Ranking "best": `score=0.40*textRank+0.25*(1-dist/radius)+0.20*ratingBayes+0.10*recency+0.05*verifiedBoost`, `ratingBayes=(C*m+sum)/(C+n)`, C=5. NATIONAL/INTERNATIONAL distance=0, redistribute to text+rating. No sponsored ordering.
8. Return: localized name, price, distanceKm 1 decimal LOCAL only, estDeliveryMinutes LOCAL `15+distance*6` labeled "estimate", NATIONAL/INTL "delivery estimate on WhatsApp", open-now, WhatsApp link.
9. Cache popular 60s (lat/lng rounded 3 decimals). Cursor pagination 20/page.

### 8.2 WhatsApp deep link (`lib/whatsapp.ts`)
- Normalize E.164 (default CountryConfig.phonePrefix, BD +880, strip leading 0). `https://wa.me/<e164>?text=<encoded>`
- Templates bn/en: product inquiry, delivery, service hire, live-location.
- On click: log ContactEvent non-blocking `sendBeacon`, then open. Never expose raw phone in HTML before click for logged-out bots (server action/token).

### 8.3 Marketing kit
- QR `https://ekota.store/store/{slug}?utm_source=qr&utm_medium=print`, error correction H.
- A4/A3 poster PDF, business card 90x55mm PDF bleed 3mm, PNG social. Server-side on demand, cached by store version hash. Only if subscriptionStatus=ACTIVE.

### 8.4 KYC state machine
`NOT_STARTED -> PENDING -> IN_REVIEW -> VERIFIED|REJECTED`. Steps: doc -> OCR/validation -> liveness/face -> duplicate docNumberHash -> admin queue low-confidence. Re-submit max 3/30 days. Cannot publish/earn until VERIFIED. Signed URLs, AuditLog, retention configurable (delete raw images X days after verification, keep hash+status).

### 8.5 OTP + WhatsApp OTP RISK + DEV BYPASS HARD BLOCK
6-digit, store `sha256(code+salt)`, 5-min expiry, max 5 attempts, resend cooldown 60s, rate limit phone+IP+device. WhatsApp template first, SMS after 2 failed deliveries. Email magic link.

RISK: WhatsApp Auth template needs Meta approval 1-3 days, cannot change without re-approval. Use fixed template Day 1. Cost per OTP. Delivery can fail if blocked/no WhatsApp. SMS fallback must be tested. Auth.js v5 Credentials + WhatsApp OTP NOT built-in, implement send->store hash->verify->session. Do NOT use Auth.js email provider as shortcut.

**OTP_DEV_BYPASS HARD BLOCK (LOCKED Decision 22):** If `NODE_ENV=production AND OTP_DEV_BYPASS=true`, app MUST refuse to boot. Fail fast: "OTP_DEV_BYPASS must be false in production". Startup check in `lib/otp/` + unit test. Warning-only NOT allowed. Dev bypass code `123456` only, logged `DEV_BYPASS_USED`.

### 8.6 Provider matching
Same radius engine, filter category, activeStatus, availability, `coverageRadiusKm >= distance`. Show rate, rating, verified, WhatsApp. Seller hire = pick -> WhatsApp (no in-app payment). If `isMedical=true AND medicalListingRequiresApproval=true`, hidden until admin approves.

---

## 9. API / SERVER ACTION CONTRACT

Each: Zod, auth guard, rate limit, AuditLog where mutates, typed `{ ok:true, data } | { ok:false, error:{code,message} }`.

- `POST /api/otp/send|verify`
- `GET /api/search`, `/api/store/[slug]`, `/api/provider/[id]`
- Actions: `createStore, updateStore, upsertListing, deleteListing, setDeliveryMode, submitKyc, applyPromo, createCheckout, createPartnerStore, inviteClient, bulkRenewStores, createPromoCode, requestPayout, submitReview, reportEntity`
- `POST /api/webhooks/lemonsqueezy`, `POST /api/kyc/webhook`
- `GET /api/qr/[slug]`, `GET /api/marketing-kit/[slug]?type=poster|card`
- Cron: `/api/cron/expire-subscriptions`, `/approve-commissions`, `/renewal-reminders`, `/purge-kyc`, `/retry-webhooks`
- Admin: approve/reject KYC, suspend, edit Pricing/Country/AppConfig, payout batch, CSV export

---

## 10. UI / UX

Design: clean, trustworthy, warm. Deep green/teal + gold. Touch >=44px. Hind Siliguri bn + Inter en. Dark mode. Skeleton. Offline fallback.

Pages: Home (search bar voice `webkitSpeechRecognition` bn-BD, scope tabs Local|National|Global, radius slider LOCAL only, toggle Products|Services|Stores, use my location + manual pin + saved addresses, category chips, featured, how-it-works), Search results (list/map, filters price/open/verified/self-delivery/rating, cards distance/price/WhatsApp), Store page (banner, verified, hours, delivery, catalog, reviews, WhatsApp, share, report, JSON-LD LocalBusiness, OG), Provider page, Seller dashboard (onboarding KYC->store->catalog->subscribe->kit, CRUD bulk CSV, image compression, delivery, sub status, analytics views/clicks/scans), Partner dashboard (token, stores status/renewal, wizard, margin, bulk renew), Promoter dashboard (codes, redemptions, ledger, payout), Admin (KYC queue side-by-side, reports, config, payouts, audit). Accessibility WCAG AA, keyboard, both languages. Empty/error/loading every screen.

---

## 11. SECURITY, PRIVACY, COMPLIANCE (BLOCKERS)

- OWASP ASVS L2: CSRF, strict CSP, secure cookies, sanitization, file validation, malware scan hook.
- Encrypt KYC (AES-256-GCM, KMS/env). Least-privilege DB. Row-level. Admin MFA.
- Privacy: consent before biometrics. Policy/terms/refund pages. Export/delete flow. Minimal retention.
- Trust: disclaimer connector not party. Prohibited-items. Report/takedown. Fake-store heuristics (duplicate NID hash/phone, abnormal contacts).
- Rate limits search/OTP/promo.

LEGAL BLOCKERS — Do NOT launch without lawyer sign-off:
1. BD Data Protection Act 2023 + Biometric: NID+selfie+face = biometric. Explicit consent bn/en, retention, deletion, storage location (BD vs abroad). Manual KYC does NOT remove.
2. Doctor/Medical: BMDC/DGDA compliance. `medicalListingRequiresApproval=true` default. Do NOT auto-publish doctor without admin.
3. Payout/FX: Commission via bKash/bank, Partner offline margin may trigger Bangladesh Bank FX/tax. Need guidance threshold, withholding, Payoneer allowed?
4. WhatsApp + OTP consent: Opt-in required. OTP template must include opt-out. No marketing on OTP template.

---

## 12. PERFORMANCE, SEO, PWA/TWA

- ISR store/provider (revalidate on edit via tag), edge cache search suggestions, `next/image` AVIF/WebP, font subsetting.
- Sitemap (stores+providers+categories per locale), hreflang, robots, structured data.
- PWA: manifest bn/en, maskable icons, offline shell, install prompt after 2nd visit, background-sync reviews/favorites.
- TWA: `/.well-known/assetlinks.json`, Bubblewrap, .aab checklist, Play Store notes.
- Budget Sec 0 Rule 8. If map route cannot meet, document gap, do NOT silently drop.

---

## 13. ENV VARS (`.env.example`)

`DATABASE_URL, DIRECT_URL, AUTH_SECRET, AUTH_GOOGLE_ID/SECRET, WHATSAPP_PHONE_ID, WHATSAPP_TOKEN, WHATSAPP_OTP_TEMPLATE, WHATSAPP_OTP_ENABLED, SMS_FALLBACK_KEY, GOOGLE_MAPS_BROWSER_KEY, GOOGLE_MAPS_SERVER_KEY, LEMONSQUEEZY_API_KEY, LEMONSQUEEZY_STORE_ID, LEMONSQUEEZY_WEBHOOK_SECRET, LS_VARIANT_LOCAL/NATIONAL/INTERNATIONAL/PARTNER, KYC_PROVIDER, KYC_API_KEY, KYC_WEBHOOK_SECRET, S3_ENDPOINT/BUCKET_PUBLIC/BUCKET_PRIVATE/KEYS, KYC_ENCRYPTION_KEY, PAYOUT_ENCRYPTION_KEY, UPSTASH_REDIS_URL/TOKEN, SENTRY_DSN, NEXT_PUBLIC_APP_URL, OTP_DEV_BYPASS`.

Comment: `OTP_DEV_BYPASS must be false in production, app will refuse to boot if true in production`.

---

## 14. TESTING + SEED LOCATIONS

- Unit: promo, partner margin, commission (hold/reversal), Haversine/bbox, ranking, E.164, OTP expiry/attempts, policy, geo PostGIS vs fallback parity, OTP_DEV_BYPASS block, retry timing `POWER(2,retryCount+1)`, webhook token claim, SavedAddress validation.
- Integration: webhook idempotency (replay 3x), signature rejection, subscription lifecycle, crash-after-side-effect (exactly 1 CommissionEntry).
- E2E (Playwright): Shamim story. Partner creates store -> client KYC -> live. Promoter code -> purchase -> commission PENDING -> APPROVED after hold.
- Seed (LOCKED Decision 21, do NOT invent others):
  1. Mirpur-10, Dhaka — 23.8375, 90.3570 — 12 stores, 8 providers. Shamim family home. Shawon grocer + Shihab provider here.
  2. Uttara Sector 7 — 23.8729, 90.3967 — 10 stores, 6 providers.
  3. Dhanmondi 27 — 23.7465, 90.3760 — 8 stores, 6 providers.
  Total 30 stores, 20 providers, 1 admin, 2 partners, 2 promoters, bilingual categories. Listings must have BOTH nameBn+nameEn.

---

## 15. BUILD PHASES (one at a time, stop + report after each)

**Phase 1 — Foundation + Data Layer (ONE phase, 3 sub-steps):**
- 1.1 Repo, Next 14.2.5, Tailwind/shadcn, i18n core strings, .env.example, lint/test, CI.
- 1.2 Prisma schema (Phase 1 models ONLY: CountryConfig, PricingConfig, AppConfig, User, SavedAddress, OtpCode table-only, AuditLog minimal, WebhookEvent table-only, infra_setup_log) + migrations + PostGIS 3-step (check -> migrate -> ensure-postgis --phase=1) + `lib/geo.ts` + CountryConfig/PricingConfig (4 rows BD) + AppConfig seed incl `medicalListingRequiresApproval=true` + OTP guard.
- 1.3 Seed (phase-aware: Phase 1 prod seed ONLY Country/Pricing/AppConfig, NO Category, NO Admin default password — Admin via separate provisioning) + home shell reading CountryConfig.
*Accept:* runs, locale works, DB migrates, seed works, geo distance via both paths, Config readable, OTP_DEV_BYPASS block test passes, Prisma migrations contain NO PostGIS SQL, SavedAddress rules pass.

**Phase 2 — Auth:** WhatsApp OTP + email/Google, sessions, policy.ts, onboarding, rate limits. WhatsApp risk checklist 8.5.
*Accept:* OTP lifecycle, unauthorized blocked, SMS fallback tested.

**Phase 3 — KYC:** abstraction `manual`, upload, state machine, admin queue, audit.
*Accept:* unverified cannot publish, duplicates flagged.

**Phase 4 — Stores:** CRUD, slug, map pin, listings nameBn/En, categories, media, delivery modes. Single scope. + `ensure-postgis --phase=4` + Category seed (Phase 4 only).
*Accept:* seller can publish (draft until sub+KYC).

**Phase 5 — Billing:** LS checkout, promo, webhook handler (Sec 4.5, verify LS event names from docs), lifecycle + grace + cron expiry + retry cron. PARTNER row for Partner checkout.
*Accept:* replayed webhooks harmless, expired hidden, retry + token + downstream idempotency tests pass.

**Phase 6 — Search:** Sec 8.1, home/results/map, store/provider pages, SEO. Scope inclusion.
*Accept:* Shamim story passes, p95 search <400ms seed.

**Phase 7 — WhatsApp + kit:** 8.2, 8.3, contact events, analytics.
*Accept:* printable poster/card PDFs, QR lands correct store + UTM.

**Phase 8 — Partners/Promoters:** token, managed stores, ledger, hold/approve/reverse, payout batches, dashboards. Ask approval for PartnerStoreSetup 3B before implementing.
*Accept:* money math to cent, self-referral blocked, payout encryption format + rotation policy.

**Phase 9 — Providers:** profile individual/corporate, matching, hire flow, reviews. Medical requires approval. + `ensure-postgis --phase=9`.
*Accept:* matching works, hire via WhatsApp, medical hidden until approved.

**Phase 10 — Admin, hardening, PWA/TWA, launch:** reports/moderation, security, Lighthouse, Play Store, backups, monitoring, legal pages, legal blockers Sec 11 signed off.
*Accept:* Legal cleared, Lighthouse met.

---

## 16. LOCKED DECISIONS (DO NOT CHANGE WITHOUT ASKING)

1. `APP_DOMAIN = ekota.store`. Intentional spelling. Do NOT autocorrect to ekota.store.
2. Money = integer cents, billing USD, display BDT BD. No floats.
3. DB = Supabase Postgres + PostGIS. Prisma 5.x. Next.js 14.2.5 pinned.
4. Promoter = 10% recurring. New seller discount promoter code = 25% (20-30 AppConfig).
5. Partner discount default 45% (40-50). Partner collects full price offline.
6. Providers free launch. `providerPaidEnabled=false`.
7. Commission hold 30 days. Payout threshold 2000 cents ($20). Payouts manual monthly.
8. KYC = abstraction, v1 = `manual` + admin. No custom ML.
9. No in-app buyer payments, ever. Platform shows "estimated" delivery only.
10. Country default BD. Phone +880, display BDT, billing USD.
11. Base = BD only, LOCAL+NATIONAL. INTERNATIONAL hidden `internationalEnabled=false` but schema-ready.
12. Self-referral = NID hash + phone + payout account. No device fingerprint sole signal.
13. No device fingerprint as primary anti-fraud, ever.
14. Money calculations ONLY in pricing/promo/commission (+ billing/subscription for grace). No money math elsewhere.
15. Geo logic ONLY in `lib/geo.ts`. No PostGIS SQL outside geo.ts (repository uses geo.ts params, parameterized).
16. Phase 1 is ONE phase. Do NOT split into 1a/1b as separate phases. Sub-steps are execution order inside Phase 1.
17. New decisions require user approval before adding to DECISIONS.md.
18. Bilingual: separate columns `nameBn+nameEn`, `descriptionBn+descriptionEn`. No Json. Helper `getLocalizedName()` in `lib/i18n.ts`. Fallback to other language.
19. Store scope: ONE scope, not array. Hierarchical visibility. Price by single scope.
20. Partner pricing in `PricingConfig` as `scope=PARTNER` (1000 cents BD). No separate Partner pricing table.
21. Seed locations LOCKED: Mirpur-10, Uttara Sector 7, Dhanmondi 27, counts 12/10/8 stores, 8/6/6 providers. Do NOT invent others.
22. OTP_DEV_BYPASS: If `NODE_ENV=production AND OTP_DEV_BYPASS=true`, app MUST refuse to boot. Fail fast. Dev code `123456` only.

---

## 17. CODE + OUTPUT STYLE

- Small pure functions for money/geo in `/lib` with unit tests. UI never business math.
- Prefer Server Components. Client only for interactivity (map, slider, QR print, OTP input).
- Consistent error codes. User-facing errors localized.
- Conventional Commits. One PR-sized change per step.
- Every file 1-line purpose comment. No dead code, no TODO without issue note.

**START NOW:** Reply only with: (1) 10-line confirmation, (2) questions from Sec 16 blocking Phase 1 (if any), (3) then begin Phase 1.


---

## 📗 PART 2 — IMPLEMENTATION NOTES (v3 + v3.1 + v3.2 + v3.3 + v3.4 Consolidated)

# IMPLEMENTATION NOTES — ekota.store v5 Companion (FINAL CONSOLIDATED v3.4)
> Companion to `CLAUDE.md` v5 FINAL CONSOLIDATED. Do NOT treat as new master.
> This file consolidates: IMPLEMENTATION_NOTES v3 + PATCH v3.1 (6 fixes) + PATCH v3.2 (3 clarifications) + PATCH v3.3 (4 corrections) + PATCH v3.4 (final details).
> Do NOT keep separate v1/v2/v3 patch files in repo. Keep ONLY this file as `docs/IMPLEMENTATION_NOTES.md`.
> Precedence: `CLAUDE.md v5 > this file (v3.4 > v3.3 > v3.2 > v3.1 > v3)`. If this file conflicts with CLAUDE.md, CLAUDE.md wins. No new Locked Decisions here. PartnerStoreSetup 3B is PENDING approval, do NOT implement until user approves.
> Save as `docs/IMPLEMENTATION_NOTES.md`.

---

## 1. CONFIG + POSTGIS (v3 + v3.1 + v3.2 + v3.3 + v3.4)

**Single source:** `AppConfig.usePostgis` only. No env `USE_POSTGIS`. `lib/geo.ts` decides: if false -> Haversine, if true -> check extension, if exists -> PostGIS, else warn `POSTGIS_NOT_AVAILABLE_FALLBACK_USED` + Haversine. Caller never decides.

**3-Step Deployment (mandatory order, PATCH v3.3-v3.4):**
1. `check-postgis-prerequisite.ts` — check extension. Production + missing -> throw `POSTGIS_REQUIRED_IN_PRODUCTION`, stop. Dev + missing -> warn, continue. Creates NO columns.
2. `prisma migrate deploy` — Prisma migrations must contain NO PostGIS SQL in non-comment SQL. CI parses SQL, strips `--` and `/* */` comments, checks for `geography` type, `ST_MakePoint/ST_SetSRID/ST_DWithin/ST_Distance`, `CREATE EXTENSION postgis`. If found -> fail `POSTGIS_SQL_IN_PRISMA_MIGRATION`. Comment-only mention passes.
3. `ensure-postgis.ts --phase=1|4|9` — phase-scoped ONLY. Phase 1 only SavedAddress, Phase 4 only Store, Phase 9 only Provider. Missing `--phase` -> throw `MISSING_PHASE_ARGUMENT`. Never run Phase 4 setup in Phase 1. Log to `infra_setup_log { step, status, environment, errorDetails }`, one row per execution.

**Prisma schema:** ONLY `latitude Float?, longitude Float?`. `location geography` is DB-only, NOT in Prisma schema, accessed via `$queryRaw` parameterized only. See CLAUDE.md Sec 5.

**Coordinate order:** ALWAYS `ST_MakePoint(longitude, latitude)`. Test Mirpur-10 (23.8375, 90.3570) asserts `ST_X=90.3570, ST_Y=23.8375`.

**Responsibility split (PATCH v3):** `geo.ts` = selection, distance, bbox, search query building (params), validation. Repository/service = INSERT/UPDATE, calls geo.ts for params. Components never raw SQL, never build `ST_MakePoint` string. Parameterized: `ST_SetSRID(ST_MakePoint($1,$2),4326)::geography`, $1=lng, $2=lat. Never `` `ST_MakePoint(${lng},${lat})` ``. `geo.ts` returns `[lng, lat]` params, not SQL string.

---

## 2. STORE LIFECYCLE + GRACE (v3 + v3.1-C + v3.2)

**StoreStatus:** `DRAFT | DRAFT_BY_PARTNER | CLIENT_INVITED | CLIENT_KYC_PENDING | ACTIVE | SUSPENDED`. Two axes: `status` (published?) vs `subscriptionStatus` (paid?). Visible ONLY if `status=ACTIVE AND subscriptionStatus IN (ACTIVE, PAST_DUE) AND grace not expired`.

**Grace (PATCH v3.1-C, v3.2):** Fields `pastDueAt?, gracePeriodEndsAt?` (Phase 5). `gracePeriodEndsAt = pastDueAt + graceDays` (AppConfig, default 7). Compute in `lib/billing/subscription.ts`, NEVER pricing.ts/UI. First failure only sets pastDueAt, duplicate must NOT reset (protected by WebhookEvent). Cron `/api/cron/expire-subscriptions` sets EXPIRED if `now >= gracePeriodEndsAt`. Visibility: `now < gracePeriodEndsAt` if PAST_DUE. At exactly `gracePeriodEndsAt`, EXPIRED. LS event names must be verified from LS docs in Phase 5, do NOT guess.

---

## 3. DATABASE — PHASE-WISE + WEBHOOK + PAYOUT + POLYMORPHIC

**Phase 1 ONLY:** CountryConfig, PricingConfig (4 rows BD), AppConfig, User, SavedAddress, OtpCode (table only), AuditLog (minimal), WebhookEvent (table only), infra_setup_log. **Do NOT build Store/Category/Listing/Kyc/Commission/Payout/Provider in Phase 1.**

**Phase 4:** Store, StoreManager, Category, Listing (nameBn/En, descriptionBn/En). Category seed ONLY Phase 4, NOT Phase 1.
**Phase 5:** PromoCode, PromoRedemption, PartnerStoreSetup (table only), Store grace fields.
**Phase 8:** CommissionEntry, Payout, PayoutItem, PartnerStoreSetup logic.
**Phase 9:** ServiceProviderProfile, ContactEvent, Review, Favorite, Report.

**WebhookEvent (PATCH v3.1-v3.4):** `id String @id` = LS event ID (NOT UUID), type, payload Json, processingStatus PENDING|PROCESSING|DONE|FAILED, processingToken String? (UUID, new per claim), processingStartedAt?, lastError (errorCode only), retryCount Int 0, nextRetryAt?, processedAt?, createdAt.
- Order: 1) Verify signature FIRST. Fail -> 401, do NOT insert, do NOT log payload, log only sanitized eventId/type/ip (max 100 chars, strip newlines). 2) Insert `ON CONFLICT DO NOTHING`. 3) Atomic claim `UPDATE ... SET status='PROCESSING', token=newUUID WHERE id=$1 AND status='PENDING'`. 4) Final update MUST check BOTH `status='PROCESSING' AND token=$token`, else claim lost, do NOT overwrite.
- Bulk stale/FAILED: SELECT IDs first, then claim each with NEW UUID, never same token for all. Stale: `PROCESSING AND startedAt < NOW()-10min AND retryCount<5` -> reclaim. If retryCount>=5 -> separate update to FAILED `STALE_CLAIM_EXCEEDED_MAX_RETRIES`.
- Retry: `nextRetryAt = NOW() + POWER(2, retryCount+1) minutes` (0->2, 1->4, 2->8, 3->16, 4->32). Max 5, then manual Admin retry. Cron `/api/cron/retry-webhooks`.
- Downstream idempotency (PATCH v3.4): CommissionEntry `subscriptionEventId @unique` + `ON CONFLICT DO NOTHING`. Subscription update idempotent (same status = no-op, pastDueAt only if NULL). DB side effects + webhook DONE in SAME transaction. External actions need idempotency key `eventId:actionName` + `ExternalActionLog` (unique key).
- Allowlist logging ONLY: `eventId, type, processingStatus, retryCount, errorCode`. Never log payload/phone/bank/full token (only first 8 chars if needed). Delete `sanitizeWebhookLog()` denylist, use allowlist.

**Payout Encryption (PATCH v3.1-F, v3.3):** AES-256-GCM app-layer, format `v1:base64(iv):base64(tag):base64(ciphertext)`. Decrypt checks version, unknown -> throw `UNSUPPORTED_ENCRYPTION_VERSION`. Key `PAYOUT_ENCRYPTION_KEY` outside DB, separate from KYC key, never log. Admin decrypt logged `VIEW_PAYOUT_DETAILS`, CSV masked `****1234`. Key rotation + backup policy prerequisite before Phase 8. Test: raw DB must NOT contain plaintext bank.

**PartnerStoreSetup 3B — PROPOSAL PENDING, DO NOT IMPLEMENT:** Proposal: status `ACTIVE|EXPIRED` only + `renewedAt?` + `renewalCount` + `PartnerStoreRenewal` history. Ask user before implementing. Until approval, keep current status.

**Polymorphic (PATCH v3):** ContactEvent/Review/Favorite/Report: validate targetType STORE|PROVIDER, target exists, target ACTIVE, Review requires ContactEvent, cannot review own. Tests for all.

---

## 4. OTP_DEV_BYPASS

Phase 1: ONLY guard in `lib/config/guard.ts` + 1 test. If `NODE_ENV=production AND OTP_DEV_BYPASS=true`, refuse to boot. Phase 2: full OTP flow + bypass `123456` logged `DEV_BYPASS_USED`.

---

## 5. MONEY OWNERSHIP

| Source | Owns |
|---|---|
| PricingConfig | Base price (country, scope) — LOCAL 1000 ($10), NATIONAL 1500 ($15), INTERNATIONAL 2000 ($20), PARTNER 1000 ($10) |
| AppConfig | Percentages/thresholds/days — promoterSellerDiscount 25, partnerDiscountDefault 45, commissionPct 10, hold 30d, payoutThreshold 2000, graceDays 7 |
| pricing.ts / promo.ts / commission.ts | ONLY calculation, no hardcoded numbers |
| billing/subscription.ts | Grace + visibility |

Rules: No other module reads PricingConfig for math, must call pricing.ts. Never `baseCents*(1-discount/100)` inline. Price in PricingConfig, percent in AppConfig. Display `1000 cents ($10)`, never bare `1000`.

---

## 6. SAVEDADDRESS (v3 + v3.1-D + v3.2 + v3.3 + v3.4)

**Model:** userId, label, recipientName?, countryCode, region?, city?, areaText?, address?, latitude?/longitude?, DB-only location, phoneE164?, isDefault. Indexes (userId,isDefault), GiST location.

**Rules:**
- Create without pin allowed (both null). One only -> reject `INVALID_COORDINATES`. If present, lat -90..90, lng -180..180.
- Search with SAVED_ADDRESS requires valid pin + ownership (`userId==currentUser`), else `SAVED_ADDRESS_HAS_NO_LOCATION` / `FORBIDDEN`. Do NOT fallback to current location.
- Partial unique index: `CREATE UNIQUE INDEX ... ON SavedAddress(userId) WHERE isDefault=true AND deletedAt IS NULL`. Guarantees AT MOST 1 default, NOT at least 1. 0 addresses -> 0 defaults is valid.
- Locking: Create/Change-default/Delete ALL start with `SELECT User WHERE id=$1 FOR UPDATE`. Different users parallel, same user serialized.
- First address auto-default even if client says false. Delete default promotes oldest remaining `ORDER BY createdAt ASC, id ASC` in same transaction. Delete must check `id + userId + deletedAt IS NULL`, else ROLLBACK + `ADDRESS_NOT_FOUND_OR_NOT_OWNED`, do NOT change other addresses.
- Privacy: Never expose another user's addresses. Seller sees only text buyer shares via WhatsApp.

**Seed Safety (PATCH v3):** Phase 1 prod seed ONLY Country/Pricing/AppConfig. Phase 4 Category seed. Admin via separate provisioning, NO default password. Dev seed `seed.dev.ts` checks `if production throw`, contains Shamim/Mirpur. Prod seed test must check STRUCTURED data (SavedAddress 0 rows, Country 1, Pricing 4), NOT text grep for `Mirpur-10` (comments allowed).

---

## 7. FUTURE — MULTI-COUNTRY, OWNERSHIP, WHATSAPP

- Every Store/Listing/Provider query filters `countryCode` first. Phone uses CountryConfig.phonePrefix, currency uses currencyDisplay, KYC doc types use kycDocTypes, retention strictest law.
- Store ownership ALWAYS seller, never Partner. Partner = StoreManager, cannot change ownerId/payout/NID. Partner expiry loses edit rights, seller store stays ACTIVE if seller sub ACTIVE. Seller expiry hides store regardless Partner.
- Search/store pages must work WITHOUT WhatsApp. WhatsApp = `wa.me` deep link, ContactEvent non-blocking sendBeacon. Fallback phone/email if WhatsApp down. OTP WhatsApp + SMS + Email independent. Feature flag `whatsappEnabled`.

---

## 8. HOW TO USE

1. Keep `CLAUDE.md` v5 as master. This file is companion.
2. Phase 1 prompt: "Execute Phase 1 per CLAUDE.md + this file Sec 1,2,4,6 + Phase 1 models only"
3. Phase 5 prompt: "Execute Phase 5 per CLAUDE.md + this file Sec 2,3 (webhook, grace). Verify LS event names from docs."
4. Phase 8 prompt: "Execute Phase 8 per CLAUDE.md + this file Sec 3 (payout, PartnerStoreSetup 3B pending approval)."
5. If conflict, CLAUDE.md wins. Flag it. Do NOT silently override.

**END — No new Locked Decisions. All patches are clarifications, except 3B proposal pending.**




---

## 🔁 PART 3 — FINAL GUARDRAILS (READ BEFORE CLAIMING PROJECT COMPLETE)

1. Project is COMPLETE only when: Phase 1-10 ALL DONE + PHASE_STATE shows 10/10 DONE + Self-Test passes for Phase 10 + Legal Blockers (Section 11) signed off + Lighthouse targets met.
2. NEVER claim COMPLETE if any Phase Acceptance is untested.
3. NEVER delete this file. NEVER split this file. NEVER create a second master.
4. If user says "start Phase N", you MUST re-read this file + DECISIONS.md + PHASE_STATE.md first, even if you just read it.
5. If context is lost (new session), Step 0.1-0.2 is your recovery: re-read this file, re-read PHASE_STATE, continue from NEXT in PHASE_STATE, do NOT restart from scratch.
6. PartnerStoreSetup 3B remains PENDING until user explicitly says YES. Do NOT implement it on your own.

**END OF SINGLE FILE — ekota.store MASTER CONTEXT PROMPT v5 FINAL (COMPLETE)**
> Save this file as CLAUDE.md first. Then execute Phase 1. Then Phase 2... Phase 10. One phase at a time. Self-test every time. Never lose context.

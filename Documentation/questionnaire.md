# Questionnaire.md — Rahal رحّال

> This file captures all decisions made, open questions, and owner preferences gathered during the design and build conversation. Use this as a reference when continuing development in a new chat.

---

## 1. App Identity

| Question | Answer |
|---|---|
| App name | **Rahal رحّال** (meaning: traveler in Arabic) |
| Previous name | AutoTrack (discarded — name already taken) |
| Support email | support@rahal.app |
| Target market | Egypt (primary), Arabic-speaking markets (secondary) |
| App language | English + Arabic (full toggle, RTL support) |
| App type | Mobile-optimized PWA → later wrapped as APK (Capacitor) |

---

## 2. Logo & Branding

| Question | Answer |
|---|---|
| Logo status | **Not yet finalized** |
| Designs explored | 12 total (6 dark, 6 light versions) |
| Dark versions liked | Options 1 (road horizon), 3 (location pin), 4 (Arabic-first), 5 (speedometer) |
| Light versions shown | A (lavender steering wheel), B (soft white pin), C (clean white speedometer), D (warm gold Arabic), E (sky blue road), F (mint green speed ring) |
| Key requirement | The word "Rahal" must appear **inside** the logo icon |
| Both scripts required | Yes — "Rahal" in English AND "رحّال" in Arabic both inside the logo |
| Current placeholder | Simple purple square with serif R (to be replaced once logo is chosen) |
| **Action needed** | Owner to pick final logo from light or dark round, or request new variations |

---

## 3. Features & Scope

| Question | Answer |
|---|---|
| Core feature set | Vehicle profiles, activity logging, reminders, reports, media, AI assistant |
| AI logging | Yes — Claude API, natural language input, confirms before saving |
| Voice input | UI microphone button present, full voice-to-text to be implemented natively |
| Multiple vehicles | Yes — Free: 1, Basic: 2, Pro: unlimited |
| Trip distance logger | Yes — via Google Maps Distance Matrix API (Pro feature) |
| GPS auto-tracking | Not in PWA — requires native app (Capacitor); planned for later |
| Media types | Photos, videos, audio recordings (Pro feature) |
| Export formats | CSV (implemented), PDF (planned for production release) |
| Mileage reminders | Yes — Basic and Pro tiers only |
| Date reminders | Yes — all tiers including Free |

---

## 4. Registration & Trial

| Question | Answer |
|---|---|
| Trial duration | 30 days, full Pro access |
| Credit card required for trial | No |
| Trial abuse prevention method | Hash lock on: email + phone + plate + VIN + device fingerprint |
| OTP verification | Yes — phone number verified via OTP at registration |
| Demo OTP code | 1234 (for testing only) |
| Registration steps | 3 steps: Personal info → Vehicle info → Registration document upload |
| Vehicle registration photo | Required upload (can be skipped for now) — no color reference (Egypt-specific) |
| Fields that lock trial | Phone, email, plate number, VIN, device fingerprint |

---

## 5. Subscription & Payments

| Question | Answer |
|---|---|
| Free tier | Yes — permanent, limited features, shows ads |
| Basic tier | 19 EGP/month or 155 EGP/year |
| Pro tier | 49 EGP/month or 399 EGP/year |
| Yearly discount | 32% saving |
| Payment provider | Paymob (primary) — supports Fawry, Visa, Mastercard, Meeza, mobile wallets |
| Backup payment | Fawry standalone (for users without bank cards) |
| Stripe | Not recommended — difficult to set up from Egypt without foreign entity |
| Paymob fee | ~2.5% per transaction |
| Ads in free tier | Yes — planned via auto shop / fuel brand partnerships |
| Break-even estimate | ~200 subscribers at 49 EGP = ~10,000 EGP/month |

---

## 6. Publishing & Distribution

| Question | Answer |
|---|---|
| APK export from Claude | Not possible — requires Capacitor + Android Studio |
| Recommended wrapper | Capacitor by Ionic (free, wraps HTML/JS into native APK + IPA) |
| Web hosting | Vercel or Netlify (free tier) |
| Google Play cost | $25 one-time developer fee |
| Apple App Store cost | $99/year developer account |
| iOS build requirement | Mac + Xcode required (or MacStadium cloud Mac) |
| PWA option | Yes — can be installed on phone via Chrome → "Add to Home Screen" |
| Review times | Google Play: 3–7 days · App Store: 1–3 days |

---

## 7. Backend & Infrastructure

| Question | Answer |
|---|---|
| Current storage | sessionStorage (demo only — not persistent across sessions) |
| Recommended backend | Firebase (Auth + Firestore + Storage) |
| OTP provider (production) | Twilio or Vonage (server-side, not client-side) |
| Rate limiting (production) | Cloudflare Workers or Firebase Security Rules |
| API key storage | Server-side only — never in the app bundle |
| SSL | Let's Encrypt via Vercel (free) |
| Database encryption | Firebase handles encryption at rest |

---

## 8. Security Decisions

| Question | Answer |
|---|---|
| Client-side sanitization | Yes — all inputs sanitized (XSS, script injection, HTML stripping) |
| OTP lockout | 3 attempts → 5-minute cooldown |
| Session timeout | 30 minutes of inactivity → auto logout |
| Odometer validation | Cannot enter reading lower than previous |
| File size limits | Photos: 5MB · Media: 20MB |
| AI prompt injection | System prompt includes anti-injection rules |
| AI output sanitized | Yes — before display and before saving to logs |
| Trial hash storage | sessionStorage (demo) → Firestore in production |

---

## 9. Design & UX Decisions

| Question | Answer |
|---|---|
| Dark mode | Yes — full dark mode toggle in Settings |
| RTL Arabic layout | Yes — `direction: rtl` applied when Arabic selected |
| Bottom navigation | 6 tabs: Home · Log · AI · Alerts · Reports · Account |
| Settings location | Gear icon top-right of Account screen |
| Feedback section | Yes — star rating (1–5) + text box inside Settings |
| FAQ | Yes — 4 expandable questions inside Settings |
| Contact Us | Yes — email + phone inside Settings |
| Onboarding walkthrough | Suggested but not yet built |
| Quick-add widget | Suggested but not yet built |
| Shared vehicle mode | Suggested (family sharing) — not yet built |

---

## 10. Open Questions (Needs Owner Decision)

| # | Question | Status |
|---|---|---|
| 1 | Which logo design to use? | ⏳ Pending owner selection |
| 2 | Dark or light logo background preferred? | ⏳ Pending — both rounds shown |
| 3 | Should ads be implemented now or after launch? | ⏳ Not decided |
| 4 | Which ad partners to approach? (auto shops, fuel brands) | ⏳ Not decided |
| 5 | Is a family/shared vehicle mode needed at launch? | ⏳ Not decided |
| 6 | Should onboarding walkthrough be built before launch? | ⏳ Not decided |
| 7 | Firebase or alternative backend? | ⏳ Not decided |
| 8 | Will owner handle Paymob integration or hire developer? | ⏳ Not decided |
| 9 | Google Maps API key — does owner have one? | ⏳ Not confirmed |
| 10 | Will owner publish under personal name or company? | ⏳ Not decided |

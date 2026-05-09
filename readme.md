# Rahal رحّال — Vehicle Manager App

![React](https://img.shields.io/badge/React-18-61DAFB?logo=react&logoColor=white)
![Vite](https://img.shields.io/badge/Vite-5-646CFF?logo=vite&logoColor=white)
![TypeScript](https://img.shields.io/badge/TypeScript-5-3178C6?logo=typescript&logoColor=white)
![Firebase](https://img.shields.io/badge/Firebase-planned-FFCA28?logo=firebase&logoColor=black)
![Vercel](https://img.shields.io/badge/Deployed_on-Vercel-000000?logo=vercel&logoColor=white)
![License](https://img.shields.io/badge/License-Proprietary-red)

---

## Overview

Rahal (رحّال) is an Egyptian-market smart vehicle management app built as a mobile-optimized PWA (Progressive Web App) using React. It helps car owners track fuel, maintenance, repairs, insurance, and registration — all powered by an AI assistant that lets users log data by simply describing what happened in natural language.

---

## App Name

- **English:** Rahal
- **Arabic:** رحّال
- **Meaning:** Traveler (Arabic)
- **Support email:** <support@rahal.app>

---

## Tech Stack

- **Frontend:** React (artifact), mobile-optimized PWA
- **AI:** Claude Sonnet 4 via Anthropic API (`claude-sonnet-4-20250514`)
- **Payments:** Paymob (Egyptian market — Fawry, Visa, Mastercard, Meeza)
- **Planned backend:** Firebase (auth, Firestore, storage)
- **Planned deployment:** Vercel (web) + Capacitor (Android APK + iOS IPA)

---

## Subscription Tiers

| Feature | Free | Basic (19 EGP/mo) | Pro (49 EGP/mo) |
|---|---|---|---|
| Vehicles | 1 | 2 | Unlimited |
| Activity logging | ✅ | ✅ | ✅ |
| Basic reminders (date) | ✅ | ✅ | ✅ |
| Mileage-based reminders | ❌ | ✅ | ✅ |
| Full reports & insights | ❌ | ❌ | ✅ |
| Media uploads | ❌ | ❌ | ✅ |
| CSV / PDF export | ❌ | ❌ | ✅ |
| AI assistant | ❌ | ❌ | ✅ |
| Trip distance logger | ❌ | ❌ | ✅ |
| History | 30 days | 6 months | Unlimited |
| Ads | ✅ | ❌ | ❌ |

**Yearly pricing:** Basic 155 EGP/yr · Pro 399 EGP/yr (32% saving)

**Free trial:** 30 days of full Pro access. No credit card required. Trial is locked to phone number + email + plate number + VIN + device fingerprint to prevent abuse.

---

## App Screens

1. **Registration** (3-step)
   - Step 1: Personal info (name, email, phone, password) + OTP phone verification
   - Step 2: Vehicle info (make, model, year, plate, VIN) + car photo upload
   - Step 3: Vehicle registration document upload

2. **Home / Dashboard**
   - Vehicle switcher tabs
   - Car photo/icon display
   - 4 key metrics: odometer, fuel economy, monthly spend, reminders due
   - Recent activity feed

3. **Activity Log**
   - Filter by type: fuel, oil, tires, repair, insurance, registration
   - Add entries manually via modal
   - Odometer validation (cannot go backwards)
   - Input sanitization on all fields

4. **AI Assistant**
   - Real Claude API-powered chat
   - Natural language logging (e.g. "Filled up 45L at 18 EGP, odometer 87420")
   - AI parses and returns structured log entry for user confirmation
   - Rate-limited (20 messages/minute)
   - All AI output sanitized before saving

5. **Reminders & Alerts**
   - Color-coded: Red (urgent/overdue) · Amber (upcoming) · Green (all good)
   - Mileage-based triggers (Pro/Basic)
   - Date-based triggers (all plans)
   - Progress bars showing proximity to trigger

6. **Reports & Insights**
   - Time range toggle: 1M · 3M · 6M · 1Y · All time
   - Bar chart dynamically updates — wider view for 1Y shows all 12 months
   - All 4 metrics (total spend, economy, fill-ups, service events) recalculate per selected range
   - Cost breakdown by category with percentage bars
   - AI-generated insight card
   - CSV export includes the selected range in the filename (Pro)
   - PDF export (planned for production)
   - One full year of data pre-loaded so reports look realistic across all time ranges

7. **Account**
   - 4 sub-tabs: Profile · Vehicle · Media · Plan
   - Profile photo upload
   - Car photo upload
   - Media gallery (photos, videos, audio) — Pro feature
   - Subscription plan display with trial countdown
   - Settings drawer (gear icon, top-right — accessible from any account sub-tab):
     - Language toggle: English ↔ Arabic (full RTL layout applied instantly)
     - Dark / Light mode toggle with smooth animation
     - FAQ (4 questions, expandable)
     - Feedback (star rating + text)
     - Contact us (email + phone)

8. **Subscription Screen**
   - Monthly / Yearly billing toggle
   - 3 plan cards: Free · Basic · Pro
   - Paymob payment integration (planned)

---

## Security Features

### Client-Side Layers (Implemented)

**1. Input Sanitization**
- Strip HTML/script tags from all text inputs
- Prevent XSS (cross-site scripting) attacks
- Validate all fields before saving (type, length, format)

**2. Phone Number Validation**
- Enforce Egyptian format only (01x xxxx xxxx)
- Block fake/malformed numbers

**3. Rate Limiting (UI side)**
- Lock OTP attempts after 3 wrong tries (5-minute cooldown)
- Lock login after 5 failed attempts with countdown timer

**4. Trial Abuse Prevention**
- Hash and store all 5 identifiers (phone + email + plate + VIN + device fingerprint)
- Block registration if any identifier matches an existing trial

**5. Session Security**
- Auto-logout after 30 minutes of inactivity
- Session token expiry

**6. Data Validation**
- Reject impossible values (odometer going backwards, negative costs, future dates)
- Max character limits on all fields

**7. AI Security**
- System prompt includes anti-injection rules
- All AI responses sanitized before display or storage
- Rate-limited to 20 messages per minute

**8. Media Security**
- Photos max 5MB, media max 20MB
- Filenames sanitized on upload

### What Requires a Real Backend

| Threat | Solution |
|---|---|
| API key theft | Store Claude/Paymob keys server-side only — never in the app |
| Man-in-the-middle | HTTPS + SSL pinning (done via Capacitor) |
| Database breach | Encrypt all user data at rest (Firebase/Supabase handles this) |
| Account takeover | Server-side OTP with Twilio/Vonage — not client-side |
| Brute force | Server-side rate limiting (Cloudflare, Firebase rules) |
| Payment fraud | Never touch card data — Paymob handles PCI compliance |
| Reverse engineering | Code obfuscation when building APK (ProGuard) |
| Root/jailbreak detection | Capacitor plugin: `cordova-plugin-root-detection` |

### Security Stack

| Layer | Tool | Cost |
|---|---|---|
| Auth & OTP | Firebase Authentication | Free |
| Database rules | Firestore Security Rules | Free |
| API protection | Cloudflare Workers | Free tier |
| Payment security | Paymob (PCI-DSS compliant) | % per transaction |
| SSL | Let's Encrypt via Vercel | Free |
| Key storage | Firebase Environment Variables | Free |

---

## Localization

- **Languages:** English, Arabic
- **Arabic:** Full RTL layout applied via `direction: rtl`
- **All UI strings** stored in `STRINGS.en` and `STRINGS.ar` objects
- Language preference saved to session storage

---

## Logo & Branding

- **Full logo:** Road/journey icon with "Rahal" in English + "رحّال" in Arabic
- **App icon:** Gradient purple background with a stylized R incorporating road lines — visible in the Plans tab
- **Logo placement:** Top bar, subscription screen, account/plan tab, splash screen

### Color Palette

```text
Primary:   #6C5CE7 (purple)
Success:   #00B894 (green)
Warning:   #EF9F27 (amber)
Danger:    #E24B4A (red)
Dark bg:   #0f0f14
Light bg:  #F5F5F7
Top bar:   #1a1a2e
```

---

## Getting Started (Local Development)

**Prerequisites:** Node.js 18+

```bash
# Install dependencies
npm install

# Start dev server
npm run dev
```

The app runs at `http://localhost:5173`.

### Environment Variables

Copy `.env.example` to `.env.local` and fill in your key:

```bash
cp .env.example .env.local
```

| Variable | Required | Description |
|---|---|---|
| `VITE_ANTHROPIC_API_KEY` | Pro feature | Anthropic API key for the AI assistant |

> **Note:** The AI assistant currently calls the Anthropic API directly from the browser. For production, this should be proxied through a backend (e.g. a Vercel Edge Function) to keep the API key server-side.

---

## Deployment (Vercel)

1. Push this repo to GitHub.
2. Import it in the [Vercel dashboard](https://vercel.com/new).
3. Vercel auto-detects Vite — no framework override needed.
4. Add `VITE_ANTHROPIC_API_KEY` under **Settings → Environment Variables**.
5. Deploy.

The `vercel.json` at the repo root handles SPA routing (all paths fall back to `index.html`).

---

## Project Structure

```text
rahal/
├── autotrack_app.tsx   # Main React app (single-file component)
├── src/
│   └── main.tsx        # React entry point
├── index.html          # HTML shell
├── vite.config.ts      # Vite build config
├── tsconfig.json       # TypeScript project references
├── tsconfig.app.json   # App TypeScript config
├── tsconfig.node.json  # Vite/Node TypeScript config
├── vercel.json         # Vercel SPA rewrite rules
└── .env.example        # Environment variable template
```

---

## Roadmap

### v1.0 (Current — MVP)
- [x] Full PWA with React + Vite
- [x] All 8 app screens
- [x] AI assistant (Claude Sonnet 4)
- [x] Subscription tier system
- [x] Full dark mode
- [x] Arabic/English localization with RTL
- [x] Client-side security layers
- [x] Paymob integration design

### v1.1 (Next)
- [ ] Firebase backend (auth, Firestore, storage)
- [ ] Server-side OTP via Twilio/Vonage
- [ ] Vercel Edge Function as API proxy (keep keys server-side)
- [ ] Cloudflare rate limiting

### v1.2
- [ ] Capacitor build — Android APK
- [ ] PDF export
- [ ] Push notifications for reminders

### v2.0
- [ ] iOS IPA via Capacitor
- [ ] Trip distance logger
- [ ] Full media gallery (photos, videos, audio)
- [ ] Advanced AI insights

---

## License

This project is proprietary software. All rights reserved. Unauthorized copying, distribution, or use is strictly prohibited.

---

## Acknowledgements

- [Anthropic](https://anthropic.com) — Claude Sonnet 4 AI API
- [Paymob](https://paymob.com) — Egyptian payment gateway
- [Firebase](https://firebase.google.com) — Planned auth & database
- [Vercel](https://vercel.com) — Hosting & deployment
- [Capacitor](https://capacitorjs.com) — Native mobile builds
- [Vite](https://vitejs.dev) — Frontend build tooling

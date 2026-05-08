# Rahal رحّال — Vehicle Manager App

## Overview
Rahal (رحّال) is an Egyptian-market smart vehicle management app built as a mobile-optimized PWA (Progressive Web App) using React. It helps car owners track fuel, maintenance, repairs, insurance, and registration — all powered by an AI assistant that lets users log data by simply describing what happened in natural language.

---

## App Name
- **English:** Rahal
- **Arabic:** رحّال
- **Meaning:** Traveler (Arabic)
- **Support email:** support@rahal.app

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
   - Time range toggle: 1M · 3M · 6M · 1Y · All
   - Cost breakdown by category with percentage bars
   - Monthly fuel spend bar chart
   - AI-generated insight card
   - CSV export (Pro)
   - PDF export (planned for production)

7. **Account**
   - 4 sub-tabs: Profile · Vehicle · Media · Plan
   - Profile photo upload
   - Car photo upload
   - Media gallery (photos, videos, audio) — Pro feature
   - Subscription plan display with trial countdown
   - Settings drawer (gear icon top-right):
     - Language toggle: English ↔ Arabic (full RTL support)
     - Dark / Light mode toggle
     - FAQ (4 questions, expandable)
     - Feedback (star rating + text)
     - Contact us (email + phone)

8. **Subscription Screen**
   - Monthly / Yearly billing toggle
   - 3 plan cards: Free · Basic · Pro
   - Paymob payment integration (planned)

---

## Security Features (Implemented)

| Layer | Implementation |
|---|---|
| Input sanitization | All text fields strip HTML, script tags, special chars |
| Phone validation | Egyptian format only: 01x xxxx xxxx |
| Email validation | Regex format check |
| Password policy | Minimum 8 characters |
| Plate/VIN validation | Length and format checks |
| OTP brute-force protection | Locked after 3 wrong attempts (5-min cooldown) |
| Login rate limiting | UI-level lockout with countdown |
| Trial abuse prevention | Hashes: email + phone + plate + VIN + device fingerprint |
| Odometer validation | Cannot log a reading lower than previous |
| Date validation | Future dates blocked on log entries |
| File size limits | Photos max 5MB, media max 20MB |
| Session timeout | Auto-logout after 30 minutes of inactivity |
| AI prompt injection prevention | System prompt includes anti-injection rules |
| AI output sanitization | All AI responses sanitized before display/storage |
| AI rate limiting | 20 messages per minute max |
| Filename sanitization | Media filenames sanitized on upload |
| Character limits | All fields have max character limits |

**Note:** Production security also requires server-side enforcement via Firebase Security Rules, Cloudflare rate limiting, and server-side OTP (Twilio/Vonage). The above covers the client-side layer.

---

## Localization
- **Languages:** English, Arabic
- **Arabic:** Full RTL layout applied via `direction: rtl`
- **All UI strings** stored in `STRINGS.en` and `STRINGS.ar` objects
- Language preference saved to session storage

---

## Logo Status
- Logo designs have been explored across 2 rounds (dark and light versions)
- 6 concepts: Steering wheel, Location pin, Speedometer, Arabic-first, Road perspective, Speed ring
- **Owner is still deciding** — logo not yet finalized
- Once chosen, logo will be applied to: top bar, subscription screen, account/plan tab, splash screen

---

## Color Palette
```
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

```
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

Thanks
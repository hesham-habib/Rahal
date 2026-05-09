# Plan.md — Rahal رحّال
## Development Checklist

> ✅ Done · 🔄 In progress · ⏳ Pending decision · 🔧 Needs building · 👤 Owner action required

---

## PHASE 1 — Design & Concept ✅ Complete

- [x] App name decided: Rahal رحّال
- [x] Subscription model designed (Free / Basic 19 EGP / Pro 49 EGP)
- [x] Feature set defined across all 5 areas
- [x] UI mockup created (6 screens)
- [x] Frontend built in React (PWA)
- [x] All 6 screens implemented and functional
- [x] Dark mode implemented
- [x] Arabic / English language toggle with RTL
- [x] 3-tier subscription screen with monthly/yearly toggle
- [x] 30-day free trial system with abuse prevention
- [x] Registration flow (3 steps + OTP)
- [x] Security layer (sanitization, validation, rate limiting, session timeout)
- [x] AI assistant (Claude API — natural language logging)
- [x] Reports with time range toggle (1M/3M/6M/1Y/All)
- [x] CSV export
- [x] Reminders with mileage + date triggers and progress bars
- [x] Media gallery (photos, videos, audio)
- [x] Settings drawer (language, dark mode, FAQ, feedback, contact)
- [x] Profile photo upload
- [x] Car photo upload
- [x] Logo exploration (12 designs across 2 rounds)

---

## PHASE 2 — Finalization 🔄 In Progress

### Owner must do 👤
- [ ] **Pick final logo** from the designs shown (dark or light round, A–F)
- [ ] Confirm app color scheme preference (current: purple #6C5CE7)
- [ ] Decide on ads: include at launch or add later?
- [ ] Decide on family/shared vehicle mode: needed at launch?
- [ ] Decide on onboarding walkthrough: needed before launch?
- [ ] Register Google account for Google Play ($25 one-time)
- [ ] Register Apple Developer account ($99/year) — needs Mac or MacStadium
- [ ] Get Google Maps API key (for trip distance logger)
- [ ] Create Paymob merchant account at paymob.com
- [ ] Decide: publish under personal name or register a company?

### Claude will do once logo is chosen 🔧
- [ ] Apply final logo to: top bar, subscription screen, account tab, splash/loading screen
- [ ] Apply logo as app icon (rounded square format for stores)

---

## PHASE 3 — Production Features 🔧 To Build

### Claude will build
- [ ] **PDF export** — branded report with charts (requires a PDF library like jsPDF)
- [ ] **Onboarding walkthrough** — first-time user tips overlay (3–4 steps)
- [ ] **Quick-add fuel button** — one-tap shortcut on Home screen
- [ ] **Trip distance logger** — enter start/end location, Maps calculates distance and adds to odometer
- [ ] **Voice-to-text input** — Web Speech API for the AI screen microphone button
- [ ] **Notification center** — inbox of past alerts and reminders
- [ ] **Cost per km metric** — total cost ÷ odometer delta
- [ ] **Shared vehicle mode** — multiple users log to the same car
- [ ] **Offline mode** — cache data locally, sync when online (PWA service worker)

### Owner must arrange 👤
- [ ] Set up Firebase project (free tier)
  - Firebase Authentication (phone OTP)
  - Firestore database
  - Firebase Storage (for media/photos)
- [ ] Set up Twilio or Vonage for production OTP SMS
- [ ] Set up Cloudflare account for rate limiting and DDoS protection
- [ ] Get Google Maps API key and enable Distance Matrix API

---

## PHASE 4 — Backend Integration 🔧 To Build

- [ ] Replace sessionStorage with Firebase Firestore
- [ ] Replace client-side OTP mock with Firebase Auth phone verification
- [ ] Move Claude API calls to a server-side proxy (Firebase Cloud Function or Vercel Edge Function) so API key is never exposed in the app
- [ ] Move Paymob API calls server-side
- [ ] Implement Firebase Security Rules to enforce plan-based access
- [ ] Store trial identifier hashes in Firestore (not sessionStorage)
- [ ] Implement server-side rate limiting via Firebase or Cloudflare
- [ ] Set up Firebase Storage rules for media uploads
- [ ] Add root/jailbreak detection (Capacitor plugin) for native app

---

## PHASE 5 — Publishing 🔧 To Do

### Android (Google Play)
- [ ] Install Capacitor: `npm install @capacitor/core @capacitor/android`
- [ ] Build APK: `npx cap add android` → open in Android Studio → generate signed APK
- [ ] Create Google Play Console account ($25)
- [ ] Upload APK + screenshots + description + privacy policy
- [ ] Submit for review (3–7 days)

### iOS (App Store)
- [ ] Install Capacitor iOS: `npx cap add ios`
- [ ] Open in Xcode (Mac required) → build IPA
- [ ] Create App Store Connect listing
- [ ] Submit for review (1–3 days)

### Web (PWA)
- [ ] Deploy to Vercel: connect GitHub repo → auto-deploy
- [ ] Add `manifest.json` for PWA installability
- [ ] Add service worker for offline support
- [ ] Test "Add to Home Screen" on Android Chrome + iOS Safari

---

## PHASE 6 — Marketing & Monetization 🔧 To Plan

- [ ] Set up Paymob recurring subscription billing
- [ ] Define ad partners (auto shops, fuel stations, tire brands in Egypt)
- [ ] Create app store listing assets:
  - [ ] App icon (final logo in 1024×1024 px)
  - [ ] 5 screenshots per store (phone mockups)
  - [ ] Short description (80 chars)
  - [ ] Full description (4000 chars)
  - [ ] Privacy policy page (required by both stores)
- [ ] Create social media presence (Facebook + Instagram for Egypt market)
- [ ] Plan launch offer (e.g. "First 100 users get 3 months Pro free")
- [ ] Set up analytics (Firebase Analytics or Mixpanel)
- [ ] Set up crash reporting (Firebase Crashlytics)

---

## Priority Order Recommendation

```
1. ✅ Pick the logo  (owner)
2. ✅ Apply logo to app  (Claude)
3. ✅ Set up Firebase  (owner)
4. ✅ Move API keys server-side  (Claude + owner)
5. ✅ Implement real OTP via Firebase Auth  (Claude + owner)
6. ✅ Set up Paymob  (owner)
7. ✅ Build PDF export + trip logger  (Claude)
8. ✅ Wrap app with Capacitor → APK  (owner + developer)
9. ✅ Publish to Google Play  (owner)
10. ✅ Publish to App Store  (owner)
```

---

## Estimated Costs at Launch

| Item | Cost |
|---|---|
| Google Play developer account | $25 one-time |
| Apple Developer account | $99/year |
| Firebase (Spark free tier) | Free |
| Vercel hosting | Free |
| Twilio OTP SMS | ~$0.05/SMS |
| Paymob transaction fee | ~2.5% per payment |
| Google Maps API | Free up to $200/month usage |
| **Total to launch** | **~$124 + transaction fees** |

---

## Notes for Next Chat Session

1. Attach `README.md`, `Questionnaire.md` and `Plan.md` to the project instructions before starting a new chat.
2. Start the new chat by saying: *"Continue building the Rahal app. Here is the project context."*
3. The app code lives in the artifact titled **"Rahal رحّال — Secured Vehicle Manager App"**.
4. The logo is **not yet finalized** — this should be the first thing resolved in the next session.
5. Claude will need the chosen logo letter (A–F, dark or light) to update the app.
6. After logo, next priority is **Phase 3 production features** (PDF export, trip logger, voice input).

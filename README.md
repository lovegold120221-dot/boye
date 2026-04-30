# EBURON AI VEP

VEP means **Virtual Employee Persona**. This app is the EBURON AI mobile-first live voice assistant experience, with Beatrice as the default persona for Boss Jo Lernout. The runtime combines Firebase authentication, Realtime Database context, and Gemini Live audio sessions to let a virtual employee speak and respond like a working assistant.

## Product Scope

- Brand: **EBURON AI**
- App: **VEP - Virtual Employee Persona**
- Default persona: **Beatrice**
- Default role: **Boss Jo Lernout's secretary**
- Primary experience: realtime voice assistant with live transcription, session memory, and generated artifacts
- Auth options: Google sign-in for Google-connected services, or email/password for voice assistant access without Google service scopes

## LLM Use Whitelist

This repository is explicitly approved to use configured LLM providers under the EBURON AI brand for the following app features:

- Realtime voice assistant responses
- Base prompt, persona prompt, and session-context execution
- Live audio reasoning through Gemini Live or another configured provider
- Transcription, translation, summarization, and context recall when enabled
- Generated assistant artifacts such as drafts, notes, plans, and structured outputs
- User-approved integrations that require AI reasoning over connected account data

The default provider is Gemini Live through `VITE_GEMINI_API_KEY`. LLM calls must use configured environment variables only. Do not hardcode provider credentials in source files. Email/password users can use the voice assistant, but Google-connected services should only run for users authenticated through Google OAuth with the required scopes.

## Local Setup

**Prerequisites**

- Node.js 20+
- npm
- Firebase project configuration already present in the app
- Gemini API key for live AI sessions

**Install**

```bash
npm install
```

**Configure**

```bash
cp .env.example .env.local
```

Set `VITE_GEMINI_API_KEY` in `.env.local`.

**Run**

```bash
npm run dev
```

The dev server starts on `0.0.0.0:3000`.

## Validation

```bash
npm run lint
npm run build
```

For UI and audio changes, also verify:

- Auth page loads as a mobile app surface
- Google sign-in and email/password flows render correctly
- Microphone permission handling works
- Live session starts with the EBURON AI base prompt before the customizable persona
- Orb animation reacts to assistant speaker output
- Transcript bubble updates without blinking animation

## Environment Variables

| Variable | Required | Purpose |
| --- | --- | --- |
| `VITE_GEMINI_API_KEY` | Yes | Gemini Live API key used by the browser runtime. |
| `VITE_LLM_USE_WHITELISTED` | Yes | Documents that EBURON AI LLM usage is approved for this app runtime. |
| `VITE_LLM_BRAND_NAME` | Yes | Public brand name for LLM-backed runtime behavior. |
| `VITE_PRODUCT_NAME` | Yes | Short product name. |
| `VITE_PRODUCT_FULL_NAME` | Yes | Full product name. |
| `VITE_DEFAULT_PERSONA_NAME` | Yes | Default virtual employee persona name. |
| `VITE_DEFAULT_BOSS_NAME` | Yes | Default boss/user name used by the persona context. |
| `VITE_EBURON_LOGO_URL` | No | Public EBURON logo asset URL. |
| `APP_URL` | No | Public app URL for callbacks, self-referential links, and deployment metadata. |

## Commands

```bash
npm run dev      # Start Vite development server
npm run lint     # Type-check with tsc --noEmit
npm run build    # Create production bundle in dist/
npm run preview  # Preview the production bundle locally
npm run clean    # Remove dist/
```

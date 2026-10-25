# HA Creator — one-time setup (AI key + Gmail send)

The **HA Creator** page (Dashboard → ✉️ HA Creator) writes the customer email
with AI in the approved format, then sends it from **plee@rabdcsolutions.com**
via Google Sign-in. Two free, one-time steps.

Everything you paste stays **in your own browser** (Settings → stored locally).

---

## 1. AI key (writes the email body) — free Gemini key

1. Go to https://aistudio.google.com/app/apikey
2. Sign in with any Google account → **Create API key** → copy it
   (starts with `AIza…`).
3. In the site: **✉️ HA Creator → ⚙ AI & Gmail settings → AI API key** →
   paste → **💾 Save settings**.

> OpenAI keys (`sk-…`) do **not** work from a website (OpenAI blocks browser
> calls) — the page will tell you to use Gemini instead. The free Gemini tier
> is more than enough for this volume.

## 2. Gmail send (Google sign-in) — free OAuth Client ID

1. Go to https://console.cloud.google.com/
2. Top bar → **Select a project → New Project** → name it `rabdc-ha-creator` → **Create**.
3. Left menu → **APIs & Services → OAuth consent screen**:
   - User type: **Internal** (if you use Google Workspace for rabdcsolutions)
     — otherwise **External**, then add yourself under **Test users**.
   - App name: `HA Creator` → Save.
4. **APIs & Services → Credentials → Create credentials → OAuth client ID**:
   - Application type: **Web application**
   - Name: `HA Creator site`
   - **Authorized JavaScript origins** → Add exactly:
     - `https://rabdc-solutions.netlify.app`
     - `http://127.0.0.1:8321` (optional, for local testing)
   - **Do not** add anything under redirect URIs (not needed).
5. **Create** → copy the **Client ID** (`…apps.googleusercontent.com`).
6. In the site: **✉️ HA Creator → ⚙ AI & Gmail settings → Google OAuth
   Client ID** → paste → **💾 Save settings**.

> Google will show the app as "unverified" on first sign-in because it is your
> own project: **Advanced → Go to HA Creator (unsafe)**. That is expected.

## 3. Use it

1. **To** = the customer's email, pick **Mrs./Mr./Ms.**, fill name / VIN /
   phone (auto-formatted with parentheses & hyphens) and what the message
   should say.
2. **✨ Write email (AI)** → the message appears in the preview in the exact
   approved structure (one paragraph, "would like", no "the customer").
3. Edit freely if needed, then either **📋 Copy message** or
   **📤 Send from Gmail** — sign in with the **plee@rabdcsolutions.com**
   Google account the first time; it sends straight from that inbox.

## Troubleshooting

| Message | Fix |
|---|---|
| `⚠ Add your AI API key…` | Paste the Gemini key (step 1). |
| `Gemini replied 400… API key not valid` | Wrong/pasted-with-space key — copy it again. |
| `⚠ Add your Google OAuth Client ID…` | Paste the Client ID (step 2). |
| `Google sign-in failed: idpiframe_initialization_failed` | The site's origin is missing from **Authorized JavaScript origins** — must match exactly, no trailing slash. |
| `Gmail refused the send (403)…` | The account you signed in with isn't allowed to send as plee@… — sign in with the plee@ account, or add it as a **Send-as** address in that inbox's Gmail settings. |
| Popup blocked | Allow popups for the site, then press Send again. |

The writing instructions (structure, wording rules) are editable in
⚙ Settings → "Writing instructions the AI follows"; **↺ Restore default
instructions** puts your original prompt back.

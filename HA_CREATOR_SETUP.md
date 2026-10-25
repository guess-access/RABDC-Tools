# HA Creator — one-time setup (AI key)

The **HA Creator** page (Dashboard → ✉️ HA Creator) writes the customer email
with AI in the approved format. One free, one-time step.

The key stays **in your own browser** (Settings → stored locally).

---

## 1. AI key (writes the email body) — free Gemini key

1. Go to https://aistudio.google.com/app/apikey
2. Sign in with any Google account → **Create API key** → copy it
   (starts with `AIza…`).
3. In the site: **✉️ HA Creator → ⚙ AI settings → AI API key** →
   paste → **💾 Save settings**.

> OpenAI keys (`sk-…`) do **not** work from a website (OpenAI blocks browser
> calls) — the page will tell you to use Gemini instead. The free Gemini tier
> is more than enough for this volume.

That's it — **✨ Write email (AI)** works with just the key. No Gmail
connection, no OAuth, no Client ID is needed or used.

## 2. Use it

1. Fill in **Customer name**, **VIN**, **Phone number** (auto-formatted with
   parentheses & hyphens) and what the message should say.
2. **✨ Write email (AI)** → the message appears in the preview in the exact
   approved structure (one paragraph, "would like", no "the customer").
   **Mr./Mrs. is chosen automatically** from the customer's name.
3. Edit freely if needed, then **📋 Copy message** (and **📋 Copy subject**)
   and paste it into your email.

**Subject is always:** `Centereach Hyundai Customer Follow-up` — shown fixed
on the page and included in the subject box for pasting.

## Troubleshooting

| Message | Fix |
|---|---|
| `⚠ Add your AI API key…` | Paste the Gemini key (step 1). |
| `Gemini replied 400… API key not valid` | Wrong/pasted-with-space key — copy it again. |
| `⚠ Fill in the customer name…` | Enter at least the name or the message request. |

The writing instructions (structure, wording rules) are editable in
⚙ Settings → "Writing instructions the AI follows"; **↺ Restore default
instructions** puts your original prompt back.

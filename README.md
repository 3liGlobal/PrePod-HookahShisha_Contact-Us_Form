# PrePod-HookahShisha_Contact-Us_Form

> 3LI Global — AIR Global integration estate. Generated 2026-08-31 by the US-Infrastructure audit. Facts below are drawn from this repo's code; anything not directly evidenced is marked _unverified_.

## Connected Resource
- **Azure resource:** none — static HTML/CSS/JS form (no Azure Function App, no deploy workflow in the repo)
- **Deploy trigger:** _unverified_ — no `.github/workflows/` present; hosting/publishing is done outside this repo
- **Talks to:**
  - Zoho Forms (`forms.zohopublic.com/airglobal/...`) — the form POSTs submissions directly to a hosted Zoho Form (`HookahShishaSupportFormSandbox21`), which feeds Zoho CRM
  - jQuery 3.6.4 via Google CDN (`ajax.googleapis.com`) — client-side only

## What It Does
A standalone "Hookah Shisha" support / contact-us web form. It renders the branded Zoho form markup, runs client-side field validation, and submits the collected fields straight to Zoho's hosted form endpoint (no backend of our own in between).

## Why It Exists
It is the public front end for capturing Hookah-Shisha support/contact requests into Zoho CRM via Zoho Forms. Unlike the ERP↔Zoho Azure Functions in this estate, it holds no server code — it is the form template/asset bundle. The page title and the `...Sandbox2` form permalink mark this as the Sandbox-2 (pre-production) twin of the live support form.

## How It Works
1. `index.html` — a Zoho-generated form whose `<form action>` points at `forms.zohopublic.com/airglobal/form/HookahShishaSupportFormSandbox21/.../htmlRecords/submit` with `method=POST`, `enctype=multipart/form-data`.
2. `js/validation.js` (`zf_ValidateAndSubmit`) runs Zoho's standard client-side validation on submit; `css/form.css` styles the template.
3. On submit the browser posts the fields to Zoho Forms, which creates the record in the linked Zoho CRM (hidden `zf_referrer_name`, `zf_redirect_url`, `zc_gad` fields support referral tracking / redirect / AdWords GCLID).
4. Operator note: the input `name` attributes are Zoho field keys — renaming/removing them makes submitted values arrive empty (called out in an HTML comment).

---
_Environment:_ Sandbox-2 / PreProd (page title "...Support Form Sandbox-2" and the Sandbox-2 Zoho form permalink)
_Runtime:_ Static HTML/CSS/JS (no build, no server runtime)

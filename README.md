# Omada Captive Portal Template

A free, open-source custom captive portal for **TP-Link Omada SDN Controller** — built on Omada's real portal API (voucher, local user, SMS, RADIUS, LDAP, and form-auth survey support), with a modern card-based UI and a slow animated background.

Ships with an **offline color customizer** (`customize.html`) so non-technical users can change colors and background style — no code editing required — before uploading to their controller.

> Not affiliated with or endorsed by TP-Link. This is an independent, community-built template that talks to Omada's documented external-portal endpoints.

## Features

- Works with whatever authentication types you've enabled in Omada (Voucher, Local User, SMS, RADIUS, LDAP, or Form Auth survey) — the UI adapts automatically
- Modern card design with a greeting banner (dynamic "Good Morning / Afternoon / Evening" + live date & time)
- Slow, subtle animated gradient background (respects `prefers-reduced-motion`)
- Choice of animated gradient background **or** your own background image
- All colors defined as CSS custom properties in one clearly labeled block — easy to hand-edit, and exactly what the customizer tool targets
- Zero build step — plain HTML, CSS, and JS. Upload as-is.

## Repository structure

```
.
├── portal/
│   ├── index.html        # the captive portal page
│   ├── index.css         # all styling + the customization variables block
│   ├── index.js          # Omada portal logic (auth flow, all auth types)
│   └── jquery.min.js     # required by the form-auth survey feature (MIT licensed)
├── customize.html        # offline, no-code color & background customizer
├── LICENSE
└── README.md
```

## Quick start (no code editing)

1. Download this repository (Code → Download ZIP, or `git clone`).
2. Open `customize.html` in any browser — it works fully offline, no server needed.
3. Pick your colors, and choose either an animated gradient or your own background image.
4. Click **Download index.css**, and replace `portal/index.css` with the downloaded file.
   - If you chose a background image, copy that image file into the `portal/` folder using the exact filename you entered in the tool.
5. Zip the contents of the `portal/` folder (not the folder itself — the files should be at the root of the zip).
6. In your Omada Controller: **Settings → Authentication → Portal** → create or edit a portal → set **Authentication Type** to **Custom** → upload your zip.
7. Set the **Landing Page** to whichever URL you want clients redirected to after a successful login.

## Going further (for developers)

Everything is plain HTML/CSS/JS — no build tools, no framework. `index.js` talks directly to Omada's documented external-portal endpoints:

- `POST /portal/getPortalPageSetting` — fetches the controller's configuration (enabled auth types, landing page, form-auth survey definition, etc.) on page load
- `POST /portal/auth` — submits the authentication attempt
- `POST /portal/radius/auth`, `POST /portal/ldap/auth` — used automatically for RADIUS/LDAP auth types
- `POST /portal/sendSmsAuthCode` — used for SMS auth

All page-specific text and behavior comes from that config response, so the same files work across different customers' controllers without modification — only `index.css`'s variable block needs to change per deployment.

## License

MIT — see [LICENSE](#). Free for personal and commercial use, including reselling customized versions, with attribution appreciated but not required.

## Contributing

Contributions are very welcome, from developers of any experience level — bug fixes, new features, translations, documentation, or design ideas. See [CONTRIBUTING.md](./CONTRIBUTING.md) for how to get set up and what to expect from the review process, and please follow our [Code of Conduct](./CODE_OF_CONDUCT.md).

Not sure where to start? Check the issues tab for anything labeled `good first issue`, or open a new issue to propose something.

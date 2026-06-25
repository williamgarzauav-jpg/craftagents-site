# CraftAgents Marketing Site

The v1 landing page for CraftAgents. Static site (HTML/CSS/JS, no build step, no backend).

## Files
- `index.html` — the landing page (hero, cost-of-missed-calls, value props, **scripted mock demo widget**, how-it-works, FAQ, founder/trust, data-handling, CTA).
- `privacy.html` — privacy policy (template-based; review before handling real customer data at scale).
- `_headers` — security headers for Netlify-style hosts (the ones that can't be set via `<meta>`).
- `data-handling-blurb.txt` — plain-English data stance, reusable in sales conversations.
- `.gitignore`

## Important notes
- **The on-page chat is a SCRIPTED MOCK.** No backend, no real AI. Answers come from the
  hard-coded `ROOFING_SCRIPT` object in `index.html`. Replace with the live RAG agent later.
- **Roofing-specific copy** is wrapped in `<!-- ROOFING: ... -->` markers so it's easy to find
  and swap when expanding to other verticals.
- **Visual design is not final.** Navy/amber identity is intentional, but colors and any
  animation direction are decided with Will later.

## Run locally
Just open `index.html` in a browser (no server needed for the static page).

## Deploy (free)
1. Drag this folder onto https://app.netlify.com/drop (or connect the repo).
2. Point `craftagents.net` DNS at the Netlify site.
3. The `_headers` file applies security headers automatically on Netlify.

## Code review workflow
This folder is its own git repo so CodeRabbit (VS Code extension) can review diffs. Build in
small, scoped commits.

---

## NEEDS WILL (action items waiting on you)
1. **Cal.com booking link** — replace `BOOKING_URL = "REPLACE_WITH_CALCOM_LINK"` in `index.html`.
   Until then, all "Book a demo" buttons fall back to the email link.
2. **Business phone number** — optional, strengthens the founder/trust block. Placeholder comment
   is in `index.html` in the founder section.
3. **UI/UX plugin** (Step 1) — could not be installed from the agent. Run these yourself in Claude Code:
   `/plugin marketplace add nextlevelbuilder/ui-ux-pro-max-skill`
   `/plugin install ui-ux-pro-max@ui-ux-pro-max-skill`
4. **Confirm contact email** — site uses `will@craftagents.net`. Make sure that inbox reliably
   receives mail, or swap to your Gmail.
5. **Final design direction** — colors / animations to be decided together.
6. **Privacy policy legal review** — before taking real customer data at scale.
7. **Real demo agent backend** — replace the scripted mock widget with the live RAG agent when built.
8. **Confirm the ~62% missed-call stat source** before relying on it in writing, or soften the wording.

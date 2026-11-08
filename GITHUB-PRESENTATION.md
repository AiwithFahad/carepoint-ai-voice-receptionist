# GitHub Presentation — CarePoint AI Voice Receptionist

## Repository description (one line — paste into GitHub's "About" field)

> AI voice receptionist for a medical clinic — ElevenLabs voice agent "Emma" + n8n automation that books patient appointments by voice and stores them in Google Sheets.

## Topics / tags

`elevenlabs` · `voice-ai` · `ai-receptionist` · `n8n` · `workflow-automation` · `google-sheets` · `appointment-booking` · `healthcare-automation` · `conversational-ai` · `ai-agents`

(Topics reflect the author's stated stack. `n8n` is included because the author's published caption names it as the automation layer; the repository's own docs disclose that the workflow itself is not shown in the demo video.)

## Suggested commit messages

- `docs: add complete project documentation pack (README, workflow, architecture, setup, limitations)`
- `assets: add demo screenshots extracted from project video`
- `docs: add LinkedIn demo video link`

## Upload instructions

**Option A — GitHub web UI (no git required):**
1. Create a new public repository named `carepoint-ai-voice-receptionist` (no README/.gitignore/license — this pack provides them).
2. Upload all files from this folder, preserving the structure: the Markdown files at the root, `assets/` with its three PNGs, and `demo/VIDEO-LINK.md`.
3. Set the About description (above) and add the topics.

**Option B — git:**
```bash
cd carepoint-ai-voice-receptionist
git init
git add .
git commit -m "docs: add complete project documentation pack (README, workflow, architecture, setup, limitations)"
git branch -M main
git remote add origin https://github.com/AiwithFahad/carepoint-ai-voice-receptionist.git
git push -u origin main
```

## Presentation advice

- **Lead with the validation moment.** The "3:99 AM" exchange is the strongest 15 seconds of the demo — it proves the agent protects the clinic's data instead of blindly booking. Quote it in the README (done) and mention it when sharing the LinkedIn post.
- **Keep the honesty visible.** The "Demonstrated vs. Stated" split and the limitations file make this portfolio piece more credible, not less — recruiters and clients trust documented limits.
- **Strengthen it later with one addition:** publish the actual n8n workflow (export JSON + a canvas screenshot). That single upload would let WORKFLOW-EXPLANATION.md gain the node-level detail it currently — deliberately — lacks.
- Pin this repository alongside the other voice-receptionist projects (Hercules, Blade & Crown) to show the same skill across three industries: healthcare, automotive, hospitality.

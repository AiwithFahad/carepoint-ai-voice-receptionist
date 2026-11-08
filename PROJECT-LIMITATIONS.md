# Project Limitations & Disclosures — CarePoint AI Voice Receptionist

This documentation was produced from the project's **demonstration video** and the author's **published LinkedIn caption** only. The following limitations apply and are disclosed deliberately — they are part of what makes this portfolio entry credible.

## Source Limitations

1. **No n8n workflow is shown in the video.** There is no workflow canvas, no node names, no executions panel, and no workflow JSON export in this repository. n8n's role is known only from the author's caption. Node-level documentation would have to be invented, so it is intentionally absent; the flow is documented at the level the evidence supports (see [WORKFLOW-EXPLANATION.md](WORKFLOW-EXPLANATION.md), Part B).
2. **No source code or live deployment link** is included or claimed. The clinic website and agent are shown in the video only.
3. **Configurations are not verifiable.** The agent's system prompt, voice/model settings, tool definitions, and the mechanism that writes to Google Sheets cannot be confirmed from the video.

## Demonstrated vs. Stated

| Capability | Status |
|---|---|
| Voice/typed booking conversation with structured intake | ✅ Demonstrated |
| Invalid-input validation ("3:99 AM" rejected and re-asked) | ✅ Demonstrated |
| Booking written to Google Sheets | ✅ Demonstrated |
| Patient FAQ handling | ✅ Demonstrated |
| Appointment reminders | ⚠️ Stated by the author — not demonstrated |
| Rescheduling / cancellation flows | ⚠️ Implied by "appointment management" in the author's description — not demonstrated |
| Live availability checking against a real calendar | ⚠️ Emma *offers* to check next available slots in conversation; no calendar or slot list is shown — mechanism not confirmed |

## Data Notes

- All patients, phone numbers, and appointments visible in the video's spreadsheet are **demo data** (the phone numbers are visibly sequential test numbers). No real patient information is reproduced in this repository's text; phone numbers are referred to by column only.
- In a production clinic deployment, appointment data is sensitive personal data: a shared spreadsheet would need strict access control, and a purpose-built, access-logged system would be preferable.

## System Limitations (as evidenced)

- The system of record is a spreadsheet: no built-in protection against double-booking, concurrent edits, or accidental deletion is visible in the demo.
- The demonstrated booking depends on the patient confirming a valid time after correction; how the agent handles repeated invalid answers, call drop-offs mid-booking, or a full schedule is not shown.
- The demo shows one clinic, one agent persona, and English-language conversation only; multi-language or multi-branch behaviour is not evidenced.

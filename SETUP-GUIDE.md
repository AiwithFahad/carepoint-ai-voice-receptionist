# Setup Guide — CarePoint AI Voice Receptionist

This guide separates three kinds of information, clearly labelled:

- ✅ **Verified from video** — visible in the demo.
- 🗣️ **Author-stated** — from the author's published project caption.
- 🛠️ **Suggested reconstruction** — a reasonable way to rebuild an equivalent system; **not** a claim about how the original was built.

> ⚠️ No credentials, API keys, or agent identifiers are included in this repository. The demo video partially shows an agent identifier in one frame — it is deliberately **not** reproduced here. Never commit real keys or patient data to a repository.

---

## Required Components

| Component | Purpose | Status |
|---|---|---|
| A website page for the clinic | Hosts the voice widget; presents services and a Book Appointment entry point | ✅ Verified from video |
| ElevenLabs account + voice agent ("Emma") | The conversational receptionist | ✅ Verified from video (platform + persona) |
| Google account + Google Sheet | The appointment record with columns **Name \| Phone \| Appointment Type \| Date \| Time \| Doctor** | ✅ Verified from video |
| n8n instance | Automation between the agent and the sheet | 🗣️ Author-stated |
| Credential types you will need (yours, kept secret) | ElevenLabs account/API access for your agent; Google account access for your sheet; n8n credentials for Google Sheets | 🛠️ Suggested reconstruction |

## Configuration Visible in the Video ✅

- Widget behaviour: call button to start, live transcript, typed fallback input ("Or type a question to the assistant…") with Send, state indicators ("Agent speaking…", "Listening to your voice…"), and an End Conversation control.
- Agent persona: "Emma", virtual receptionist for CarePoint Medical Clinic, with a fixed greeting.
- Intake order: appointment type → doctor preference → patient name → phone number → date → time.
- Validation behaviour: an invalid time is rejected conversationally and re-asked in a standard format.
- Sheet schema: six columns exactly as listed above; "No Preference" is a valid Doctor value.

## Recreation Steps 🛠️ (suggested reconstruction)

1. **Create the appointment sheet.** In Google Sheets, create a workbook with the six columns (Name, Phone, Appointment Type, Date, Time, Doctor). Keep patient data access restricted — this is health-adjacent personal data.
2. **Build the voice agent.** In ElevenLabs, create a conversational agent ("Emma") with a clinic receptionist system prompt that: greets the patient, collects the five intake fields in order, reads back and validates date/time values (rejecting impossible times and asking for a standard format), and answers the "what do I need to book?" FAQ with the same field list.
3. **Embed the widget.** Add the ElevenLabs widget to the clinic website with both voice and typed input enabled, mirroring the states shown in the video.
4. **Connect the automation.** In n8n (the author's stated layer), build a workflow that receives the completed booking from the agent and appends a row to the sheet. 🗣️ The original's exact mechanism (tool calls, webhook shape, node layout) is **not confirmed from video** — design your own equivalent and document it as yours.
5. **Test like the demo.** Run the two demonstrated conversations: (a) a booking with a deliberately invalid time — the agent must refuse and re-ask; (b) the FAQ question — the answer must list the intake fields. Then check the sheet for the new row.

## What Cannot Be Verified

- The original n8n workflow structure, node configuration, and error handling.
- The agent's full system prompt, voice/model settings, and any tool definitions.
- How reminders (author-stated feature) are implemented, and through which channel.

See [PROJECT-LIMITATIONS.md](PROJECT-LIMITATIONS.md) for the full disclosure.

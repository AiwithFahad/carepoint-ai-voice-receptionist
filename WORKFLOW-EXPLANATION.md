# Workflow Explanation — CarePoint AI Voice Receptionist

> **Read this first — an honesty note about scope.**
> The demo video shows **no n8n canvas, no workflow nodes, and no executions panel**. n8n is named as the automation layer only in the author's published project caption. This document therefore does **not** invent nodes. Part A documents the end-to-end flow exactly as the video demonstrates it, stage by stage. Part B states plainly what is known — and not known — about the automation layer behind those stages.

Demo video: [Watch on LinkedIn](https://lnkd.in/p/dGZ_7Aq2) (timestamps in [demo/VIDEO-LINK.md](demo/VIDEO-LINK.md)).

---

## Part A — The demonstrated flow, stage by stage

### Stage 1 — Patient opens the voice widget on the clinic website

- **Purpose:** Give the patient a way to start a spoken (or typed) conversation with the clinic from the CarePoint website.
- **Input:** Patient visits the CarePoint Medical Clinic site (nav: Home / Services / About Us / Contact; Book Appointment button; hero "Healthcare That Puts You First"; services: Primary Care, Preventive Health, Family Medicine, Follow-up Care) and starts the widget ("Talk to CarePoint Voice AI — Click the call button below to start an interactive voice consultation", labelled "ElevenLabs Voice Agent"). A typed alternative is offered: "Or type a question to the assistant…" with a Send button.
- **Processing:** The widget connects to the ElevenLabs agent and shows live state — "Agent speaking…", "Listening to your voice…" — plus an End Conversation control and a live transcript.
- **Output:** An open conversation channel with the agent "Emma".
- **Connection to next stage:** The agent opens the conversation (Stage 2).

### Stage 2 — Greeting and intent capture

- **Purpose:** Welcome the patient and establish what they need.
- **Input:** The open conversation from Stage 1.
- **Processing:** Emma greets the patient verbatim: *"Hello, thank you for calling CarePoint Medical Clinic! My name is Emma, and I'm your virtual receptionist. How may I help you today?"* The patient replies (voice or typed): *"I would like to book an appointment for general checkup."*
- **Output:** Booking intent recognised; the intake sequence begins.
- **Connection to next stage:** Emma starts collecting the booking fields (Stage 3).

### Stage 3 — Structured intake (appointment type, name, phone, doctor preference)

- **Purpose:** Collect the fields the clinic needs for a booking, one at a time, in a fixed order.
- **Input:** The patient's answers, turn by turn.
- **Processing:** Emma asks what type of appointment is needed and whether a specific doctor is preferred (her reply is tagged *[informative]* in the on-screen transcript). The patient confirms a general medical appointment, and provides a name ("Ahmed") and a phone number (demo data — values are not reproduced in this documentation).
- **Output:** A partial booking record: appointment type = general medical appointment, patient name, phone number, doctor preference (asked; "No Preference" is an accepted value in the clinic's sheet).
- **Connection to next stage:** Emma asks for the date and time (Stage 4).

### Stage 4 — Date and time collection, with availability help

- **Purpose:** Agree a concrete slot for the appointment.
- **Input:** The partial record from Stage 3.
- **Processing:** Emma asks: *"What date would work best for your general medical appointment, and what time do you prefer? If you're unsure, I can check for the next…"* (offering to check the next available slots — tagged *[helpful]*). The patient answers with a date (13 October 2026) and a garbled time containing "3:99 AM" alongside "9:00 AM".
- **Output:** A candidate date/time that must pass validation before it can be booked.
- **Connection to next stage:** The answer is validated (Stage 5) before anything is stored.

### Stage 5 — Input validation and clarification (the demo's key moment)

- **Purpose:** Stop invalid data from becoming a booking.
- **Input:** The garbled time from Stage 4.
- **Processing:** Emma detects that "three ninety nine AM" is not a valid time and responds (tagged *[calm]*), repeating back what she understood and asking for a correction: *"…you mentioned three ninety nine AM, which isn't a valid time. Could you please confirm the exact time you prefer in a standard format, like nine thirty AM or ten forty five AM? Also, is there a preferred doctor, or would you like the first available provider?"*
- **Output:** A clarification request to the patient — **no booking is written with the invalid value**.
- **Connection to next stage:** Once the patient confirms valid details, the booking is stored (Stage 6).

### Stage 6 — Booking written to Google Sheets

- **Purpose:** Persist the appointment in the clinic's appointment record.
- **Input:** The validated booking fields.
- **Processing:** A new row is written to the Google Sheets appointment record, whose columns are **Name | Phone | Appointment Type | Date | Time | Doctor**. The sheet already holds six demo bookings (general checkups, follow-up visits, a general consultation, a blood-pressure check, across 2026-10-13 → 2026-10-15, with named doctors or "No Preference").
- **Output:** The new row for the demo patient — *Ahmed — general medical — 2026-10-… — 9:00 — (doctor cell shown as "empty")* — appears selected in the sheet (~0:08 and again ~0:44 in the video).
- **Connection to next stage:** End of the demonstrated flow. (A spoken confirmation to the patient is part of the conversation pattern, but the video cuts to the sheet; the exact confirmation wording after validation is **not confirmed from video**.)

### Stage 7 — Patient FAQ handling (second demonstrated conversation)

- **Purpose:** Answer common patient questions inside the same conversation channel.
- **Input:** Patient asks: *"What information do I need to book an appointment?"*
- **Processing:** Emma answers (tagged *[friendly]*) with the exact intake list — full name, a contact phone number, the appointment type or specialty, a preferred date and time, and optionally a preferred doctor — and offers to begin: *"May I have your full name to start?"*
- **Output:** The patient knows what to provide; the conversation can flow straight into Stage 3.
- **Connection to next stage:** Loops back into the intake (Stage 3) if the patient proceeds.

---

## Part B — The automation layer (author-stated, not shown)

- The author's published caption names **n8n** as the workflow-automation layer of this project (caption stack: "n8n | AI Voice Agent | Google Sheets | Workflow Automation").
- The video, however, contains **no n8n canvas, node names, workflow structure, webhook configuration, or executions**. How the ElevenLabs agent's collected fields reach Google Sheets — which tool calls the agent makes, what the n8n workflow(s) look like, how errors are handled — is **Not confirmed from video**.
- Accordingly, this repository deliberately contains **no node-by-node n8n documentation and no workflow JSON**: inventing either would misrepresent the project. If the workflow export is published later, this file is where its node documentation belongs.

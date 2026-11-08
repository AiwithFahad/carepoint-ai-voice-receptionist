# CarePoint AI Voice Receptionist

An AI voice receptionist for **CarePoint Medical Clinic**: an ElevenLabs voice agent named **"Emma"** embedded on the clinic's website that greets patients, collects booking details in natural conversation, validates what it hears, and stores confirmed appointments in **Google Sheets** — with **n8n** as the automation layer (author-stated; see the honesty notes below).

> 📹 **Demo video:** [Watch on LinkedIn](https://lnkd.in/p/dGZ_7Aq2) — see [demo/VIDEO-LINK.md](demo/VIDEO-LINK.md) for a timestamped walkthrough of what the video shows.

---

## Overview

Clinic front desks spend a large share of every day on the same phone tasks: answering calls, collecting a patient's name, phone number, appointment type, preferred date and time, and writing the booking into a register. This project replaces that repetitive loop with a voice agent that:

1. Answers the patient on the clinic website (voice or typed input).
2. Holds a natural booking conversation and collects the required fields one by one.
3. **Validates the input** — in the demo, Emma hears an impossible time ("3:99 AM"), recognises it is not a valid time, and calmly asks the patient to confirm the time in a standard format instead of booking garbage data.
4. Writes the resulting appointment into a Google Sheets appointment record alongside the clinic's other bookings.

## Business Problem

- Reception staff repeat the same intake questions for every booking.
- Calls are missed outside working hours or while the desk is busy.
- Hand-taken bookings are error-prone — an invalid or ambiguous time can be written down without anyone noticing.
- Appointment data ends up scattered instead of in one structured record.

## Solution

A website-embedded ElevenLabs voice agent ("Emma") acts as the clinic's virtual receptionist. It follows a structured intake flow — appointment type → patient name → phone number → date and time → optional preferred doctor — checks what the patient said for validity, and stores the finished booking in a Google Sheets appointment sheet with the columns **Name | Phone | Appointment Type | Date | Time | Doctor**.

## Key Features

### Demonstrated in the video ✅

| Feature | Evidence |
|---|---|
| Voice + typed conversation on the clinic website | Widget with call button, live transcript, "Or type a question to the assistant…" input with Send, "Agent speaking…" / "Listening to your voice…" states, and an End Conversation control |
| Structured appointment intake | Emma collects appointment type, full name, phone number, date, time, and optional preferred doctor, in order |
| **Input validation** | Patient gives a garbled time ("3:99 AM"); Emma flags it — *"you mentioned three ninety nine AM, which isn't a valid time"* — and asks for the time in a standard format (e.g. "nine thirty AM or ten forty five AM") |
| Availability assistance | Emma offers to check the next available slots when the patient is unsure of a time |
| Appointment stored in Google Sheets | The sheet is shown with six existing bookings; a new row for the demo patient ("Ahmed — general medical — 2026-10-… — 9:00") appears selected after the conversation |
| Patient FAQ handling | Asked *"What information do I need to book an appointment?"*, Emma lists exactly what is needed and offers to start |

### Stated by the author, not demonstrated ⚠️

The author's project description also lists **appointment reminders** and appointment management beyond booking (the published caption mentions simplifying appointment management generally). These capabilities are **not shown working in the demo video** and are documented here as stated, not demonstrated. Cancellation/rescheduling flows are likewise not demonstrated.

## Technologies

| Layer | Technology | Status |
|---|---|---|
| Voice agent | ElevenLabs Voice Agent ("Emma") | ✅ Verified from video (widget labelled "ElevenLabs Voice Agent") |
| Front end | CarePoint Medical Clinic website (Home / Services / About Us / Contact, Book Appointment) | ✅ Verified from video |
| Data store | Google Sheets — appointment record (Name, Phone, Appointment Type, Date, Time, Doctor) | ✅ Verified from video |
| Automation layer | n8n | ⚠️ Author-stated in the published project caption — **no n8n canvas, nodes, or executions are shown in the video** |
| LLM / speech models | Not named in the video | ❌ Not confirmed from video |

## Architecture

```
Patient (voice or typed input)
        │
        ▼
CarePoint website ── ElevenLabs voice widget ("Emma")
        │  conversation: greeting → intake → validation
        ▼
Automation layer (n8n — author-stated, not shown)
        │
        ▼
Google Sheets — appointment record
(Name | Phone | Appointment Type | Date | Time | Doctor)
```

Full detail: [PROJECT-ARCHITECTURE.md](PROJECT-ARCHITECTURE.md). Step-by-step flow: [WORKFLOW-EXPLANATION.md](WORKFLOW-EXPLANATION.md).

## Step-by-Step Flow (as demonstrated)

1. **Greeting** — Emma: *"Hello, thank you for calling CarePoint Medical Clinic! My name is Emma, and I'm your virtual receptionist. How may I help you today?"*
2. **Intent** — the patient asks to book a general checkup.
3. **Intake** — Emma confirms the appointment type, asks about a preferred doctor, and collects the patient's name and phone number.
4. **Date & time** — Emma asks what date and time work best and offers to check the next available slots.
5. **Validation** — the patient answers with a garbled time; Emma detects the invalid time, repeats back what she understood, and asks for the time in a standard format plus the doctor preference.
6. **Storage** — the completed booking appears as a new row in the Google Sheets appointment record.

## Screenshots

| Asset | What it shows |
|---|---|
| [assets/project-demo-thumbnail.png](assets/project-demo-thumbnail.png) | Opening frame (~0:01) — the CarePoint Medical Clinic interior from the demo's opening footage |
| [assets/workflow-overview.png](assets/workflow-overview.png) | System front-end overview (~0:12) — clinic website + ElevenLabs voice widget mid-conversation (no workflow canvas exists in the video, so the front end is the honest "overview" shot) |
| [assets/execution-result.png](assets/execution-result.png) | Result (~0:44) — the Google Sheets appointment record with the new booking row selected |

## Setup (summary)

You need: a website page to host the widget, an ElevenLabs voice agent configured with the clinic's intake script, a Google Sheet with the six appointment columns, and an automation connection (author used n8n) that writes the collected booking into the sheet. Full guide with verified vs. suggested steps separated: [SETUP-GUIDE.md](SETUP-GUIDE.md).

## Use Cases

- Medical clinics handling routine booking calls and web enquiries.
- Any appointment-based business (dental, physio, diagnostics) that records bookings in a spreadsheet.
- After-hours enquiry capture with the same intake quality as the front desk.

## Limitations

- This documentation is reconstructed **from the demo video plus the author's published caption only**. The video shows **no n8n workflow canvas**, so node-level detail is **not confirmed from video** — see [PROJECT-LIMITATIONS.md](PROJECT-LIMITATIONS.md).
- Reminders and cancellation/rescheduling are stated by the author, not demonstrated.
- The bookings shown in the sheet are demo data.
- No live deployment link is published in this repository.

## Future Improvements

*Suggested directions — none of these are shown in the video:*

- Publish the n8n workflow export alongside this documentation.
- Demonstrate the reminder flow and reschedule/cancel flows end-to-end.
- Add double-booking checks against existing sheet rows before writing.
- Send the patient an SMS/WhatsApp confirmation after booking.

## Author

**Fahad Ahmed Shanawar**
- GitHub: https://github.com/AiwithFahad
- LinkedIn: https://www.linkedin.com/in/fahad-ahmed-shanawar-107a5535a/

# L&L Agent Contracting Kit — HIPAAtizer (HZ) Build Spec

**Owner:** Tim Meuret, Loreen & Lane, LLC d/b/a The Retirement Answer Team
**Draft:** October 2026
**Source material:** Slate Jotform "Clone of Loreen & Lane Direct Agent Contracting Kit" (settings, 22 conditions, notification email, thank-you page), the Aug 21 HZ Onboarding Workflow Map, the L&L NDA (`Loreen_Lane_NDA_Fillable.pdf`), Tim's agent recruiting email, and the Spirit New Mexico appointment link.

Items marked **[VERIFY IN HZ]** depend on an HZ feature I could not confirm from documentation. Test each one before go-live.

---

## 1. What changes from the Slate Jotform

| Area | Slate Jotform today | L&L HZ kit |
|---|---|---|
| Branding | Slate "S" logo in email, L&L + Slate on thank-you page | L&L only (logo, Brand Blue `#2596BE`, Greens `#1BA750` / `#6EBB50`, Orange CTA `#F0843B`, Charcoal text `#333333`, Open Sans) |
| Platform | Jotform, encryption **off** | HZ (HIPAA-compliant, encrypted by default) |
| Licensing | Assumes licensed | Licensed / not-licensed branch. Not-licensed **pauses** after contract + NDA and sends the test-prep email |
| NDA | None | L&L Non-Disclosure and Confidentiality Agreement signed before any carrier, training or process information is shown |
| Preparation | None | "Get Prepared to Contract" page + video explaining every document and why it's needed |
| Voided check | Required (condition #19) | **Optional now, required before first commission.** "I'm still setting up my account" creates a follow-up |
| E&O | Not handled | Three paths: L&L E&O (via Next live certificate), own E&O upload, or still obtaining |
| AML | Yes/No + date/name | Completed inside WebCE; upload the WebCE AML certificate |
| Spirit Dental & Vision | Not in form | L&L-direct section with the Spirit NM appointment link embedded (or button fallback) |
| Thank-you contacts | SLATE Agent Support 833-752-8300, contracts@slatefs.com | L&L contacts (see §9) |
| Duplicate PDFs | Two attachments both named "New Document 1" | One submission PDF + one executed NDA PDF, named clearly |

---

## 2. Form settings

| Setting | Value |
|---|---|
| Form title | Loreen & Lane Agent Contracting Kit |
| Status | Enabled |
| Encryption | On (HZ default) |
| Save & Continue Later | **On**. Required for the pause-and-return licensing path **[VERIFY IN HZ: resume link survives weeks, not hours]** |
| Submission editing | On, so an agent can return to the same record after licensing |
| Unique submission | One per email address |
| Signature capture | HZ e-signature on NDA page and Final Review page |
| Auto-delete | Off |

---

## 3. Page flow

```
P1  Welcome (video)
P2  About You (identity + contact)
P3  Licensing Status  ──── NOT licensed ──┐
P4  Get Prepared to Contract (video)      │
P5  Background Questions 1–12             │
P6  NDA (signature)  ◄────────────────────┤  unlicensed agents still complete P2, P4, P5, P6
                                           └─► P13 Paused: "Let's get you licensed" → submit → test-prep email
P7  Licenses, NPN & Current Upline        (licensed only)
P8  Documents: DL, E&O, AML               (licensed only)
P9  Banking (Andre video) — optional now  (licensed only)
P10 Carrier Selections                    (licensed only)
P11 Spirit Dental & Vision (L&L direct)   (licensed only)
P12 Final Review & Signature              (licensed only)
P14 Thank You
```

HZ skips a screen automatically when every row on it is hidden by conditional logic. All "licensed only" rows carry the condition **Show if `licensed` = "Yes"**, so the unlicensed agent flows P6 → P13 with no extra rules.

---

## 4. Field-by-field

### P1 — Welcome
- **Video:** Welcome to L&L contracting (script in `03_Video_Scripts.md`, V1)
- Text block: what this kit does, about how long it takes, and that they can save and come back.

### P2 — About You
Carried over from Slate, renamed to plain language.

| Field | Type | Req | Notes / Slate equivalent |
|---|---|---|---|
| Are you contracting as an individual or an entity? | Radio: Individual / Entity | Y | `areYou` |
| First name | Text | Y | `firstName410` |
| Last name | Text | Y | `lastName411` |
| Full legal name | Calculated | — | Slate condition #1 inserts `{Last} {First}`. **Change to `{First} {Last}`** so it reads naturally on the NDA |
| Date of birth | Date | Y | |
| SSN | Masked text | Y | |
| Mobile phone | Phone | Y | |
| Email | Email | Y | `emailAddress5`. Also used for Basecamp invite |
| Resident state | Dropdown | Y | `whatState404` |
| Home address | Address | Y | |
| Mailing address different? | Yes/No | Y | |
| Mailing address | Address | C | Show if mailing different = Yes (Slate #20) |
| Entity name | Text | C | Show if Entity (Slate #22) |
| Entity TIN | Masked text | C | Show if Entity (Slate #18) |
| Entity principal | Text | C | Show if Entity (Slate #21) |
| Entity NPN | Text | C | Show if Entity (Slate #21) |
| Entity resident license | Upload | C | Show if Entity (Slate #18) |
| Headshot (optional) | Upload | N | Feeds Medicare 101 bio page |

### P3 — Licensing Status
| Field | Type | Req |
|---|---|---|
| Do you currently hold an active resident Life & Health license? | Radio: **Yes** / **No, not yet** / **I'm studying now** | Y |

`licensed` = Yes → full path. Either "No" answer → pause path.

### P4 — Get Prepared to Contract
- **Video:** V2, the document checklist, with the what and why for each item.
- Checklist (display only, each with a one-line "why"):
  1. Driver's license (carriers verify identity)
  2. NM resident Life & Health license + NPN (carriers can't appoint you without it)
  3. E&O certificate (every carrier requires proof of coverage; L&L covers you if all contracts are with L&L)
  4. AML certificate from WebCE (carriers require anti-money-laundering training before you can write annuities and most life products)
  5. Voided check or bank letter (**can wait** until your first commission; open a separate business account)
  6. Release from your current upline, if you have one
- For unlicensed agents this page doubles as their shopping list while they study.

### P5 — Background Questions
Copy all twelve questions verbatim from the Slate build tab **(questions 5 and 6 did not appear in the conditions screenshots; pull them from the Jotform Build tab)**. Each "Yes" reveals an explanation field. Conditions from Slate:

| Q | Topic (truncated in screenshots) | Yes reveals | Slate # |
|---|---|---|---|
| 1 | Indebtedness to an insurance company | Company, amount, repayment agreement | 17 |
| 2 | Felony or misdemeanor conviction | Explain + dates | 16 |
| 3 | Driver's license revoked | Explain + dates | 15 |
| 4 | Bankruptcy in process or ever filed | Explain + dates, supporting docs upload, 4a, 4b, 4c | 2, 14 |
| 4c | Brokerage firm bankruptcy | When filed, amount, which filed, settled date | 3 |
| 5 | *(copy from Jotform)* | | |
| 6 | *(copy from Jotform)* | | |
| 7 | Refused a bond or E&O | Explain | 13 |
| 8 | Insurance license suspended | Explain | 12 |
| 9 | Fined or disciplinary action | Explain | 11 |
| 10 | Present or past 5 years… | Explain | 10 |
| 11 | Denied an appointment | Explain | 9 |
| 12 | Terminated for cause | Explain | 8 |

Unlicensed agents answer these now. Carriers will ask again; this lets Tim spot a problem before someone spends money on the exam.

### P6 — Non-Disclosure and Confidentiality Agreement
- Text block: full NDA text from `Loreen_Lane_NDA_Fillable.pdf`, Sections 1–12. Set as a scroll box with "I have read the agreement" checkbox **[VERIFY IN HZ: scroll-to-bottom enforcement]**.
- Prefilled from earlier answers (read-only):

| NDA field | Source |
|---|---|
| Effective Date | Today's date |
| Recipient Full Legal Name | Full legal name |
| Role/Relationship | "Independent Field Agent" |
| Agency/Company | Entity name (blank if Individual) |
| Recipient Address | Home address |
| Phone / Email | Mobile / Email |

- Recipient fields: **Signature**, Printed Name (prefilled), Title/Role (prefilled), Date (auto).
- Company side: Tim Meuret, Founder & CEO. Apply Tim's stored signature on generation, or route for countersignature after submission **[VERIFY IN HZ: second-signer workflow]**.
- Store **NDA version** as a hidden field: `LL-NDA-2026-10`. When the NDA changes, bump the version and resend for signature.
- Generate an executed NDA PDF and email a copy to the agent.

**Before go-live:** the NDA's own footer says to have a New Mexico attorney review it. Run it past LegalShield once.

### P7 — Licenses, NPN & Current Upline *(licensed only)*
| Field | Type | Req | Notes |
|---|---|---|---|
| Individual NPN | Text | Y | Verify at nipr.com |
| Resident license number | Text | Y | |
| Resident license (upload) | Upload | Y | |
| Lines of authority | Checkbox: Life, Health, Annuity | Y | |
| Non-resident states held | Multi-select | N | |
| States you plan to add | Multi-select | N | Feeds future licensing work |
| Are you currently contracted with another FMO? | Yes/No | Y | Slate #4, #5, #6 (#5 and #6 are duplicates; build once) |
| Carriers you're contracted with now | Text | C | Show if FMO = Yes |
| Release from current upline | Upload + "I'm obtaining this" | C | Show if FMO = Yes |

### P8 — Documents *(licensed only)*
Every item offers **Upload now / I'm obtaining this / Not applicable** per the workflow map. "I'm obtaining this" creates a follow-up task instead of blocking.

**Driver's license** — Upload, required.

**AML (via WebCE)**
- Have you completed the AML course in WebCE? Yes / Not yet
- Yes → AML completion date + certificate upload
- Not yet → link to webce.com/loreenandlane, follow-up task
- Replaces Slate #7.

**E&O — How will you carry E&O?** (Option A selected by Tim)

| Choice | What shows | Status after submit |
|---|---|---|
| **A. Cover me under L&L's E&O** | (1) Acknowledgment checkbox: *"I understand L&L's E&O covers me only while all of my carrier contracts are placed through Loreen & Lane."* (2) Video V4 on requesting a change on the live certificate. (3) Button: **Open L&L's E&O certificate** → `https://portal.nextinsurance.com/public/certificates/live-certificate/3ebd3f96a7c8913203077c7c567933a0`. (4) Upload: updated certificate PDF (optional now) | **Pending — L&L E&O certificate** until PDF uploaded |
| **B. I have my own E&O** | Upload certificate PDF (required), carrier, policy #, per-claim / aggregate limits, expiration date | Complete. Reminder 30 days before expiration **[VERIFY IN HZ: date-based reminders]** |
| **C. I'm still getting E&O** | Text: Next Insurance through Marla is an option. Button to Marla's contact | **Pending — E&O**; follow-up task |

How Option A works with Next: the agent opens the live certificate and submits a change request with their name. Next notifies Tim automatically; Tim approves in the Next app. The agent then downloads the updated PDF (Print → Save as PDF if no download button) and uploads it, from the HZ resume link if they've already submitted.

Automatic link-to-PDF conversion (webhook → PDF service → HZ record) is a **phase 2** option **[VERIFY IN HZ: outbound webhook / Zapier]**. Next has no public policyholder API, so the Tim-approval step stays manual.

**Open item for Tim:** confirm in the Next app that a change request can add a *named individual agent*, not just a certificate holder.

### P9 — Banking *(licensed only, optional now)*
- **Video:** V3, Andre (CFO) on individual vs. entity payments, separate business account, name matching.
- Bank account status: **Upload voided check now** / **Upload bank letter** / **I'm still setting up my account**
- Upload field (replaces Slate #19, no longer required).
- "Still setting up" → banking follow-up task, due before first commission.
- Routing/account numbers are **not** typed in; the document carries them.

### P10 — Carrier Selections *(licensed only)*
Text block (Tim's guidance, NM): contract only with the carriers below. Dental, vision and life are contracted directly through L&L for higher commission.

| Category | Carriers | Contracted through |
|---|---|---|
| Medicare Advantage | UnitedHealthcare, Devoted, BCBS, HealthSpring, Humana | Upline (Slate) |
| Med Supp & Ancillary | Mutual of Omaha, Aetna, Heartland, GTL | Upline (Slate) |
| Dental & Vision | Spirit Dental & Vision (Direct Benefits) | **L&L direct** (P11) |
| Life | *(list L&L-direct life carriers)* | **L&L direct** |

- Checkbox per carrier, all MA and Med Supp checked by default.
- Annuities: Do you sell or plan to sell annuities? Yes reveals state annuity training upload (workflow map stage 11).
- Life: interest captured now; appointments deferred to the MU Sophomore Year milestone (stage 12).
- New carrier request: free text, creates a carrier-request task.

### P11 — Spirit Dental & Vision (L&L direct) *(licensed only)*
- Text: *"Spirit is contracted directly through Loreen & Lane, not through an upline, which is what gets you the higher commission. Complete Spirit's New Mexico appointment below, then come back and check the box."*
- **Embed:** `https://appoint.directbenefits.com/Spirit/NewMexico` in an HTML/iframe block **[VERIFY IN HZ + Spirit]**.
- **Fallback if the frame comes up blank** (Spirit's site may block framing): orange button **Open Spirit Appointment (new tab)** pointing to the same URL.
- Required checkbox: *"I've submitted my Spirit Dental & Vision appointment."*
- Optional upload: Spirit confirmation screenshot or email.
- Note for the team: whatever the agent types into Spirit's page goes to Direct Benefits, not HZ. HZ only records the checkbox and upload.

**30-second embed test:** in HZ add an HTML block with
`<iframe src="https://appoint.directbenefits.com/Spirit/NewMexico" width="100%" height="900"></iframe>`, preview the form. If Spirit's page shows, keep it. If it's blank or shows "refused to connect", delete the block and use the button.

### P12 — Final Review & Signature *(licensed only)*
- Summary of answers + **outstanding items list** (anything marked "I'm obtaining this" or Pending).
- Authorization to release information to carriers for contracting and background checks.
- **Basecamp email confirmation** (prefilled from P2).
- Signature + date.

### P13 — Paused: "Let's get you licensed" *(unlicensed only)*
- Shown only when `licensed` ≠ Yes.
- Text (in Tim's voice) explaining the pause, WebCE link, Life & Health Producer selection, AHIP reimbursement after first app, and that they'll return to this same record.
- Submit button label: **Save and send my study plan**.
- On submit: status **Paused — Pre-licensing**, send **E2 test-prep email**, notify Tim (E5).

### P14 — Thank You
Two variants (§9).

---

## 5. Conditional logic (complete list)

| # | IF | THEN | Replaces Slate |
|---|---|---|---|
| L1 | Contracting as = Entity | Show entity name, TIN, principal, NPN, resident license | #18, #21, #22 |
| L2 | Mailing different = Yes | Show mailing address | #20 |
| L3 | First + Last filled | Set Full legal name = `{First} {Last}` | #1 |
| L4 | Licensed ≠ Yes | Hide P7–P12 rows (screens auto-skip); show P13 | new |
| L5 | Licensed = Yes | Hide P13 rows | new |
| L6 | Q1…Q12 = Yes | Show matching explanation field | #2, #3, #8–#17 |
| L7 | Q4 = Yes | Show supporting-docs upload, 4a, 4b, 4c | #2, #14 |
| L8 | Q4c = Yes | Show when filed, amount, which filed, settled date | #3 |
| L9 | FMO = Yes | Show current carriers + release upload | #4, #5, #6 |
| L10 | AML done = Yes | Show date + certificate upload; else show WebCE link | #7 |
| L11 | E&O = A | Show acknowledgment, video V4, live-cert button, optional upload | new |
| L12 | E&O = B | Show own-E&O upload + policy fields (required) | new |
| L13 | E&O = C | Show Next/Marla info | new |
| L14 | Banking = upload choices | Show upload field (required) | #19 (changed) |
| L15 | Annuities = Yes | Show state annuity training upload | new |
| L16 | Each document = "I'm obtaining this" | Hide its upload; add to outstanding list | new |
| L17 | Licensed ≠ Yes on submit | Send E2, set status Paused, Thank-You variant B | new |
| L18 | Licensed = Yes on submit | Send E1, E3, E4; Thank-You variant A | new |

---

## 6. Emails

Full copy is in `02_Email_Templates.md`.

| ID | Name | To | Trigger | Attachments |
|---|---|---|---|---|
| E1 | New contracting submission (internal) | tim@meuret.com, andre@meuret.com, contracts@slatefs.com, george@slatefs.com | Licensed submission received or edited | Submission PDF, uploaded files, executed NDA |
| E2 | Test-prep / study plan (to agent) | Agent | Unlicensed submission | Executed NDA |
| E3 | Welcome and next steps (to agent) | Agent | Licensed submission | Executed NDA |
| E4 | E&O certificate needed (internal) | tim@meuret.com | E&O = A | none |
| E5 | Pre-licensing agent paused (internal) | tim@meuret.com, andre@meuret.com | Unlicensed submission | Submission PDF, executed NDA |
| E6 | Outstanding documents reminder (to agent) | Agent | 7 and 14 days after submit while anything is Pending **[VERIFY IN HZ]** | none |

Slate settings to **change**:
- Sender name: "Loreen & Lane Contracting" (not "Jotform")
- Reply-to: tim@meuret.com (Slate used the applicant's email)
- Send on edit: keep on for E1 only
- Hide empty fields: on
- PDF password: on for E1 (contains SSN/TIN) **[VERIFY IN HZ]**

**Open item:** Slate (contracts@ and george@) stays on E1 because the MA and Med Supp carriers still run through the Slate upline. Remove them if those contracts move.

---

## 7. Record statuses (for the HZ submissions view)

| Status | Meaning |
|---|---|
| Paused — Pre-licensing | Contract + NDA done; studying for the exam |
| Submitted — Docs pending | Licensed; one or more items marked "I'm obtaining this" |
| Pending — L&L E&O certificate | E&O option A; waiting on Next approval + PDF |
| Ready for carrier contracting | All required items in |
| Spirit submitted | Agent checked the Spirit box |

---

## 8. Return-after-licensing path

1. E2 contains the agent's HZ resume link **[VERIFY IN HZ]**.
2. Agent passes the exam, opens the link, changes Licensing Status to **Yes**.
3. P7–P12 appear; P2, P5, P6 stay filled in, so the NDA is not re-signed unless its version changed.
4. Submit fires E1, E3 and (if chosen) E4.

If HZ can't resume an already-submitted record, use **prefill instead**: E2 links to the same form with name, email, phone and state prefilled, plus a hidden `returning=yes`. The NDA page then shows "Already signed on {date}" and skips.

---

## 9. Thank-you pages

**Variant A — Licensed**
- L&L logo, green check, "Thank you, {First}!"
- "We'll review your paperwork and get back to you shortly."
- Outstanding items list (if any)
- "Add **@meuret.com** to your safe senders list so carrier and Basecamp emails reach you." Keep the Gmail and Outlook how-to links from the Slate page:
  - Gmail: https://www.youtube.com/watch?v=x4VgK77OB2Y
  - Outlook: https://www.youtube.com/watch?v=NCV9v3HWAag
- Questions: Tim Meuret, (505) 750-7024, tim@meuret.com **(confirm the contracting contact you want shown)**

**Variant B — Paused for licensing**
- "You're on the path, {First}."
- WebCE button, what to do next, same contact block.

---

## 10. Before go-live

- [ ] Copy questions 5 and 6 (and exact wording of 1–12) from the Jotform Build tab
- [ ] NM attorney / LegalShield review of the NDA
- [ ] Run the Spirit embed test (§4 P11)
- [ ] Confirm Next change request can name an individual agent
- [ ] Confirm HZ: save-and-resume duration, second signer, date reminders, PDF password, webhooks
- [ ] List L&L-direct life carriers for P10
- [ ] Confirm thank-you contact and safe-sender domain
- [ ] Record videos V1–V5 (`03_Video_Scripts.md`)
- [ ] Test both paths end-to-end with a dummy agent (licensed and unlicensed)
- [ ] Keep the Slate Jotform live until HZ passes testing

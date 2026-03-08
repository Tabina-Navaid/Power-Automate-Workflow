# ⚙️ Fee Installments Automation Workflow - Power Automate

An end-to-end automated workflow built in **Microsoft Power Automate** for a leading university in Pakistan. The flow processes student fee installment requests submitted via Microsoft Forms — handling validation, blacklist checking, managerial approval routing, and student notifications entirely without manual administrative intervention.

---

## 🧩 Problem Statement

The university's fee installment process was entirely manual:

- Students submitted requests through informal channels
- Staff individually verified eligibility and cross-checked records
- Approvals were escalated manually to the relevant authority
- Decisions were communicated back to students by hand

This created **delays for students**, **inconsistent policy enforcement**, and **unnecessary workload** for finance and admin teams every semester.

---

## 🏗️ Workflow Architecture

The flow is structured across **five sequential stages:**

```
Microsoft Forms Submission
        ↓
Initialize FlowStatus Variable (Boolean = true)
        ↓
Apply to Each → Get Response Details → Insert Row into Excel
        ↓
Scope: Blacklist Check → Flip FlowStatus to false if matched
        ↓
Condition: FlowStatus = true?
    ├── If YES → Send Email + Start Approval
    └── If NO  → (Filtered out, no escalation)
```

---

## 📸 Workflow Screenshots

### Stage 1 & 2 — Trigger + Variable Initialization
> Flow is triggered on new form submission. `FlowStatus` Boolean variable is initialized to `true`.

<img width="1407" height="816" alt="Screenshot 2026-02-26 032757" src="https://github.com/user-attachments/assets/31a83049-2bfe-4c81-80c3-ffa35a589666" />

---

### Stage 3 & 4 — Response Retrieval, Excel Logging & Blacklist Check
> Each form response is fetched and inserted into Excel. The Scope block then retrieves blacklist rows and loops through them to check for a match.

<img width="1644" height="809" alt="Screenshot 2026-02-26 032812" src="https://github.com/user-attachments/assets/3edab7be-bc9a-4415-833c-db205183d87c" />

---

### Stage 5 — Condition Branch: Approval Routing
> If `FlowStatus` remains `true`, a notification email is sent to the student and a formal approval request is started. Blacklisted students fall into the **If No** branch and are silently filtered out.

<img width="1659" height="821" alt="Screenshot 2026-02-26 032821" src="https://github.com/user-attachments/assets/ecf156b8-fd35-462e-9cb8-fc16fedb5e6c" />

---

## 🔄 Flow Logic — Step by Step

**Step 1 — Trigger**
- Fires automatically when a student submits the **Fee Installment Form (Regular Students Spring-2026)** via Microsoft Forms
- No manual initiation required

**Step 2 — Initialize Variable**
- A Boolean variable `FlowStatus` is set to `true`
- Acts as a control flag that governs the final conditional branch

**Step 3 — Apply to Each: Response Logging**
- Loops through the list of form responses
- Retrieves full response details for each submission using the Form ID
- Inserts each submission as a new row into a connected **Excel sheet** for structured record-keeping

**Step 4 — Scope: Blacklist Check**
- Retrieves all rows from a separate blacklist reference sheet
- Loops through each row using a nested **Apply to Each 2**
- If the submitting student matches a blacklist entry, `FlowStatus` is flipped to `false`

**Step 5 — Condition: Approval Routing**
- Evaluates whether `FlowStatus` equals `true`
- **If Yes:** Sends an email notification to the student → starts a formal approval using Power Automate's built-in approval action → routes to the relevant authority → waits for response before executing the final condition
- **If No:** Student is filtered out silently — no escalation occurs

---

## 📈 Business Outcomes

- **Eliminated manual handling** of fee installment requests entirely for the semester
- Submissions processed in **real time** — no administrative bottleneck
- **Blacklisted students** automatically filtered before any escalation occurs
- **Eligible students** receive immediate confirmation and enter the approval queue automatically
- Finance team has a **clean, structured Excel record** of every request each semester
- **Consistent policy enforcement** across all submissions with zero human error

---

## 🧰 Stack & Tools

| Component | Technology |
|-----------|-----------|
| **Workflow Automation** | Microsoft Power Automate |
| **Form Intake** | Microsoft Forms |
| **Record Keeping** | Microsoft Excel (via Power Automate connector) |
| **Approval Routing** | Power Automate Approvals |
| **Notifications** | Outlook / Send an Email action |
| **Logic Control** | Boolean variable + Condition blocks + Scoped loops |

---

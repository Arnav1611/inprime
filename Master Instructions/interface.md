# interface.md

Screens and elements to be designed. The runtime rules for each live in the agent files — this is
the inventory, not the behaviour.

## 1 · Onboarding

Fixed. Nothing added, nothing removed.

Splash → language → walkthrough videos → mobile and OTP → occupation selection.

**No permission is asked here.** Every connector is requested later, in the thread.

| Also needed | |
|---|---|
| OTP states | Wrong code, resend, timeout, number already registered, code not received |
| Occupation | Search, and a path for an occupation not on the list |
| Walkthrough | One set per language. Skippable |
| Returning user | Splash straight to the last chat |

## 2 · Connections and permissions

Bottom sheets. Every one says **why** it is needed and **what** it unlocks, in that order. Connect
and Not now carry equal weight.

| Connector | Journey |
|---|---|
| Location | Why and what → permission. Captured once. Not continuous |
| SMS | Why and what → permission |
| Credit bureau | Why and what → PAN → fetch → show the score |
| Account aggregator | Why and what → vendor journey → return and confirm linked accounts |

| Also needed | |
|---|---|
| Declined | What the sheet says, and how the customer returns to it later |
| Bureau: no record found | The most likely outcome for this customer. Not an error screen |
| Bureau: PAN mismatch, name mismatch, multiple matches | Three separate outcomes |
| Aggregator: partial linking | Some accounts linked, some not |
| Disconnect and withdraw consent | Required. Lives in the connectors view |
| DigiLocker, QR settlement | Both are connectors with no sheet designed yet |

## 3 · Chat interface

### Elements

Headings L1–L3 · body · italic · bold · underline · strikethrough · blockquote · nested lists ·
tables · comparison view · highlighted text · callouts · image carousel · video carousel · video
embed · regular URL · CTA button with text · file download CTA · share on replies and artifacts ·
question nudges with and without emoji · upload from camera, file and image · mic with running
visual · new chat and delete chat.

`story.md` governs when each is used. The default reply stays plain.

### Artifact in the thread — not yet designed

The largest open piece. Artifact designs exist; how they sit in the stream does not.

- Width, margins, behaviour on scroll
- What a tap does on a display-only artifact
- Two artifacts stacked, for the paired cases
- Expandable sections — balance first, each further section on request
- An artifact in a partial or failed state

### Chat states

| State | |
|---|---|
| Clean hero | No alert, no key info |
| Hero with key info | Overdue, new loan, income |
| Persistent alert | Stays until resolved. Most serious first, one at a time |
| Response streaming | And a stop control |
| Empty | First-ever chat, and a new chat — different |
| Offline | Question saved, sends later. Old threads readable |
| Voice transcript confirmation | Required before acting on an amount, a date or a lender name |
| Message actions | Copy, share, feedback, long-press menu |

## 4 · Other surfaces

| Surface | |
|---|---|
| Profile | Sign out, dark mode, language |
| Connectors view | Status, connect, disconnect, withdraw consent |
| Chat list | Sidebar, with search |
| Section entry points | Loans, income, reminders, credit score. Placement to be settled |
| Full-screen views | Full bureau report as scrollable PDF, full bank statement, repayment schedule |
| Notifications | Push, plus an in-app centre. Four bureau alerts fire unprompted and nothing carries them today |
| Reminders | Where a set reminder lives after it is set |
| Documents | Key Facts Statement, sanction letter, loan agreement |
| Grievance and escalation | Grievance officer, ombudsman. Required, and not only through the assistant |
| Account deletion | Required |

## Cross-cutting

- **Three languages.** Kannada and Hindi run roughly 40% longer. Review every layout in all three
  before build. A label that does not translate gets changed, not shrunk
- **Counter phone.** Small screen, one hand, bright light, slow network
- **Reads slowly, reads English barely.** Tap targets and type size follow from that

## Open decisions

| Decision | Why it matters |
|---|---|
| Dark mode in the first release | Doubles the surface across every artifact and element |
| Tables and comparison view versus the artifact rule | A table compares; it never presents one record. Confirm the boundary before build |
| What location is used for | Nothing reads it yet. Name the use before asking for it |
| Subscription and paywall screens | Only if the freemium model ships |
| Name capture | Dropped from onboarding. Captured later, or not at all |

<div align="center">

<img src="https://img.shields.io/badge/Live-nesprnt.in-e8410a?style=for-the-badge&logo=google-chrome&logoColor=white" />
<img src="https://img.shields.io/badge/Status-Production-0a8a4a?style=for-the-badge" />
<img src="https://img.shields.io/badge/Users-136%20Students-1a52e8?style=for-the-badge" />
<img src="https://img.shields.io/badge/Backend-Supabase%20Edge%20Functions-3ECF8E?style=for-the-badge&logo=supabase&logoColor=white" />

<br/><br/>

```
███╗   ██╗███████╗███████╗██████╗ ██████╗ ███╗   ██╗████████╗
████╗  ██║██╔════╝██╔════╝██╔══██╗██╔══██╗████╗  ██║╚══██╔══╝
██╔██╗ ██║█████╗  ███████╗██████╔╝██████╔╝██╔██╗ ██║   ██║   
██║╚██╗██║██╔══╝  ╚════██║██╔═══╝ ██╔══██╗██║╚██╗██║   ██║   
██║ ╚████║███████╗███████║██║     ██║  ██║██║ ╚████║   ██║   
╚═╝  ╚═══╝╚══════╝╚══════╝╚═╝     ╚═╝  ╚═╝╚═╝  ╚═══╝   ╚═╝   
```

### **The Official Student Print Mediator**
*A production-grade, full-stack print order management platform serving 136 students at Amrita Vishwa Vidyapeetham*

<br/>

[🌐 Live App](https://nesprnt.in) · [✨ Features](#-features) · [🏗️ Architecture](#️-architecture) · [🔒 Security](#-security-design) · [🚀 Tech Stack](#-tech-stack)

</div>

---

## 🧠 The Origin Story

> *"From WhatsApp Chaos to a 90+ Feature Production System with End-to-End Security."*

In an era dominated by AI agents and LLMs, I chose to solve a small real-world problem that grew bigger than I expected — one I lived through for multiple semesters and decided to fix myself. The solution ended up having a bigger impact than I ever imagined.

---

### The Problem

Every semester during exams, I faced the same situation — **10 to 20 classmates sending PDFs on WhatsApp**, asking me to handle their printouts. As a day scholar, I had to go to a nearby print shop, sit there for nearly **60 minutes**, manage multiple PDFs, calculate pages manually, and coordinate everything in real time.

---

### 🔁 How It Escalated

| Semester | Reality |
|---|---|
| **1st time** | Manageable — a few friends, small load |
| **2nd time** | Load exploded — more PDFs, more payments, more time |
| **3rd time** | Started avoiding requests due to complete overload |
| **4th time** | Same chaos heading my way again |

---

### 🟡 The Real Chaos

What looked like *"just one printout"* per person quickly became an overwhelming operational mess:

- Managing multiple PDFs simultaneously with no structure
- Manually counting pages and calculating costs on the spot
- Handling constant calls: *"Did my payment go through?"*
- Tracking payments with no system — just memory and WhatsApp history
- Wrong files sent, wrong pages printed, wrong amounts collected

**Complete operational chaos. Every single semester.**

---

### 💡 The Realization

> *This isn't a printing problem. This is a system design problem.*

On the 4th time, instead of avoiding the situation again, I asked one question:

**"What if I build a system to make this disappear entirely?"**

```
Manual system  →  O(n × chaos)
This system    →  O(1 structured flow)
```

---

### 🚀 What I Built

A **Workflow Automation System** that eliminates manual coordination entirely — transforming semester-chaos into a structured, automated pipeline.

```
Student  →  Upload PDFs  →  Customize  →  Pay  →  Track  →  Collect
   ↓
System   →  Validate  →  Calculate  →  Store  →  Update Status
   ↓
Admin    →  Verify  →  Process  →  Notify  →  Delivery
```

---

### 🔄 Before vs After

| Before | After |
|---|---|
| WhatsApp PDFs with no order | Structured upload system |
| Manual page counting | Auto page detection & pricing |
| *"Did my payment go through?"* calls | Real-time order tracking |
| Payment confusion, no receipts | Clear UPI confirmation + Order ID |
| Wrong PDFs printed | Thumbnail preview before submit |
| Binding confusion | Per-PDF customisation |
| **45–60 minutes of chaos** | **Under 5 minutes, structured** |

---

### ⚡ The Result

This didn't just fix a process — **it eliminated the complexity entirely.**

Every semester what started as helping friends with printouts evolved into a full production system with end-to-end security, built to scale. A system I designed and built from a problem I personally experienced.

> This isn't just a project — it's a production-ready system, used and tested by real users.
>
> What started as a frontend-driven solution is now a backend-driven system with proper APIs, role-based access, and a real revenue layer.
>
> **I didn't just build a project. I designed a scalable system.**

---

**Nesprnt eliminates all of that.**

Students log in with their college email, upload PDFs, configure per-document print settings, pay via UPI, and get a tracked Order ID — all in under 2 minutes. The admin verifies payments, sends print instructions to the shop via WhatsApp with one tap, and students are notified by SMS when their order is ready.

> Built solo. Deployed to production. Used by real people 

---

## 🏗️ Architecture

```
┌─────────────────────────────────────────────────────────┐
│                    Student Browser                       │
│  Single HTML file — zero frameworks, zero build step    │
│  PDF.js (client-side PDF processing & thumbnails)       │
└──────────────────────┬──────────────────────────────────┘
                       │  HTTPS POST  (JSON)
                       │  x-api-secret header (every req)
                       │  Authorization: Bearer JWT (admin only)
                       ▼
┌─────────────────────────────────────────────────────────┐
│           Supabase Edge Function  (Deno / TypeScript)    │
│                   printdesk-api                          │
│                                                          │
│  • API secret validation  (all requests)                │
│  • HMAC-SHA256 JWT verification  (admin requests)       │
│  • Business logic + rate limiting                       │
│  • Student ownership verification                       │
│                                                          │
│  All secrets live HERE only — never in the browser      │
└──────────┬──────────────────────────┬───────────────────┘
           │                          │
           ▼                          ▼
┌──────────────────┐      ┌─────────────────────────────┐
│  PostgreSQL DB   │      │     Supabase Storage         │
│                  │      │   (private PDF bucket)       │
│  orders          │      │                              │
│  students        │      │  orders/{id}/file.pdf        │
│  settings        │      │  signed URLs, 1hr expiry     │
│  feedbacks       │      │                              │
└──────────────────┘      └─────────────────────────────┘
```

### Why a single HTML file?

136 students. One department. A React app would have a build pipeline, `node_modules`, deployment configs, and 200KB of JavaScript runtime for a problem that needs none of that. One HTML file loads faster, deploys in seconds, has zero dependencies to break, and is something I can maintain completely solo. **Complexity should match the problem.**

---

## 🔒 Security Design

Security was not an afterthought. Every decision has a reason.

### No Supabase SDK in the browser
The Supabase JS client requires exposing a `service_role` or `anon` key in the frontend. Anyone with DevTools can steal it and query your entire database directly. The solution: **remove the SDK from the browser entirely.** Every database call goes through a Supabase Edge Function that holds all credentials as environment variables — invisible to any user.

### Two-layer API security

| Layer | Mechanism | Protects against |
|---|---|---|
| **Layer 1** | `x-api-secret` header on every request | Random internet requests to the Edge Function |
| **Layer 2** | HMAC-SHA256 signed JWT (admin actions only) | Unauthorized access to admin operations |

### JWT implementation
Admin JWT is signed server-side using the **Web Crypto API** (native to Deno) with HMAC-SHA256. It's stored **in JavaScript memory only** — not localStorage, not cookies, not sessionStorage. Refresh the page and it's gone. Expires in 2 hours. Even if someone opens DevTools during an admin session, they cannot persist the token.

### Student identity verification
- Email regex enforces college email format before any server call
- Roll number extracted from email and verified against the `students` table
- Name fuzzy-matched against the registered name to prevent impersonation
- Every `studentDeleteOrder` call verifies server-side that the order belongs to that student AND is in `cancelled` status — students cannot delete active orders or other students' data

### Brute force protection
5 failed admin login attempts → 30-second client-side lockout. Server-side, a forged JWT without the correct `JWT_SECRET` is cryptographically invalid regardless of how many attempts are made.

### XSS prevention
Two sanitization layers: `esc()` for anything rendered into `innerHTML`, `sanitize()` for user inputs sent to the backend. Every user-supplied string is treated as untrusted.

---

## ✨ Features

<details>
<summary><strong>🔐 Authentication (5 features)</strong></summary>

- College email-only login with strict regex validation
- Auto roll number extraction from email (no manual entry)
- Database-backed verification against the students table
- Persistent session via localStorage — no repeated logins
- Full-screen gate that cannot be bypassed

</details>

<details>
<summary><strong>📝 Order Form — Progressive UX (5 features)</strong></summary>

- Step-by-step field unlocking: name → section → student ID → PDFs → payment
- Server-verified name matching (fuzzy word-level check)
- Student ID regex validation with helpful format hint
- 4-step visual progress bar with live active/done states
- All validation errors surface inline with specific messages

</details>

<details>
<summary><strong>📄 PDF Processing — Client-Side (12 features)</strong></summary>

- Up to 5 PDFs, 30MB each, PDF-only enforced
- Drag & drop + click-to-upload on the same zone
- Duplicate filename detection
- Live page count extraction via PDF.js (in-browser, no upload needed)
- Page cap at 80 pages per PDF
- First-page thumbnail preview rendered from PDF canvas
- Password-protected PDF detection with specific error message
- Corrupted/invalid PDF detection
- Per-PDF scanning status indicator (Scanning → Ready / Error)
- Individual file removal without clearing others
- PDF count badge (2 / 5)
- All error PDFs blocked from submission with named list

</details>

<details>
<summary><strong>🖨️ Print Customisation (5 features)</strong></summary>

- Per-PDF print sides: all single / all double / first-single rest-double
- Per-PDF binding: pins (free) or spiral (+₹25)
- Print Details card locked until ALL PDFs are individually customised
- Live sheet count formula per PDF based on sides selection
- Plain-language description: "10 pages → 5 sheets (all double-sided)"

</details>

<details>
<summary><strong>💰 Pricing & Payment (9 features)</strong></summary>

- B&W (₹1.50/sheet) or Colour (₹8.00/sheet) — applies to all PDFs
- Live total recalculates on every change
- Per-PDF cost breakdown table for multi-file orders
- Spiral binding line item with count
- UPI number display with one-tap copy
- Page Visibility API — detects when student returns from payment app and pulses the "I Paid" button
- Pre-generated Order ID displayed before submission
- Payment proof entry (phone + UPI name for admin matching)
- Client + server-side rate limit: max 3 orders per student per day

</details>

<details>
<summary><strong>📤 Submission & Upload (5 features)</strong></summary>

- Base64 PDF upload via Edge Function (never touches storage directly from browser)
- Per-file retry logic: 3 attempts with 1.5s delay, shows "retry 2/3" in UI
- Live upload progress: "Uploading 2 of 3...", "Saving order..."
- Atomic order creation: all PDFs uploaded before order row inserted
- If any upload fails, order is never created (no orphaned partial records)

</details>

<details>
<summary><strong>🔍 Order Tracking (6 features)</strong></summary>

- Public tracking by Order ID + Student ID (prevents tracking others' orders)
- Auto-uppercase input as student types
- Enter key triggers search from either field
- Full order details card
- 4-stage visual timeline with done/active/waiting states
- Timestamps shown on completed steps (verified at, printed at)

</details>

<details>
<summary><strong>📦 My Orders — Cross-Device (5 features)</strong></summary>

- Orders fetched from DB by roll number — works on any device (like Amazon/Flipkart)
- Full order cards with per-PDF details
- Cancel pending orders (sends WhatsApp refund request to admin)
- Delete cancelled orders (server-verified ownership + status before deletion)
- Loading state with empty state messaging

</details>

<details>
<summary><strong>🔐 Admin Dashboard (17 features)</strong></summary>

- Hidden access: `A+D+M` keys (desktop) or 5 logo taps (mobile)
- Email + password login, credentials verified server-side
- 5-attempt brute force lockout (30 seconds)
- JWT session: memory-only, 2-hour expiry, auto-logout on expiry
- Stats tiles: Total / Pending / Verified / Revenue
- Filter tabs: All / Pending / Verified / Printed / Cancelled (with badge counts)
- Order detail modal with full info + payment matching box
- Verify order: confirmation modal → WhatsApp opens + PDFs auto-download
- WhatsApp message auto-generated with all print instructions
- PDFs downloaded with 400ms stagger (prevent browser blocking)
- Mark as Printed
- SMS to student on ready
- Bulk WhatsApp: all verified orders in one formatted message
- Refund Done: marks DB, disables button, SMS to student
- Delete order: removes DB row + Storage files
- Manual refresh
- Logout clears JWT from memory

</details>

<details>
<summary><strong>⏰ Order Cutoff System (6 features)</strong></summary>

- Admin sets daily open/close times, saved to DB and synced to all devices
- Live status chip in hero: green "open till X" or red "closed, opens X"
- Form auto-hides when closed; closed banner shows next opening time
- Force-open override button (bypasses schedule instantly)
- Cutoff re-checked every 60 seconds (form closes automatically)
- Remote cutoff fetched on every page load

</details>

<details>
<summary><strong>💬 Feedback System (10 features)</strong></summary>

- Post-order feedback form (shown on success screen)
- 5-star rating with interactive highlight
- 6 feedback categories
- Free-text message
- Saved to `feedbacks` table via Edge Function
- Admin panel: stats (total, avg rating, unread count)
- Filter tabs: All / Unread / 5-star / Low rating
- Mark individual as read
- Mark all as read
- Delete individual feedback

</details>

<details>
<summary><strong>📱 PWA & Performance (16 features)</strong></summary>

- Installable PWA (manifest.json + service worker)
- Theme color in mobile browser chrome
- Critical CSS inlined in `<head>` (login screen has zero FCP delay)
- Non-blocking font loading (media="print" trick)
- `defer` on PDF.js and QRCode.js
- DNS preconnect for Supabase, Google Fonts, GA4
- Web Vitals (CLS, INP, FCP, LCP, TTFB) → GA4
- Google Analytics 4 with async loading
- SEO: title, description, Open Graph, robots, author, Google verification
- Schema.org JSON-LD structured data (SoftwareApplication)
- Sticky topbar with frosted glass backdrop-filter
- Custom 4px scrollbar
- Smooth scroll
- XSS protection: `esc()` + `sanitize()` on all user inputs
- Zero secrets in frontend — all in Edge Function env vars
- Responsive mobile-first design

</details>

---

## 🚀 Tech Stack

| Category | Technology | Why |
|---|---|---|
| **Frontend** | Vanilla HTML/CSS/JS | Zero build step, instant deploy, fastest load for the use case |
| **Backend** | Supabase Edge Functions (Deno) | Serverless, runs at edge, TypeScript, free tier |
| **Database** | Supabase PostgreSQL | Relational queries, real-time capable, free tier |
| **Storage** | Supabase Storage | S3-compatible, private buckets, signed URL generation |
| **PDF Processing** | PDF.js 3.11 | Client-side page counting + thumbnail rendering — no server load |
| **Auth** | Custom HMAC-SHA256 JWT | Signed server-side with Web Crypto API, no third-party auth dependency |
| **Analytics** | Google Analytics 4 | Web Vitals + user flow tracking |
| **Fonts** | Syne + DM Sans (Google Fonts) | Non-blocking load, distinctive typographic pairing |
| **Hosting** | Static (nesprnt.in) | Single HTML file, trivially deployable anywhere |

---

## 🗄️ Database Schema

```sql
-- Pre-seeded with 136 registered students
students (
  roll_number  TEXT PRIMARY KEY,   -- AV.SC.U4CSE2XXXX
  name         TEXT NOT NULL
)

-- Every print order
orders (
  order_id     TEXT PRIMARY KEY,   -- PD7T0XS (generated client-side)
  name         TEXT,
  section      TEXT,               -- CSE-A / CSE-B
  student_id   TEXT,               -- matches students.roll_number
  pages        INTEGER,
  print_type   TEXT,               -- 'bw' | 'color'
  total        NUMERIC,
  pdf_names    TEXT,               -- comma-separated filenames
  pdf_paths    TEXT[],             -- storage paths array
  pdf_count    INTEGER,
  pdf_sides    TEXT,               -- per-PDF sides, comma-separated
  binding      TEXT,               -- per-PDF binding, comma-separated
  pay_phone    TEXT,               -- UPI phone for payment matching
  pay_name     TEXT,               -- UPI name for payment matching
  status       TEXT,               -- pending|verified|printed|cancelled
  refunded     BOOLEAN,
  created_at   TIMESTAMPTZ,
  verified_at  TIMESTAMPTZ,
  printed_at   TIMESTAMPTZ,
  refunded_at  TIMESTAMPTZ
)

-- Order open/close schedule
settings (
  key    TEXT PRIMARY KEY,         -- 'cutoff'
  value  TEXT                      -- JSON: {open, close, override}
)

-- Student feedback
feedbacks (
  id           TEXT PRIMARY KEY,
  order_id     TEXT,
  rating       INTEGER,            -- 1-5
  category     TEXT,
  message      TEXT,
  submitted_at TIMESTAMPTZ
)
```

---

## 🔄 Complete Order Lifecycle

```
Student logs in (college email → roll number → DB verify)
        │
        ▼
Fills Info (name verify → section → student ID)
        │
        ▼
Uploads PDFs (client-side scan: pages, thumbnail, validation)
        │
        ▼
Customises each PDF (sides + binding, price updates live)
        │
        ▼
Pays via UPI → enters phone + name as proof
        │
        ▼
Submits → PDFs uploaded to Storage → order row inserted (status: pending)
        │
        ▼
Admin sees order → verifies payment against UPI records
        │
        ▼
Admin clicks Verify → WhatsApp opens + PDFs auto-downloaded (status: verified)
        │
        ▼
Admin forwards to print shop via WhatsApp
        │
        ▼
Admin marks Printed → SMS sent to student (status: printed)
        │
        ▼
Student collects printout ✅
```

---

## 📊 Key Technical Decisions & Trade-offs

### Decision 1: No Supabase SDK in browser
**Problem:** Exposing Supabase keys in frontend JS is a critical security risk — anyone can steal them from DevTools and get full database access.

**Solution:** Removed the SDK entirely from the browser. Created a single Edge Function (`printdesk-api`) that proxies all database operations. The frontend never touches Supabase directly.

**Trade-off:** Every database call has one extra network hop through the Edge Function. Acceptable because Edge Functions run at Supabase's edge servers (geographically close) and the added latency is ~10-20ms.

---

### Decision 2: Client-side PDF processing
**Problem:** If PDFs were uploaded first for page counting, students would wait through an upload just to see a price estimate. That's bad UX and wastes bandwidth.

**Solution:** PDF.js runs entirely in the browser — page counting, validation, thumbnail generation — before any network request is made. Students see instant page counts and price estimates.

**Trade-off:** PDF.js is a ~400KB script. Mitigated by loading it with `defer` and only using it after the student has already interacted with the form (not a cold-load cost).

---

### Decision 3: Memory-only admin JWT
**Problem:** Storing admin JWT in localStorage means if the device is shared or a browser extension reads localStorage, the admin session is compromised indefinitely.

**Solution:** JWT stored only in a JavaScript variable (`let _adminJWT`). It disappears on page refresh, tab close, or after 2 hours. Zero persistence.

**Trade-off:** Admin has to log in again after every page refresh. Acceptable for a security-sensitive admin panel.

---

### Decision 4: Per-student server-side delete verification
**Problem:** A student could theoretically call `deleteOrder` with any order ID if there was no ownership check.

**Solution:** `studentDeleteOrder` runs three checks server-side: does the order exist, does the `student_id` match the requester, and is the status `cancelled`? All three must pass. The frontend check is just UX — the backend is the actual gate.

---

## 📁 Project Structure

```
nesprnt/
├── index.html                  # Entire frontend — one file
│   ├── <head>                  # Critical CSS, PWA meta, GA4, fonts
│   ├── Login overlay           # Email-based auth gate
│   ├── Student page (#pgS)     # Order form + success screen
│   ├── Track page (#pgT)       # Order status + timeline
│   ├── My Orders page (#pgMO)  # Cross-device order history
│   ├── Admin page (#pgA)       # Dashboard + feedback panel
│   ├── Modals                  # Detail / Confirm / Delete
│   ├── Bottom nav              # Print / Track / Admin
│   └── <script>                # All application logic (~1800 lines)
│
├── index.ts                    # Supabase Edge Function (TypeScript)
│   ├── JWT helpers             # signJWT / verifyJWT (Web Crypto API)
│   ├── API secret check        # All requests
│   ├── JWT check               # Admin-only actions
│   └── 18 action handlers      # All business logic
│
├── manifest.json               # PWA manifest
└── sw.js                       # Service worker
```

---

## 🌐 Live Metrics

- **136 registered students** across CSE-A and CSE-B sections
- **Single Edge Function** handles all 18 API actions
- **Zero server costs** — fully on Supabase free tier
- **Sub-2-minute** average order placement time
- **100% UPI-based** — no cash, full digital payment trail

---

## 👤 Built By

**G Vamsi Reddy**
B.Tech CSE — Amrita Vishwa Vidyapeetham, Amritapuri

Built, designed, deployed, and maintained solo. Every line of code, every security decision, every UX detail — one person.

[![Instagram](https://img.shields.io/badge/@nesprnt__-E4405F?style=flat&logo=instagram&logoColor=white)](https://www.instagram.com/nesprnt_)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-0077B5?style=flat&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/g-vamsi-ab87113ba)
[![Website](https://img.shields.io/badge/nesprnt.in-e8410a?style=flat&logo=google-chrome&logoColor=white)](https://nesprnt.in)

---

<div align="center">

**If you're a recruiter reading this:**

This project is not a tutorial follow-along. It is not a clone. It is a real product, solving a real problem, used by real people, built with deliberate technical decisions made by one person from scratch.

*Every feature listed above is live and working at [nesprnt.in](https://nesprnt.in)*

</div>

## 📄 License

Nesprnt Student Print Mediator License
Copyright (c) 2026 Vamsi Reddy

All Rights Reserved.

This project, including its source code, documentation, design, and associated materials,
is the intellectual property of the author.

Permission is granted to:
- View and read the code and documentation for educational and evaluation purposes
- Fork the repository for personal, non-commercial use
- Share the repository link with proper attribution

The following are strictly prohibited without prior written permission from the author:
- Reproducing, copying, or redistributing the project in whole or in part
- Using the project or its code for commercial purposes
- Deploying, hosting, or offering this system as a service
- Creating derivative works intended for public or commercial use

This project is published as a case study and portfolio work to demonstrate
problem-solving, system design, and real-world application development.

For permissions, contact:
[vamsireddygnt11@gmail.com]

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED,
INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE,
AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHOR BE LIABLE FOR ANY CLAIM, DAMAGES,
OR OTHER LIABILITY ARISING FROM THE USE OF THIS SOFTWARE.

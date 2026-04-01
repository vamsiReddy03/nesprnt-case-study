🖨️ Nesprnt — Workflow Automation System Case Study

> In an era dominated by AI agents and LLMs ,I chose to solve a small real-world problem that grew bigger than I expected." — one I lived through for multiple       semesters and I decided to solve it myself. The solution I built ended up having a bigger impact than I initially imagined."
  this project focuses on solving a real-world **last-mile problem**

> 🚀 Overview

Nesprnt is a production-grade workflow automation system built to replace a chaotic, manual print coordination process used by multiple 
students during exam cycles.

What started as a small coordination task quickly evolved into a high-volume operational problem.
Instead of optimizing the manual process, I eliminated it through system design and automation.

---

## 😤 The Problem

Every semester, exam season meant one thing — 10 to 20 students sending me PDFs on WhatsApp to coordinate printing.
Initially manageable, the process quickly became chaotic.

---
## 🟡 The Chaos
What looked like "just one printout" per person quickly turned into a overwhelming mess I couldn't handle alone..

At the print shop, I had to:
- Manage multiple PDFs  
- Count pages manually  
- Calculate cost for each student  
- Track payments manually  
- Handle constant phone calls  
- Deal with last-minute changes  

👉 This turned into **complete operational chaos**
---
## 🔁 The Journey

**1st time:**  
Small scale — manageable  

**2nd time:**  
More users → more PDFs → more confusion  

**3rd time:**  
Reduced involvement due to overload  
  
---
## 💡 The Realization

> This is not a printing problem. This is a **system design problem**.

---

**4th time:** 
Same chaos heading my way again. I asked:
"What if I build a Mobile Web App to make this disappear entirely?"
🚀 So I built Nesprnt 

Key Insight

This was not a printing problem — it was a workflow orchestration problem.

The issue was not the task itself, but the lack of a structured system to handle:

Multi-user input
State transitions
Payment confirmation
Order tracking
Admin-side execution

## 🚀 The Solution — Nesprnt

A complete workflow automation system:

**Upload → Customize → Pay → Track → Collect**

---

⚙️ System Architecture

The system was designed as a state-driven workflow engine, not just a UI application.

Core Components:
Frontend: Mobile-first interface for structured user input
Backend: Supabase (PostgreSQL) for state and data management
Storage: Secure PDF handling with signed URLs
Workflow Engine: Order lifecycle management
Automation Layer: Payment confirmation and notifications
Order Lifecycle:
Pending → Verified → Printed → Completed

## 🔄 What Changed

| Old System               | New System              |
|--------------------------|-------------------------|
| WhatsApp PDF chaos       | Organized upload system |
| Manual page counting     | Auto page detection |
| Manual price calculation | Auto pricing engine |
| Constant calls           | Real-time tracking |
| Payment confusion        | UPI confirmation |
| No order records         | Full order history |
| Follow-ups               | SMS notifications |
| Wrong PDFs               | Thumbnail preview |
| Binding confusion        | Per-PDF customization |
| Admin overload           | Bulk automation |

---

📊 Impact
⏱ Reduced execution time from ~60 minutes → ~5 minutes
📉 Eliminated manual coordination and follow-ups
🔁 Converted a chaotic workflow into a repeatable system
👥 Used by real users in live scenarios
⚙️ Reduced human dependency through automation

** Features (90+) Workflow Automation 

**🔑 Student Login & Access Control**

- College email login page before website access
- Amrita email format validation 
- Roll number extracted from email → verified against Supabase `students` table
- Login saved permanently on device via localStorage
- Outsiders with any other email → completely blocked
- Mobile keyboard auto-suggests email (`type="email"`, `autocomplete="email"`)
- Enter key triggers login directly
- Terms line — "By using Nesprnt, you agree to pay the fixed rate"
- RLS policy — student list never exposed to browser
- Returns only `ok: true/false` — never actual student data

---

**📄 PDF Management**

- Upload up to 5 PDFs (max 30MB)
- Auto page detection via PDF.js
- Thumbnail preview per PDF
- Duplicate PDF detection
- Corrupted PDF blocking
- Password-protected PDF blocking
- Per-PDF customization (sides + binding)
- PDF count badge display
- Remove individual PDF button
- Page alert when no PDFs uploaded

---

**⚙️ Print Customization**

- All single sided , All double sided
- 1st single, rest double
- Pins binding (free)
- Spiral binding (+₹25)
- Live sheet calculation per PDF
- Per-PDF sides and binding description update

---

**💰 Pricing Engine**

- B&W ₹1.50/sheet
- Colour ₹8.00/sheet
- Per-PDF price breakdown
- Spiral binding auto charge
- Live total update
- Live sheet count update
- Price summary display with breakdown

---

**📱 Payment Flow**

- UPI phone number display
- UPI copy button with confirmation
- "I Have Paid" confirmation button
- Payer name field
- Payer phone number field
- Order ID auto generation (`PD` + timestamp)
- Progressive step reveal (Step 1 → 2 → 3 → 4)
- Payment pulse animation
- Step progress bar sync

---

**🔍 Order Tracking**

- Real-time status fetch from Supabase
- Timeline view (Pending → Verified → Printed)
- Student ID verification before showing order
- Order not found error handling
- Student ID mismatch error handling
- Verified at timestamp display
- Printed at timestamp display

---

**📦 My Orders**

- Live status fetch from Supabase on open
- Per-PDF details per order
- Cancel order before verification
- Confirm dialog before cancel
- Delete cancelled orders from list
- Refund request via WhatsApp to admin
- Deleted/completed orders show "✅ Order Completed — Ready to Collect"
- Orders saved on device (up to 20)
- Shows order count on device

---

**🔐 Admin Panel Access**

- Email + password login form
- Brute force lock — 30 sec after 5 wrong attempts
- Lockout countdown message
- Logout button
- Admin nav button hidden from students

---

**📋 Admin Order Management**

- Load all orders from Supabase
- 5 status filters (All, Pending, Verified, Printed, Cancelled)
- Order details modal (name, section, student ID, pages, amount, PDF files)
- Per-PDF print instructions in detail view
- Payment details box (phone, name, amount)
- Verify order button
- WhatsApp dispatch per order
- Bulk WhatsApp dispatch (all verified orders + grand total)
- Mark as printed button
- SMS notify → turns green "✅ SMS Sent" after clicking
- UPI number masked (`****12345`) in order list
- Refund done button
- Cancelled orders tab
- Delete order (with PDF file cleanup from storage)
- Stats dashboard (total, pending, verified, printed, cancelled, revenue)
- Refresh button

---

**📲 SMS & WhatsApp**

- SMS Manual notify to student when order ready
- WhatsApp message per order with full details
- Bulk WhatsApp with all verified orders + grand total + B&W/colour/spiral counts
- Refund SMS notification Manual to student
- Cancel request via WhatsApp to admin

---

**⏰ Time Control**

- Open/close timing set by admin
- Supabase synced — works across all devices
- Override button — force open/close outside hours
- Closed banner shown to students when closed
- Cutoff loaded on page load from backend
- Cutoff saved to localStorage for offline check

---

**💬 Feedback System**

- Star rating (1-5)
- Category selection
- Feedback message text area
- Submit feedback to Supabase
- Admin feedback management panel
- Unread feedback badge on admin nav
- Filter by all/unread/5-star/low rating
- Mark individual feedback as read
- Mark all as read
- Delete feedback
- Total feedback count display
- Average rating display

---

**🔒 Security**

- College email login — outsiders blocked
- Backend rate limiting — max 3 orders/day (server-side, not bypassable)
- SHA-256 password hashing
- Salt encryption
- XSS sanitization on all inputs (name, section, student ID, phone, payer name)
- Brute force lock — 30 sec cooldown after 5 wrong admin attempts
- RLS policies on all 4 database tables
- CSP headers
- HTTPS only
- Signed PDF URLs expire in 1 hour
- All secrets in Supabase environment — never in browser
- Student data returns only `ok: true/false` — never actual list
- SQL injection safe — regex validation + parameterized queries + string comparison for admin
- No duplicate IDs in HTML

---

**🌐 SEO & Google**

- Title → `Nesprnt | The Official Student Print Mediator`
-'Nesprnt' is totally a Ghost Name
- Meta description
- Open Graph tags (`og:title`, `og:description`, `og:url`, `og:type`)
- Software Application Schema markup with aggregate rating
- Google site verification meta tag ✅
- Google Search Console verified ✅
- Sitemap submitted ✅
- `robots` meta tag — index + follow
- `author` meta tag

---

**🔗 Brand & Identity**

- Instagram icon in footer → `nesprnt_`
- LinkedIn icon in footer → your profile
- Hover effects on social icons (orange for Instagram, blue for LinkedIn)
- PWA meta tags (theme color `#e8410a`, Apple web app capable)
- `manifest.json` with Nr logo
- `icon-192.png` + `icon-512.png` — Nr brand icons
- Footer copyright with auto-updating year
- Copyright Act 1957 notice

---

**⚙️ Edge Function (16 Actions)**

---

**🚀 Deployment & Infrastructure**

- Vercel hosting
- Custom `nesprnt.in` + `www.nesprnt.in` domain
- GitHub → Vercel auto-deploy pipeline
- Supabase Edge Function (Deno/TypeScript)
- DNS fixed on GoDaddy
- ₹0 hosting cost

---

**📊 Final Stats**

- ⚡ 100+ features
- 🔒 15+ security layers
- 🗄️ 4 database tables with RLS
- ⚙️ 16 Edge Function actions
- 🧪 Live tested with real classmates
- 🐛 Continuously bug fixed
- 💰 ₹0 hosting cost
- 📱 100% mobile responsive
- 🌐 Live on Google — nesprnt.in 🎉

## 🛠️ Tech Stack

| Layer         | Technology            |
|---------------|-----------------------|
| Frontend      | HTML, CSS, JavaScript |
| Backend       | Supabase (PostgreSQL) |
| Storage       | Supabase Storage      |
| PDF Processing| PDF.js                |
| Hosting       | Vercel                |
| Security      | RLS, XSS, CSP         |

---

Future Enhancements
- Payment automation (PhonePe Collect flow)
- Fast2SMS & push notifications
- Backend migration (Node.js,Express backend + JWT)
- AI-based automation (n8n workflow)
- Mobile app (React Native)
- multi colleges (SaaS Model)

---

## 🧠  Key Takeaway

> Operational chaos is often a sign of missing system design.
  his project demonstrates how identifying workflow inefficiencies and applying system design principles
  can convert manual operations into scalable, automated systems.

---

## 🙏 Acknowledgement

This product was shaped by real users — my classmates.

Every message, call, and request helped define the system.

---

## 📌 Note

This system is currently restricted to authorized users.  

External users cannot log in.

---

## 💬 Final Thought

Your real-life frustration can become your best project idea.

I started with 15 printouts.  
I ended up building a production system.
I didn’t build a print app.
I built a system that removes the need for coordination.

---

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

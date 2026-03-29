# nesprnt-case-study
# 🖨️ Nesprnt — From WhatsApp Chaos to a 90+ Feature Production System
## 🚀 Overview
Nesprnt is a production-ready web application built to automate campus print workflows by replacing unstructured WhatsApp-based coordination with a structured, scalable system.
This project was built in my **4th semester**, solving a real problem I personally experienced over multiple semesters.
> In an era dominated by AI agents and LLMs, this project focuses on solving a real-world **last-mile problem in campus logistics**.
---
## 😤 The Problem
Every semester, students are required to submit printed and bound lab reports.
As a **day scholar**, I became the “print mediator” for my classmates.
- Hostelers avoided expensive campus print shops  
- They sent PDFs via WhatsApp  
- I printed them from a shop near my home  
Initially manageable, the process quickly became chaotic.
---
## 🟡 The Chaos
At peak times, I handled **30–40 print requests simultaneously**.
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

**1st Semester:**  
Small scale — manageable  

**2nd Semester:**  
More users → more PDFs → more confusion  

**3rd Semester:**  
Reduced involvement due to overload  

**4th Semester:**  
Same problem returned — larger than before  
---
## 💡 The Realization

> This is not a printing problem.  
> This is a **system design problem**.
---

## 🚀 The Solution — Nesprnt

A complete workflow automation system:

**Upload → Customize → Pay → Track → Collect**

---

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

## ⚙️ Features (90+)

### 📄 PDF Management
- Upload up to 5 PDFs (max 30MB)
- Auto page detection
- Thumbnail preview
- Duplicate detection
- Corrupted/password-protected PDF blocking
- Per-PDF customization

---

### ⚙️ Print Customization
- Single / Double sided
- First page single, rest double
- Pin binding (free)
- Spiral binding (+₹25)
- Live sheet calculation

---

### 💰 Pricing Engine
- ₹1.50 per B&W sheet
- ₹8 per color sheet
- Per-PDF price breakdown
- Automatic total calculation

---

### 📱 Payment Flow
- UPI display + copy
- “I Have Paid” confirmation
- Order ID generation
- Step-by-step UI flow

---

### 🔍 Order Tracking
- Real-time status updates
- Timeline view
- Student verification

---

### 📦 My Orders
- Live order tracking
- Cancel before verification
- Delete cancelled orders
- Refund via WhatsApp

---

### 🔐 Admin Panel
- Order management dashboard
- Payment verification
- Bulk WhatsApp dispatch
- Status filters
- SMS notifications
- Refund handling
- Analytics dashboard

---

### 🔑 Access Control
- Restricted login (CSE-A & CSE-B only)
- Email validation
- Outsider access blocked
- Persistent login session

---

### 🔒 Security
- Row Level Security (RLS)
- SHA-256 password hashing
- Salt encryption
- XSS protection
- Rate limiting
- Brute force protection
- HTTPS only
- Signed URL expiry

---

## 🧪 Testing

Tested with real users (classmates):

- End-to-end order flow  
- Payment confirmation  
- PDF handling  
- Admin operations  
- Mobile responsiveness  

### ✅ Results

- 90+ features working  
- Real orders processed  
- Real UPI payments tested  
- Smooth mobile performance  
- Zero production bugs  

---

## 📊 Project Stats

- ⚡ 90+ features  
- 🔒 10+ security measures  
- 🗄️ 4 database tables  
- 📁 1 storage bucket  
- 🧪 Real-world testing  
- 🐛 0 bugs  
- 💰 ₹0 hosting cost  
- 📱 100% mobile responsive  

---

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

## 🚀 Roadmap

- Payment automation (PhonePe Collect flow)
- Fast2SMS & push notifications
- Backend migration (Node.js,Express backend + JWT)
- AI-based automation (n8n workflows)
- Mobile app (React Native)
- Multi-college scaling

---

## 🧠 Key Insight

> Operational chaos is often a sign of missing system design.

---

## 🙏 Acknowledgement

This product was shaped by real users — my classmates.

Every message, call, and request helped define the system.

---

## 📌 Note

This system is currently restricted to authorized users (CSE-A & CSE-B).  

External users cannot log in.

---

## 💬 Final Thought

Your real-life frustration can become your best project idea.

I started with 15 printouts.  
I ended up building a production system.

---

## 📄 License

© 2026 Nesprnt student Print Mediator. All Rights Reserved.
Unauthorized reproduction or distribution is strictly prohibited under the Copyright Act, 1957.

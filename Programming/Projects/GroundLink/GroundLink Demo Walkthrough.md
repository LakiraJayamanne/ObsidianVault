---
tags:
  - groundlink
  - demo
  - project
---

# GroundLink Demo Walkthrough

Full end-to-end walkthrough of the Phase 1 build. Use this to walk Lahiru through the app.

---

## Roles

| Role | Purpose |
|---|---|
| `dmc_ops` | Creates and manages bookings, assigns guides/vehicles, rates guides |
| `transport_mgr` | Manages fleet (add vehicles) |
| `guide` | Accepts/declines bookings, shares live location |
| `driver` | Same as guide |
| `supplier` | Adds vehicles to the fleet |
| `admin` | Verifies pending users, full access |

---

## The Core Loop

### 1. Register & Login
- Register at `/` — role selected at signup
- Redirects to dashboard based on role
- Guides land on a **3-step onboarding wizard** (languages, zones, specialisms, day rate)
- After onboarding, guide status = **pending** (not bookable yet)

### 2. Admin Approves the Guide — `/dashboard/admin`
- Admin sees a queue of all pending users
- Expand each user to view uploaded documents inline
- Hit **Approve** → guide flips to `active`, now bookable

### 3. DMC Creates a Booking — `/dashboard/bookings/new`
- Fields: programme name, date, pax count, language, pickup location, market, notes
- Auto-assigned reference e.g. `TOR-001`
- Starts in **draft** status

### 4. DMC Assigns Guide + Vehicle — `/dashboard/bookings/[id]`
- Side panel: available guides filtered by date + language
- Second panel: vehicle assignment
- On assignment → booking moves to **pending**, guide sees it in their diary

### 5. Guide Accepts — `/dashboard` diary
- Guide sees upcoming bookings
- Can **accept or decline**
- On accept → booking flips to **confirmed**

### 6. Active Booking + Live Map
- Status moves to **active** on the day
- Guide hits "Share Live Location" → POSTs GPS to `/api/gps`
- DMC's booking detail polls every 15s, shows guide position on Leaflet map

### 7. Complete + Rate
- DMC marks booking **completed**
- Rating modal: 1–5 stars + notes
- Guide's average rating updates automatically

---

## Booking Status Flow

`draft` → `pending` → `confirmed` → `active` → `completed` (or `cancelled`)

---

## Key Pages

| Page | Who sees it | What it does |
|---|---|---|
| `/dashboard` | All | Guide: diary. DMC/Admin: stats + recent bookings |
| `/dashboard/bookings` | DMC/Admin | Full bookings table with status filter tabs |
| `/dashboard/bookings/new` | DMC | Create a booking |
| `/dashboard/bookings/[id]` | DMC/Admin | Booking detail, assign guide/vehicle, live map, rate |
| `/dashboard/guides` | DMC/Admin | Guide directory with filters |
| `/dashboard/guides/[id]` | DMC/Admin | Guide profile, ratings, zones, specialisms |
| `/dashboard/vehicles` | Transport/Supplier/Admin | Fleet list, add vehicle modal |
| `/dashboard/admin` | Admin | Verification queue |
| `/dashboard/settings` | All | Update name, phone, password |

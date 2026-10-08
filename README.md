# Meridian

> Your complete travel companion — plan, track, and budget every trip in one place.

---

## What is Meridian?

Meridian is a free, web-first travel planning app that brings together everything scattered across your inbox, notes, and spreadsheets into a single beautiful interface. It automatically syncs your travel confirmations from Gmail, lets you build detailed day-by-day itineraries, and tracks your budget and daily expenses — all accessible from any device's browser.

No app install required. No subscription. Just travel better.

---

## Core Features (V1)

### ✈️ Trip Management
- Create and manage multiple trips
- Trip overview with key dates, destination, and status (upcoming / in progress / past)
- Clean dashboard showing all trips at a glance

### 📥 Gmail Sync
- Connect your Gmail account via Google OAuth
- Automatically detects and parses travel confirmation emails:
  - Flight bookings (departure, arrival, PNR, airline)
  - Hotel reservations (check-in, check-out, property name, confirmation number)
  - Car rentals, train tickets, activity bookings
- All parsed into structured, editable cards on your trip
- Re-sync on demand or on a schedule

### 🗓️ Day-by-Day Itinerary Builder
- Visual timeline view for each day of the trip
- Add activities, meals, transport, and free time blocks
- Drag-and-drop reordering within and across days
- Notes and links per activity
- Automatically populates from Gmail-synced bookings

### 💰 Budget & Expense Tracking
- Set a total trip budget
- Log daily expenses with:
  - Amount
  - Category (Food, Transport, Accommodation, Activities, Shopping, Misc)
  - Date, notes, and optional receipt description
- Live budget vs. spent view
- Per-category breakdown
- Daily spending summary

### 🎒 Packing Lists
- Create packing lists per trip
- Reusable list templates (Beach, City Break, Business, Winter, Hiking, etc.)
- Check off items as you pack
- Add custom items
- Mark lists as complete

---

## Planned Features (Later Iterations)

- **Collaboration** — share a trip with travel companions, split expenses, settle up
- **Offline access** — full functionality without data, syncs when reconnected
- **AI itinerary suggestions** — generate a draft itinerary from destination + interests + duration
- **Push notifications** — check-in reminders, flight alerts, daily spending nudges
- **Google Maps integration** — save all trip places to a Google Maps list in one click

---

## Tech Stack

| Layer | Technology |
|-------|------------|
| Framework | Next.js 15 (App Router) |
| Hosting | Vercel (free tier) |
| Database | Supabase (PostgreSQL) |
| Auth | Supabase Auth + Google OAuth |
| Gmail Sync | Gmail API |
| UI Components | shadcn/ui |
| Styling | Tailwind CSS |
| Animations | Framer Motion |
| Client State | Zustand |
| Server State | TanStack Query |

**Running cost at launch: $0**

---

## Design Principles

- **Mobile-first, responsive** — optimized for phone browsers, no native app required
- **Speed over features** — fast load, snappy interactions, nothing sluggish
- **Reduce manual work** — Gmail sync does the heavy lifting; users fill in the gaps
- **Clarity in the budget** — expenses should take 5 seconds to log, not 30
- **Premium feel** — smooth animations, thoughtful spacing, dark and light mode

---

## Data Model (High Level)

```
User
└── Trip
    ├── Bookings (from Gmail or manual)
    │   ├── Flight
    │   ├── Hotel
    │   └── Other
    ├── Itinerary
    │   └── Day
    │       └── Activity
    ├── Budget
    │   └── Expense
    └── PackingList
        └── PackingItem
```

---

## Project Structure (Planned)

```
meridian/
├── app/                    # Next.js App Router
│   ├── (auth)/             # Login, OAuth callback
│   ├── (app)/              # Authenticated app shell
│   │   ├── dashboard/      # All trips overview
│   │   ├── trips/[id]/     # Trip detail
│   │   │   ├── overview/
│   │   │   ├── itinerary/
│   │   │   ├── budget/
│   │   │   └── packing/
│   │   └── settings/
│   └── api/                # API routes
│       ├── gmail/          # Gmail OAuth + sync
│       └── trips/          # Trip CRUD
├── components/             # Shared UI components
├── lib/                    # Utilities, Supabase client, Gmail parser
├── store/                  # Zustand stores
└── supabase/               # Migrations, types
```

---

## Getting Started (Development Setup)

> Prerequisites: Node.js 20+, a Supabase project, Google Cloud project with Gmail API enabled

```bash
# Clone and install
git clone https://github.com/shantanu0323/meridian
cd meridian
npm install

# Environment variables
cp .env.example .env.local
# Fill in: SUPABASE_URL, SUPABASE_ANON_KEY, GOOGLE_CLIENT_ID, GOOGLE_CLIENT_SECRET

# Run locally
npm run dev
```

---

## Competitive Landscape

| App | Email Sync | Itinerary Builder | Budget Tracking | Free | Great UI |
|-----|-----------|-------------------|-----------------|------|----------|
| TripIt | ✅ | Partial | ❌ | Partial | ❌ |
| Wanderlog | ❌ | ✅ | ❌ | ✅ | ✅ |
| TravelSpend | ❌ | ❌ | ✅ | ✅ | Partial |
| **Meridian** | ✅ | ✅ | ✅ | ✅ | ✅ |

---

## Status

🟡 **Pre-development** — scoping and design phase

---

*Meridian — built for travelers who want one place for everything, not five apps and a spreadsheet.*

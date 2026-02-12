# Nourish Empower - Care Management Application

A comprehensive care management application for carers and support staff with admin CRM backend. Features include scheduling, client management, medication tracking, check-in/check-out with GPS, and care notes.

## Features

### For Carers/Support Staff
- 📅 **Schedule Management** - View daily, weekly schedules with client details
- 👤 **Client Information** - Access client records, care plans, and notes
- 📝 **Tasks & Care Notes** - Record personal care, observations, incidents
- 💊 **Medication Management** - Track medication administration and refusals
- 📍 **GPS Check-In/Check-Out** - Time tracking with location verification
- 🔔 **Notifications** - Reminders for visits and tasks
- 🔐 **Facial Recognition** - Biometric authentication (optional)

### For Administrators
- 👥 **User Management** - Create and manage carer accounts
- 📊 **Client Management** - Manage client information and care plans
- 📆 **Schedule/Rota Management** - Assign visits to carers
- 📈 **Reports & Analytics** - View visit logs, care notes, medication records
- ⏱️ **Time & Attendance** - Track carer check-ins/check-outs
- 🔔 **Alerts** - System notifications for important events

## Tech Stack

- **Framework**: Next.js 14 with App Router
- **Language**: TypeScript
- **Database**: Supabase (PostgreSQL)
- **Authentication**: Supabase Auth with optional biometric
- **Styling**: Tailwind CSS
- **State Management**: Zustand
- **Date Handling**: date-fns
- **Icons**: Lucide React
- **Deployment**: Vercel
- **Mobile**: Progressive Web App (PWA)

## Project Structure

```
nourish-empower/
├── app/
│   ├── (auth)/
│   │   ├── login/
│   │   │   └── page.tsx
│   │   └── layout.tsx
│   ├── (dashboard)/
│   │   ├── dashboard/
│   │   │   └── page.tsx
│   │   ├── schedule/
│   │   │   └── page.tsx
│   │   ├── clients/
│   │   │   ├── page.tsx
│   │   │   └── [id]/
│   │   │       └── page.tsx
│   │   ├── tasks/
│   │   │   └── page.tsx
│   │   ├── medication/
│   │   │   └── page.tsx
│   │   ├── checkin/
│   │   │   └── page.tsx
│   │   └── layout.tsx
│   ├── (admin)/
│   │   ├── admin/
│   │   │   ├── dashboard/
│   │   │   ├── users/
│   │   │   ├── clients/
│   │   │   ├── schedules/
│   │   │   └── reports/
│   │   └── layout.tsx
│   ├── api/
│   │   ├── auth/
│   │   ├── clients/
│   │   ├── visits/
│   │   ├── checkin/
│   │   └── medication/
│   ├── layout.tsx
│   └── page.tsx
├── components/
│   ├── auth/
│   │   ├── LoginForm.tsx
│   │   └── BiometricAuth.tsx
│   ├── dashboard/
│   │   ├── DashboardHeader.tsx
│   │   ├── StatsCards.tsx
│   │   └── UpcomingVisits.tsx
│   ├── schedule/
│   │   ├── ScheduleCalendar.tsx
│   │   ├── VisitCard.tsx
│   │   └── ScheduleFilters.tsx
│   ├── clients/
│   │   ├── ClientList.tsx
│   │   ├── ClientCard.tsx
│   │   └── ClientDetails.tsx
│   ├── tasks/
│   │   ├── TaskList.tsx
│   │   ├── CareNotesForm.tsx
│   │   └── IncidentForm.tsx
│   ├── medication/
│   │   ├── MedicationList.tsx
│   │   ├── MedicationLog.tsx
│   │   └── MedicationForm.tsx
│   ├── checkin/
│   │   ├── CheckInForm.tsx
│   │   ├── LocationMap.tsx
│   │   └── TimeTracker.tsx
│   ├── admin/
│   │   ├── UserManagement.tsx
│   │   ├── ClientManagement.tsx
│   │   ├── ScheduleManagement.tsx
│   │   └── Reports.tsx
│   ├── ui/
│   │   ├── Button.tsx
│   │   ├── Card.tsx
│   │   ├── Input.tsx
│   │   ├── Modal.tsx
│   │   └── Navbar.tsx
│   └── layout/
│       ├── Header.tsx
│       ├── Sidebar.tsx
│       └── Footer.tsx
├── lib/
│   ├── supabase/
│   │   ├── client.ts
│   │   ├── server.ts
│   │   └── middleware.ts
│   ├── utils/
│   │   ├── date.ts
│   │   ├── location.ts
│   │   └── validation.ts
│   └── store/
│       ├── authStore.ts
│       ├── scheduleStore.ts
│       └── clientStore.ts
├── types/
│   ├── database.types.ts
│   ├── user.ts
│   ├── client.ts
│   ├── visit.ts
│   ├── medication.ts
│   └── careNote.ts
├── public/
│   ├── manifest.json
│   ├── icons/
│   └── sw.js
├── supabase/
│   └── migrations/
│       ├── 001_init.sql
│       ├── 002_rls_policies.sql
│       └── 003_seed_data.sql
├── .env.local.example
├── .gitignore
├── next.config.js
├── package.json
├── postcss.config.js
├── tailwind.config.ts
├── tsconfig.json
└── README.md
```

## Database Schema

### Tables

1. **profiles**
   - id (uuid, FK to auth.users)
   - email
   - full_name
   - role (enum: 'carer', 'admin')
   - phone
   - avatar_url
   - created_at
   - updated_at

2. **clients**
   - id (uuid)
   - full_name
   - address
   - phone
   - emergency_contact
   - care_plan
   - medical_info
   - notes
   - created_at
   - updated_at

3. **visits**
   - id (uuid)
   - client_id (FK to clients)
   - carer_id (FK to profiles)
   - scheduled_start
   - scheduled_end
   - actual_start
   - actual_end
   - status (enum: 'scheduled', 'in_progress', 'completed', 'cancelled')
   - location_lat
   - location_lng
   - created_at
   - updated_at

4. **care_notes**
   - id (uuid)
   - visit_id (FK to visits)
   - carer_id (FK to profiles)
   - client_id (FK to clients)
   - note_type (enum: 'general', 'personal_care', 'observation', 'incident')
   - content
   - attachments
   - created_at

5. **medications**
   - id (uuid)
   - client_id (FK to clients)
   - name
   - dosage
   - frequency
   - instructions
   - active
   - created_at
   - updated_at

6. **medication_logs**
   - id (uuid)
   - medication_id (FK to medications)
   - visit_id (FK to visits)
   - carer_id (FK to profiles)
   - administered_at
   - status (enum: 'given', 'refused', 'not_available')
   - refusal_reason
   - notes
   - created_at

7. **check_ins**
   - id (uuid)
   - visit_id (FK to visits)
   - carer_id (FK to profiles)
   - check_in_time
   - check_out_time
   - check_in_location
   - check_out_location
   - duration_minutes
   - created_at

## Setup Instructions

### 1. Clone Repository

```bash
git clone https://github.com/JohnOkenyi/nourish-empower.git
cd nourish-empower
```

### 2. Install Dependencies

```bash
npm install
```

### 3. Set Up Supabase

1. Go to [supabase.com](https://supabase.com)
2. Create a new project
3. Get your project URL and anon key
4. Run the SQL migrations in `supabase/migrations/`

### 4. Environment Variables

Create `.env.local` file:

```env
NEXT_PUBLIC_SUPABASE_URL=your_supabase_url
NEXT_PUBLIC_SUPABASE_ANON_KEY=your_supabase_anon_key
```

### 5. Run Development Server

```bash
npm run dev
```

Visit `http://localhost:3000`

### 6. Deploy to Vercel

```bash
# Install Vercel CLI
npm i -g vercel

# Deploy
vercel
```

Or connect your GitHub repo to Vercel dashboard for automatic deployments.

## Converting to Mobile App

### Option 1: Progressive Web App (PWA)

The application is already configured as a PWA. Users can install it from their browser:

- **iOS**: Safari > Share > Add to Home Screen
- **Android**: Chrome > Menu > Add to Home Screen

### Option 2: React Native / Capacitor

For native app stores (Apple App Store / Google Play):

```bash
# Install Capacitor
npm install @capacitor/core @capacitor/cli
npx cap init
npx cap add ios
npx cap add android

# Build and sync
npm run build
npx cap sync
npx cap open ios
npx cap open android
```

## Features Implementation Status

- ✅ Authentication System
- ✅ User Roles (Carer/Admin)
- ✅ Dashboard
- ✅ Schedule Management
- ✅ Client Management
- ✅ Visit Tracking
- ✅ Care Notes
- ✅ Medication Management
- ✅ GPS Check-In/Check-Out
- ✅ Admin CRM
- 🔄 Facial Recognition (In Progress)
- 🔄 Push Notifications (In Progress)
- ✅ PWA Support

## License

Private - All Rights Reserved

## Support

For issues and questions, contact your administrator or create an issue on GitHub.

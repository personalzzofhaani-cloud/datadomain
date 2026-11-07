# DOMAIN FEST – Science Department
### Caliph Life School &bull; Administrator Operations & Registration Portal

A complete, production-ready registration management web application built for the **Science Department of Caliph Life School** to organize, register, and analyze participants for **DOMAIN FEST**.

---

## 🌟 Application Features

### 1. Strictly Administrator-Only (No Public Portal)
- Secure login screen with Domain Fest & Caliph Life School Science Department branding.
- Multi-role administrator authorization: **Super Admin** and **Admin**.
- Super Admins can invite, manage roles, and deactivate administrators. Standard Admins manage registrations, classes, and events.
- Database Row Level Security (RLS) policies prevent unauthorized public access.

### 2. Streamlined Navigation (3 Main Sections Only)
As specified by the department, the interface avoids cluttered sidebars and features exactly three core working sections:
1. **Dashboard**: Live statistics cards, event-wise registration chart, class-wise registration chart, event distribution donut, and recent activity with a "View All" shortcut.
2. **Registration**: Primary administrative workspace to enter participant names, select dynamic classes (including `C2Z`), choose multi-track events, search, filter, edit, and delete registrations.
3. **Reports**: Three comprehensive report tabs (**Event-wise**, **Class-wise**, and **Complete Master List**) with Excel (`.xlsx`) and CSV export capabilities. Names and selected events are never truncated.

### 3. Administrative Settings (Small Gear Icon in Header)
All administrative configuration is centralized under the header gear button:
- **Manage Classes**: Add, edit, activate/deactivate, and reorder classes (includes delete protection for historical records).
- **Manage Events**: Add newly finalized events with descriptions, activate/deactivate, reorder, and view live participant counts.
- **Administrator Access**: Super Admin portal to invite new admins and toggle statuses.
- **Registration Rules**: Master toggle to open or pause new participant entries.
- **Database / Supabase**: Connection status, real-time sync, and 1-click copy of the production PostgreSQL schema.

---

## 🛠️ Technology Stack

- **Frontend**: React 18 + TypeScript
- **Styling**: Tailwind CSS
- **Charts**: Recharts
- **Icons**: Lucide React
- **Spreadsheet Generation**: SheetJS (`xlsx`)
- **Backend / Database**: Supabase PostgreSQL + Supabase Auth
- **Hosting**: Vercel-ready with `vercel.json` rewrites

---

## 🚀 Getting Started

### Local Development
```bash
# 1. Install dependencies
npm install

# 2. Run the Vite development server
npm run dev
```

### Evaluation / Offline Preview
When running without Supabase credentials, the application automatically operates with a **persistent local store**, allowing immediate testing of all features:
- **Super Admin Account**: `admin@caliphlife.edu` / `Admin@12345`
- **Admin Account**: `coordinator@caliphlife.edu` / `Admin@12345`

### Connecting to Supabase Cloud
1. Create a project at [supabase.com](https://supabase.com).
2. Open the **SQL Editor** in Supabase and paste the contents of `supabase/schema.sql` (or copy it from the in-app Settings → Database tab). Run the script.
3. Copy your project **URL** and **Anon Key** from Project Settings → API.
4. Add them to your `.env` file (or paste them directly into the Settings modal):
   ```env
   VITE_SUPABASE_URL=https://your-project.supabase.co
   VITE_SUPABASE_ANON_KEY=your-anon-public-key
   ```
5. Deploy to Vercel with a single click or `vercel deploy`.

---

## 📊 Database Design Summary

- `classes`: Initialized with `8`, `9`, `S1A`, `S1B`, `C1A`, `C1B`, `C1C`, `S2A`, `S2B`, `C2Z`, `C2B`, `C2C`, `MENTOR`, `PARENT`, `OTHER`.
- `events`: Starts empty per specifications; dynamic addition of finalized science events.
- `registrations`: Stores `registration_number` (safe sequential `DF-XXXX`), participant name, class reference, timestamps.
- `registration_events`: Junction table with unique constraint on `(registration_id, event_id)` preventing duplicate event selections.
- `admin_profiles`: User roles (`super_admin` / `admin`), active status.
- `audit_logs`: Detailed activity history.
- `app_settings`: Global registration open/closed toggle.

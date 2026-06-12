# Accountability Tracker
### Ahmed Al Sheebani Real Estate LLC | Ahmed Al Sheebani Technical Services LLC

A web-based monthly employee accountability and task management system. Employees log in to track their weekly tasks, priorities, and progress. The CEO can view all employee sheets and add notes. The Admin manages users and exports reports.

---

## Live App

**URL:** *https://accountability-app-sand.vercel.app/*

---

## Tech Stack

| Layer | Technology |
|---|---|
| Frontend | HTML, CSS, JavaScript (Vanilla) |
| Database | Supabase (PostgreSQL) |
| Hosting | Vercel |
| Version Control | GitHub |

---

## Project Structure

```
accountability-app/
│
├── index.html              ← Main application (entire app in one file)
├── users.js                ← Employee list reference (data is in Supabase)
├── chatgpt-responses.js    ← Funny ChatGPT button responses
├── README.md               ← This file
│
└── images/
    ├── logo_login_1.png    ← Login page logo (200x200px, PNG)
    ├── logo_navbar.png     ← Navbar logo (320x80px, PNG, white version)
    ├── dirham.png          ← UAE Dirham icon for salary button
    │
    ├── avatar/             ← Navbar avatar photos (80x80px per user)
    │   ├── ameera_avatar.png
    │   ├── jahara_avatar.png
    │   └── ... (firstname_avatar.png for each employee)
    │
    ├── card/               ← Dashboard card photos (200x200px per user)
    │   ├── ameera_card.png
    │   ├── jahara_card.png
    │   └── ... (firstname_card.png for each employee)
    │
    └── game/
        └── rafsan_game.png ← Whack-a-Rafsan game character (200x200px)
```

---

## Image Size Reference

| Image | Size | Location | Notes |
|---|---|---|---|
| Login Logo | 200 x 200 px | `images/logo_login_1.png` | PNG, transparent background |
| Navbar Logo | 320 x 80 px | `images/logo_navbar.png` | PNG, transparent, white version |
| User Avatar (Navbar) | 80 x 80 px | `images/avatar/firstname_avatar.png` | PNG/JPG, square crop |
| User Card (Dashboard) | 200 x 200 px | `images/card/firstname_card.png` | PNG/JPG, square crop |
| Dirham Icon | Any | `images/dirham.png` | PNG, black on transparent |
| Game Character | 200 x 200 px | `images/game/rafsan_game.png` | PNG, circular crop works best |

---

## Supabase Database

### Tables

| Table | Purpose |
|---|---|
| `users` | Employee accounts, roles, passwords, photo paths |
| `sheets` | Monthly task data per employee per month |
| `sticky_notes` | Sticky notes per employee (synced across devices) |
| `ceo_notes` | CEO notes written for each employee per week |

### Connection Details
- **Project URL:** `https://sbiquslgcarpsyxmkadq.supabase.co`
- **API Key:** *(Keep this private — stored in index.html)*

---

## User Roles

| Role | Access |
|---|---|
| **Employee** | Own sheet only. Can enter tasks, priorities, comments. Cannot write CEO notes. |
| **Admin** | Own sheet + User management (add, edit, delete, reset password) + Export all reports |
| **CEO** | Own sheet + View all employee sheets + Write CEO notes per employee per week |

---

## How to Add or Remove an Employee

**Add a new employee:**
1. Login as **Jahara** (Admin)
2. Go to **Admin Panel**
3. Fill in the Add New Employee form
4. Click **Add Employee**

**Remove an employee:**
1. Login as **Jahara** (Admin)
2. Go to **Admin Panel**
3. Click **Delete** next to the employee

**Edit an employee's name, username, title or role:**
1. Login as **Jahara** (Admin)
2. Go to **Admin Panel**
3. Click **Edit** next to the employee

---

## How to Add ChatGPT Button Messages

Open `index.html` and find the `CGPT` array near the top of the script section:

```javascript
var CGPT = [
  { user: 'Rafsan', message: "Rafsan, don't use ChatGPT - do it yourself!" },
  { user: 'all',    message: "Can't you people do anything by yourselves?" },
  // Add more here...
];
```

- `user: 'Username'` — shows only when that specific person clicks
- `user: 'all'` — shows for anyone without a personal message (picked randomly)
- Multiple messages per user are picked randomly, never repeating the same one twice in a row

---

## How to Export Reports

**Individual employee export:**
1. Login as the employee
2. Go to **My Sheet**
3. Select the month and year
4. Click **Excel** or **PDF**

**All employees export (Admin only):**
1. Login as **Jahara** (Admin)
2. Go to **Admin Panel** → Export Reports section
3. Select employee (or All Employees)
4. Select month and year
5. Click **Export Excel** or **Export PDF**

---

## Vercel Deployment

The app auto-deploys whenever `index.html` is updated on GitHub.

**To update the app:**
1. Make changes to `index.html`
2. Upload to GitHub (replace existing file)
3. Vercel detects the change and redeploys automatically (~30 seconds)

**To check deployment status:**
- Go to [vercel.com](https://vercel.com) → your project → Deployments tab

---

## Supabase Maintenance

### Run after creating any new tables (required for API access):
```sql
GRANT SELECT, INSERT, UPDATE, DELETE ON public.your_new_table TO anon;
```

### If the app stops loading (RLS issue):
```sql
ALTER TABLE public.users        DISABLE ROW LEVEL SECURITY;
ALTER TABLE public.sheets       DISABLE ROW LEVEL SECURITY;
ALTER TABLE public.sticky_notes DISABLE ROW LEVEL SECURITY;
ALTER TABLE public.ceo_notes    DISABLE ROW LEVEL SECURITY;
```

### To clear all task data (keeps users and settings):
```sql
DELETE FROM public.sheets;
```

### To clear tasks for one employee only:
```sql
DELETE FROM public.sheets WHERE username = 'Username';
```

### To clear tasks for a specific month:
```sql
-- Month is 0-indexed: January=0, February=1 ... December=11
DELETE FROM public.sheets WHERE year = 2026 AND month = 4;
```

---

## Dashboard Features

| Feature | Description |
|---|---|
| Live Clock | Dubai timezone, live ticking |
| Weather | Live Dubai weather via Open-Meteo API |
| Calendar | Current month with today highlighted |
| Task Stats | Total, Completed, In Progress, Pending counts |
| Leaderboard | Top 5 employees by completed tasks (week/month) |
| Whack-a-Rafsan | Mini clicking game with 30 second timer |
| Daily Quote | Random motivational quote, changes every session |
| Sticky Notes | Draggable notes, synced across all devices |
| ChatGPT Button | Funny personalized messages per employee |
| Salary Button | Runaway dirham button → Mafi Fulus popup |

---

## Known Limitations

- Passwords are stored as plain text in Supabase (intentional design choice)
- Supabase free tier may pause after extended inactivity — restore via Supabase dashboard
- PDF export uses browser print dialog — for best results use Chrome

---

## Support & Maintenance

Built and maintained by **Ahmad Cheema**
For technical issues or new feature requests, contact Ahmad directly.

---

*Last updated: June 2026*

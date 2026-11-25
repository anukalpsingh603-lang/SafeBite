# SafeBite — Public Food Safety Portal

SafeBite is a full-stack mini-project that demonstrates how a public-facing food-safety transparency directory could work.

**Important:** SafeBite is an independent prototype, not a government service, inspection agency, or FSSAI partner. Demo records are fictional. A user rating or submitted complaint is not proof that a restaurant is unsafe. Only mark a record `verified` after checking authoritative evidence and recording its source.

## Features

- Searchable restaurant directory
- Restaurant profiles and record-status labels
- Supabase PostgreSQL database
- Public food-safety concern submission
- Admin sign-in and review queue
- Admin-only restaurant creation and status updates
- Row Level Security (RLS) policies

## Requirements

- Node.js 18 or newer
- A GitHub account
- A Supabase account

## 1. Run locally

```bash
npm install
cp .env.example .env
npm run dev
```

Open the local URL printed by Vite.

## 2. Create the database

1. Create a project at https://supabase.com/.
2. Open **SQL Editor** in the Supabase dashboard.
3. Open `supabase/schema.sql` from this repository.
4. Paste the complete SQL file into the editor and run it.
5. In **Project Settings → API**, copy the Project URL and anon/publishable key.

## 3. Connect the website

Copy `.env.example` to `.env` and enter:

```env
VITE_SUPABASE_URL=https://YOUR_PROJECT.supabase.co
VITE_SUPABASE_ANON_KEY=YOUR_SUPABASE_ANON_OR_PUBLISHABLE_KEY
```

Restart the development server after changing `.env`.

The anon/publishable key is intended for browser use when Row Level Security is correctly configured. **Never put a Supabase service-role key in this frontend.**

## 4. Create an administrator

1. In Supabase, open **Authentication → Users**.
2. Create an account for yourself.
3. In SQL Editor, run the administrator grant query at the bottom of `supabase/schema.sql`, replacing `YOUR_ADMIN_EMAIL` with the exact email used for that account.
4. Sign in through SafeBite's **Admin sign in** option.

Public users can submit reports. Only administrators can read/manage reports and change restaurant records. Keep admin credentials private.

## 5. Publish on GitHub

Create a new repository named `SafeBite`. Upload the project files or push them with Git:

```bash
git init
git add .
git commit -m "Initial SafeBite project"
git branch -M main
git remote add origin https://github.com/YOUR-USERNAME/SafeBite.git
git push -u origin main
```

Do not commit `.env`. It is excluded by `.gitignore`.

## 6. Deploy on Vercel

1. Sign in at https://vercel.com/ using GitHub.
2. Import your `SafeBite` repository.
3. Add `VITE_SUPABASE_URL` and `VITE_SUPABASE_ANON_KEY` under project environment variables.
4. Deploy. Vercel will run `npm run build`.

## Data and verification design

- `sample`: fictional example data; not evidence.
- `pending`: record submitted but not yet checked.
- `verified`: checked by an authorised SafeBite administrator against an identified authoritative source.
- `rejected`: evidence was insufficient or did not match.

For a real deployment, store evidence provenance, source URL, verifier identity, verification timestamp, expiry/review date, and an audit trail. Add moderation, rate limits, anti-spam controls, privacy notices, and a clear complaint escalation process before opening public submissions widely.

## Project structure

```text
SafeBite/
├── package.json
├── index.html
├── .env.example
├── src/
│   ├── App.jsx
│   ├── main.jsx
│   ├── supabase.js
│   └── style.css
└── supabase/
    └── schema.sql
```

## License

MIT — see `LICENSE`.

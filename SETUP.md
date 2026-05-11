# Netlify + Supabase setup for Questenda

## 1. Supabase (database + login)

1. Create a free project at [supabase.com](https://supabase.com).
2. Open **SQL Editor** → **New query**, paste the contents of `supabase/schema.sql`, and click **Run**.
3. Open **Authentication** → **Providers** → **Email** → enable **Email** (magic link / OTP).
4. Open **Authentication** → **URL configuration**:
   - **Site URL:** `https://YOUR-SITE.netlify.app` (use your real Netlify URL after deploy).
   - **Redirect URLs:** add `https://YOUR-SITE.netlify.app/**` and `http://localhost:8888/**` if you test locally with Netlify CLI.
5. Open **Project Settings** → **API** and copy **Project URL** and **anon public** key.

## 2. Configure this repo

1. Copy `supabase-config.example.js` to `supabase-config.js` (or edit the existing `supabase-config.js`).
2. Set `QUESTENDA_SUPABASE_URL` and `QUESTENDA_SUPABASE_ANON_KEY` to the values from step 5.

## 3. Netlify (hosting)

**Option A — drag and drop**

1. Zip the `agenda` folder (include `fungenda.html`, `manifest.webmanifest`, `sw.js`, `icon.svg`, `supabase-config.js`, `netlify.toml`).
2. In Netlify go to **Sites** → **Add new site** → **Deploy manually** and upload the zip.

**Option B — Git**

1. Push this folder to GitHub/GitLab.
2. In Netlify: **Add new site** → **Import an existing project**, pick the repo, leave defaults; `netlify.toml` sets the publish directory to `.`.

After deploy, update Supabase **Site URL** and **Redirect URLs** to match your real `https://....netlify.app` address, then save.

## 4. Use the app on your phone (install like an app)

1. Open your Netlify URL in **Safari** (iOS) or **Chrome** (Android).
2. Sign in with the **same email** on both phone and PC (use **Email magic link** each time; check your inbox).
3. Use **Add to Home screen** / **Install app** so it opens from an icon like a normal app.

## Notes

- The **anon** key is meant to be public in the browser; access is limited by **Row Level Security** in `schema.sql`.
- Data is stored per logged-in user in table `questenda_save`.
- **Export backup** still works as an extra safety net.

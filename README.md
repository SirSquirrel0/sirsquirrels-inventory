# SirSquirrel's Inventory — Weapons & Ship Components

Static website for Cloudflare Pages, backed by Supabase. Public visitors can view listed stock; the authorized Supabase administrator can manage inventory.

## Before publishing

1. In `index.html`, replace:
   - `PASTE_YOUR_SUPABASE_PROJECT_URL_HERE`
   - `PASTE_YOUR_SUPABASE_PUBLISHABLE_KEY_HERE`
2. Use only the Project URL and publishable/anon key. **Never place a `service_role` or secret key in browser code.**
3. Your Supabase `public.inventory` table should have the columns created in the SQL setup, and Row Level Security (RLS) enabled.
4. Confirm the admin policies use your actual Supabase Auth user UUID, and the public policy only permits reading rows where `is_listed = true`.
5. In Supabase Authentication settings, configure the site's deployed URL as an allowed redirect URL if needed. This page currently uses email/password sign-in and does not implement password recovery.

## Upload to GitHub

Upload `index.html` and `README.md` to the root of the `sirsquirrels-inventory` repository. Cloudflare Pages should use:
- Framework preset: None
- Build command: leave blank
- Build output directory: `/` (or `.` if the dashboard requires a relative directory)

## Inventory behavior

- The public catalog reads listed rows from Supabase.
- The manager can add, edit, hide, and delete rows when signed in with the specific administrator account allowed by the database policies.
- Public users cannot change inventory; database RLS is the security boundary.
- No orders or hold requests are accepted on this website; purchases are handled through UEX.
- Prices and quantities are read from the database. No sample stock is inserted by this site.

## Important

The browser publishable key is expected to be public. Security must come from correctly configured Supabase RLS policies. Never disable RLS and never expose a secret/service-role key.

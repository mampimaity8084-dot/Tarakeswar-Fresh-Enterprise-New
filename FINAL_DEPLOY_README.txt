Tarakeswar Fresh - Final Supabase Connected Build

This build is already configured with:
- Supabase project base URL
- Supabase Publishable key
- public.fish live read connection
- existing RLS SELECT policy
- auto offer slider
- Admin PIN page

Upload this ZIP as a new deploy to the SAME Netlify project.

Important:
The supplied API URL ended in /rest/v1/. The Supabase JavaScript client uses
the project base URL, so this build correctly uses:
YOUR_SUPABASE_PROJECT_URL

Never add a Supabase Secret/service_role key to browser files.

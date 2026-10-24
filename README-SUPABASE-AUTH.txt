BDFLEET MC — Supabase Username/Password Login
==============================================

WHAT THIS UPDATE DOES
- Shows Register/Login before the website can be used.
- Users enter username + password only; there is no email input.
- Username rules: 3–24 letters/numbers/underscore. Password: at least 8 characters.
- Keeps the Supabase session on the same browser and forces a new login after 30 days.
- Adds a Log Out button.

IMPORTANT LIMITS
- GitHub Pages is static hosting, so Supabase provides the authentication backend.
- Supabase Auth natively uses email/password. This frontend maps each username to a synthetic internal address: username@users.bdfleetmc.com. Users never enter or need access to an email inbox. Disable email confirmation as below.
- No email means no email-based password reset. If a user forgets their password, you need an administrator-assisted recovery plan.
- The 30-day expiry is enforced by this website's browser code; Supabase refresh-token policies still apply. This is not a custom hard server-side 30-day token policy.
- This login gate protects the website UI only. Public website files remain downloadable from GitHub Pages, and it does not protect private downloads or APIs. Do not put secret files or private data in this repository.
- Never publish a Supabase service_role/secret key. Only Project URL and anon/public key belong in this frontend.

SETUP
1. Create a free project at https://supabase.com/ and open Project Settings → API (or Connect).
2. Copy the Project URL and anon/public key.
3. In index.html, replace:
   PASTE_YOUR_SUPABASE_PROJECT_URL_HERE
   PASTE_YOUR_SUPABASE_ANON_PUBLIC_KEY_HERE
   with those values. Do not use the service_role key.
4. In Supabase Dashboard → Authentication → Sign In / Providers → Email, turn OFF email confirmation (wording may vary). The site doesn't ask users for an email, so confirmation must be disabled for immediate registration.
5. Save/commit index.html to your GitHub Pages repository. Keep assets/hero.svg and assets/ folder intact.
6. Open the live site in a private/incognito tab and test Register, Log Out, then Login.

HOW LOGIN WORKS
A username is normalized to lowercase and mapped internally to username@users.bdfleetmc.com for Supabase Auth. This address is only an internal identifier; users do not enter an email. Usernames are case-insensitive because of this normalization.

If Supabase rejects the synthetic address or your project requires confirmation, do not enable insecure workarounds or put a service_role key in the browser. Stop and use a server-side Edge Function for username-based authentication instead.

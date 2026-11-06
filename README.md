# Family Messenger

Private Android family messenger for up to five members.

## Backend provisioned
Supabase project: https://supabase.com/dashboard/project/tgfhfgvpyituwevjqity (Paris, eu-west-3).

Database foundation currently includes:
- `family_profiles`: profile, admin/member role and pending/approved/rejected membership status.
- A database trigger that gives the first registered account admin/approved status and caps family registration at five accounts.
- `family_messages`: private direct-message records with text/media metadata, reply/forward references, delivery/read timestamps and per-participant deletion flags.
- `family_devices`: FCM token registration records.
- `family_calls`: audio/video call history and call status.
- Private `family-avatars` and `family-media` storage buckets.
- Row-level security on all exposed application tables and private storage policies.

The Supabase security advisor currently reports no security lints. Performance advisor may report unused indexes while the new tables have no traffic; this is expected until the app uses them.

## Google sign-in owner setup
Google OAuth cannot be activated until the owner creates credentials in Google Cloud:
1. Create OAuth credentials for Android package `com.family.messenger` using the final signing SHA-1.
2. Configure the Google provider in Supabase Authentication → Providers → Google (Web client ID and secret).
3. Add `family://auth-callback` to Supabase Authentication → URL Configuration → Redirect URLs.
4. Enable the provider.

Dashboard: https://supabase.com/dashboard/project/tgfhfgvpyituwevjqity

Use only the Supabase publishable key in the Android client. Never put a service-role key in the APK.

## Android implementation status
The repository currently contains the initial root Gradle configuration and project notes. The Android application module, screens, OAuth callback implementation, CI workflow, messaging UI, calls, push delivery, profile-photo flow, and production signing are not yet completed or verified. Do not treat this repository as a buildable APK yet.

## Security notes
- Five-member limit is enforced on the server, not by client-side checks.
- New accounts remain pending until the family administrator approves them.
- Profile and media data use row-level/storage policies.
- User-editable metadata is not used as an authorization source.

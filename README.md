# Family Messenger

Private Android messenger for a family of up to five members.

## Current foundation
- Kotlin + Jetpack Compose Android application.
- Supabase project: `tgfhfgvpyituwevjqity` (Paris region).
- Google OAuth sign-in through Supabase Auth.
- First registered family account becomes the initial administrator; later accounts remain pending until approved.
- Family profile records and a private avatar bucket are provisioned by the initial database migration.

## Google sign-in setup required
Google OAuth cannot be activated without credentials from a Google Cloud project:
1. Create an OAuth client for Android using the app package `com.family.messenger` and the release/debug signing SHA-1 fingerprints.
2. Add the client ID to Supabase Dashboard → Authentication → Sign In / Providers → Google.
3. Enable Google and save the provider configuration.
4. Add `family://auth-callback` to Supabase Authentication → URL Configuration → Redirect URLs.

Dashboard: https://supabase.com/dashboard/project/tgfhfgvpyituwevjqity

The Android app uses only the Supabase publishable key. Never put a service-role key in the APK.

## Build
Open in Android Studio and run the app, or use the GitHub Actions workflow. The CI workflow installs Gradle and Android SDK automatically.

## Security
- Maximum five family accounts is enforced by a database trigger, not by client-side checks.
- New members remain pending until approved by the initial administrator.
- Profile and avatar access are protected by row-level/storage policies.
- Do not treat editable user metadata as an authorization source.

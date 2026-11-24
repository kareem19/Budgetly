# Private Budget App: Setup

Files: `index.html` (the whole app). Nothing else is needed.

## Part 1: Put the app on GitHub Pages (about 5 min)
1. Go to github.com, sign in, and click **New repository**. Name it `budget-app`. Set it to **Public** (GitHub Pages on the free plan needs this; your data is still encrypted and never stored in the repo).
2. Click **uploading an existing file**, drag in `index.html`, and commit.
3. Go to **Settings > Pages**. Under **Source**, choose **Deploy from a branch**, branch **main**, folder **/ (root)**, and save.
4. After about a minute, your app is at `https://YOUR-USERNAME.github.io/budget-app/`. Note this address.

## Part 2: Create the Google sign-in (about 10 min, needed for sync)
1. Go to console.cloud.google.com and create a project called `Budget`.
2. Go to **APIs & Services > Library**, search for **Google Drive API**, and click **Enable**.
3. Go to **APIs & Services > OAuth consent screen**. Choose **External**, fill in the app name `Budget` and your email, and save. Under **Test users**, add your own Gmail address. Leave the app in *Testing* mode; that's fine for personal use.
4. Go to **APIs & Services > Credentials > Create credentials > OAuth client ID**.
   - Application type: **Web application**
   - **Authorized JavaScript origins**: `https://YOUR-USERNAME.github.io` (no trailing slash, no path)
   - Click **Create** and copy the **Client ID** (it ends in `.apps.googleusercontent.com`).
5. Open `index.html` in GitHub (click the file, then the pencil icon). Replace `PASTE_YOUR_CLIENT_ID.apps.googleusercontent.com` with your Client ID, then commit.
6. Wait a minute for Pages to rebuild, then reload the app.

## Part 3: Use it on each device
1. **iPad:** open the address in Safari, tap **Share > Add to Home Screen**.
2. **Android:** open the address in Chrome, tap **⋮ > Add to Home screen** (or **Install app**).
3. **First time:** tap **Create new budget**, choose a passphrase of at least 8 characters, and write it down somewhere safe.
4. **Second device:** open the app, tap **Restore from Google Drive**, enter the same passphrase, and sign in with the same Google account.
5. Use **Sync** → **Sync now** on each device after editing.

## How privacy works
- Your budget is encrypted in the browser (AES-256-GCM, key derived from your passphrase with PBKDF2). Only the scrambled version is saved locally or sent to Google Drive.
- Google Drive stores it in the app's private **appDataFolder**, which other apps and you can't browse in Drive.
- GitHub hosts only the app's code. Your data never touches GitHub.
- No analytics, no ads, no external scripts other than Google's sign-in.
- **If you forget the passphrase, your data cannot be recovered.** Keep an encrypted backup (Sync page > Export encrypted backup) in a second place.

## Sync rules
- Sync is "last change wins" for the whole budget. Before editing on a second device, press **Sync now** on the device you used last.
- Syncing when the passphrase is entered again is required after the app is closed (the key is kept only in memory).

## Known limits
- Google's test-mode sign-in can ask for permission again every few weeks. That's normal.
- The app has not been tested in a live browser or against Google from my side. Check the Months, Summary and Settings pages with sample numbers before entering real data.
- Circle payouts show only after you enter "My turn".

## Troubleshooting
- **Sign-in error or popup blocked:** allow popups for the site, then press Sync again.
- **"Add your Google client ID":** Part 2, step 5 wasn't saved.
- **"Google Drive error 403":** the Drive API isn't enabled, or your email isn't a test user.
- **Wrong passphrase:** nothing is lost. Try again carefully. There's no reset.

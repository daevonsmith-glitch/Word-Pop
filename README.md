# Word Pop Kids 🫧

Pop the letter bubbles in order to spell the word. Made for kids and anyone who stims: no timer, no penalty for wrong taps, color-changing bubbles, and every letter and finished word is spoken out loud.

- `www/` – the game itself (this is what goes on Cloudflare)
- `.github/workflows/android-apk.yml` – builds the Android APK on GitHub automatically
- `assets/` – app icon and splash used for the Android app

- `STORE-GUIDE.md` – step by step for Google Play and the App Store (iPhone and iPad)
- `.github/workflows/ios-testflight.yml` – builds the iPhone and iPad app on GitHub

---

## 1. Put it on GitHub

1. Go to github.com → **+** → **New repository**. Name it `word-pop`. Make it **Public** (so the APK download link works for anyone). Click **Create repository**.
2. Click **uploading an existing file**, unzip this package, and drag in **everything inside the `word-pop` folder** (including the hidden `.github` folder). Commit to `main`.
   - On a phone, uploading the `.github` folder can be hard. If it doesn't come through, in the repo tap **Add file → Create new file**, name it `.github/workflows/android-apk.yml`, and paste in that file's contents.

## 2. Get the Android APK

1. In the repo, open the **Actions** tab. "Build Android APK" starts by itself (about 5–8 minutes). If Actions asks you to enable workflows, tap enable.
2. When it shows a green check, go to the repo's **Releases** (right side of the main page) → **Word Pop Kids (latest build)** → tap **WordPopKids.apk**.
3. Open the downloaded file on the Android phone. Android will ask to allow installs from your browser/files app — allow it, then **Install**.

Every time you change a file on `main`, a fresh APK is built and replaces the old one on the same Releases page.

> This is a debug-signed APK, which is right for sharing directly. For the Google Play Store you'd need a signed release build.

## 3. Put it on Cloudflare (iPhone + any browser)

1. Sign in at dash.cloudflare.com → **Workers & Pages** → **Create** → **Pages** → **Connect to Git**.
2. Pick the `word-pop` GitHub repo.
3. Build settings:
   - Framework preset: **None**
   - Build command: *(leave empty)*
   - Build output directory: **`www`**
4. **Save and Deploy.** You get a link like `https://word-pop.pages.dev` — share that.

Cloudflare redeploys automatically whenever the GitHub repo changes, so one edit updates both the website and the APK.

### Install on iPhone
Open the Cloudflare link in **Safari** → **Share** → **Add to Home Screen**. It opens full-screen like an app and works offline after the first visit.

Tip: if letters don't speak on iPhone, check that the silent switch is off.

---

## Progress report and phonics
- **☰ → 📊 Progress report** shows Week 1, Week 2, and so on: words spelled, right taps, time per word, words spelled with hints off, tricky letters, a letter-by-letter grid and common mix-ups. **Copy report** makes a text version for a teacher.
- Progress is saved on that one phone only. Deleting the app or clearing browser data erases it.
- **Phonics (say letter sounds)** says the sound each letter makes in the word instead of its name. Sounds are written in the `SND` list in `www/index.html`; edit a value there to fix a sound.

## Updating the game
Edit `www/index.html`. Also bump `VERSION` in `www/sw.js` (e.g. `word-pop-v2`) so installed phones pick up the change.

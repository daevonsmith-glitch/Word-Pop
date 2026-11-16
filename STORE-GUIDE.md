# Word Pop Kids – publishing on Google Play and the App Store

Step by step for both stores, publishing under your own name (personal accounts), including the builds. Word Pop Kids runs on Android phones and tablets, iPhone and iPad.

**Publishing as a person:** no D-U-N-S number is needed, but your legal name is shown publicly as the seller on both stores, and Google makes each new game run a 14-day closed test with at least 12 testers.

**Already done:** the game, the name logo, the Android build (APK and Google Play file), the iPhone and iPad build, the Google signing key, the privacy policy page, store text, and screenshots for phone, tablet, iPhone and iPad.

---

## Part 0. Get the files onto GitHub (do once)

### 0A. Upload the game
1. Go to **github.com/daevonsmith-glitch/Word-Pop**.
2. **Add file → Upload files**, add the new **word-pop.zip**, and tap **Commit changes**. The build unpacks it by itself.

### 0B. Replace the Android build file
1. Open **github.com/daevonsmith-glitch/Word-Pop/edit/main/.github/workflows/android-apk.yml** in Safari or Chrome.
2. Select all the text and delete it.
3. Paste the whole "Android build file" from the end of this guide.
4. **Commit changes**, then **Commit changes** again.

### 0C. Add the iPhone and iPad build file
1. In the repository: **Add file → Create new file**.
2. Name it exactly `.github/workflows/ios-testflight.yml`.
3. Paste the whole "iPhone and iPad build file" from the end of this guide.
4. **Commit changes**, then **Commit changes** again.

### 0D. Fill in the privacy page
1. Open `www/privacy.html` in the repository and tap the pencil.
2. Replace `[YOUR NAME OR LLC NAME]` with your name and `[YOUR CONTACT EMAIL]` with an email parents can write to.
3. **Commit changes**.

### 0E. Put it on Cloudflare
Follow `README.md` section 3 if you haven't yet. Your privacy link will be `https://YOUR-CLOUDFLARE-LINK/privacy.html`. Both stores need it.

### 0F. The app ID
The app ID is `com.wordpop.game` (in `capacitor.config.json`). Both stores use it as the game's permanent ID, and it can never change after the first upload. Keep it, or change it now (for example `com.yourname.wordpop`).

---

## Part 1. Google Play

### 1A. Open the account (once)
1. Go to **play.google.com/console** and sign in with the Google account that should own the games. You must be 18 or older.
2. Choose **Personal** as the account type.
3. Enter a developer name (what players see), your legal name, address, email and phone. Verify the email and phone with the codes Google sends.
4. Pay the **$25** fee (once, no renewal).
5. Upload a government photo ID when asked.
6. If asked, confirm you have a real Android phone by signing in to the **Play Console** app on it.

### 1B. Build the Google Play file
1. Open **word-pop-play-signing-key.txt** (private, never in GitHub).
2. In the repository: **Settings → Secrets and variables → Actions → New repository secret**.
3. Name `KEYSTORE_PASSWORD`, value: the password from the file. **Add secret**.
4. **New repository secret** again. Name `KEYSTORE_BASE64`, value: the long single line from the file. **Add secret**.
5. **Actions → Build Android APK → Run workflow → Run workflow**.
6. After about 5 to 8 minutes, open **Releases → Word Pop Kids (latest build)**. You get:
   - `WordPopKids.apk` – install it on your own Android phone to test.
   - `WordPopKids.aab` – the file you upload to Google Play.

Each run raises the version number automatically, which Google requires for every upload.

### 1C. Create the app and listing
1. Play Console → **Create app**: name `Word Pop Kids`, English (United States), **Game**, **Free**. Accept the declarations.
2. **Store listing**: paste the text from "Store text" below.
3. Graphics (from **word-pop-kids-store-images.zip**):
   - App icon: `icon-512.png`
   - Feature graphic: `feature-graphic-1024x500.png`
   - Phone screenshots: the five `play-phone-...png`
   - 7-inch and 10-inch tablet screenshots: the five `play-tablet10-...png` (use them for both)
4. **App content** forms:

| Form | Answer |
|---|---|
| Privacy policy | `https://YOUR-CLOUDFLARE-LINK/privacy.html` |
| App access | All functionality available without special access |
| Ads | No |
| Content rating | Fill in honestly: no violence, no bad language, no sharing between users, no purchases. It should come out as Everyone. |
| Target audience | Ages 5 and under, and 6–8 (add 9–12 if you like). This puts the game under Google's Families policy, which Word Pop Kids already meets: no ads, no data collected, no accounts. |
| Data safety | Collects or shares user data: **No**. Data is encrypted in transit: not applicable. |
| Government, financial, health, news | No |

5. **Category:** Games → Word (or Educational). Tags: Educational, Word, Kids.

### 1D. The 14-day closed test
1. **Find 12 testers.** Each needs a Gmail account and an Android phone. They're adults testing a kids' game, which is fine. The same 12 can test all four games; the rule counts per game.
2. **Testing → Closed testing → Create track** (or use "Closed testing – Alpha").
3. **Testers:** make an email list with the 12+ Gmail addresses.
4. **Create new release**, upload `WordPopKids.aab`, accept **Play App Signing**, and roll it out.
5. Copy the **opt-in link** from the Testers tab and send it to everyone. Each opens it, taps **Become a tester**, and installs the game from Google Play.
6. All 12 must **stay opted in for 14 days in a row**. Ask them to play a few times. Recruit a few extra in case someone drops out.
7. On day 14 or later: **Dashboard → Apply for production** and answer the questions about the test.
8. Google reviews the application, usually within about a week.

### 1E. Go live
1. **Production → Create new release.** Pick the same `.aab` from the library, add release notes ("First release"), pick countries.
2. **Send for review.** A first release for a kids' game can take several days.

---

## Part 2. Apple App Store (iPhone and iPad)

### 2A. Open the account (once)
1. Your Apple Account needs **two-factor authentication** and your **legal name exactly as on your ID**.
2. Install the **Apple Developer** app on your iPhone or iPad.
3. In the app: **Account → Enroll Now → Individual**.
4. Enter your legal name, address and phone, then scan your driver's license or other government ID.
5. Accept the agreement and pay **$99 per year**.
6. Wait for the approval email. Your legal name becomes the seller name on the App Store.
7. Sign in at **appstoreconnect.apple.com** and accept the agreements on the home page.

### 2B. Register the game with Apple
1. **developer.apple.com → Account → Certificates, IDs & Profiles → Identifiers → +**.
2. **App IDs → App**. Description `Word Pop Kids`. **Explicit**, bundle ID `com.wordpop.game` (or the one you chose in 0F). No extra capabilities. **Register**.
3. **App Store Connect → Apps → + → New App**:
   - Platform: iOS
   - Name: `Word Pop Kids`
   - Primary language: English (U.S.)
   - Bundle ID: the one you just registered
   - SKU: `wordpopkids`
   - User access: Full access

### 2C. Connect GitHub to Apple (once, shared by all four games)
1. **Team ID:** developer.apple.com → **Account → Membership details**. Copy the 10-character Team ID.
2. App Store Connect → **Users and Access → Integrations → App Store Connect API**. If you see **Request Access**, tap it and accept.
3. Under **Team Keys**, tap **+**, name it `GitHub`, access **Admin**, **Generate**.
4. Copy the **Issuer ID** (above the list) and the **Key ID** (in the key's row).
5. **Download API Key** (`AuthKey_XXXXXXXXXX.p8`). Apple allows this **only once**, so keep it safe and private.
6. Open the `.p8` file and copy all of it, including the `BEGIN` and `END` lines.
7. GitHub repository → **Settings → Secrets and variables → Actions → New repository secret**, four times:

| Secret name | Value |
|---|---|
| `APPLE_TEAM_ID` | the Team ID |
| `ASC_ISSUER_ID` | the Issuer ID |
| `ASC_KEY_ID` | the Key ID |
| `ASC_KEY_P8` | the whole `.p8` file |

If you already did this for another game, add the same four secrets to this repository too.

### 2D. Build and test on iPhone and iPad
1. GitHub → **Actions → Build iPhone and iPad app (TestFlight) → Run workflow**. About 10 to 20 minutes.
2. A green check means it was sent to Apple. Apple processes it for another 15 to 30 minutes.
3. App Store Connect → Word Pop Kids → **TestFlight**. Under **Internal Testing**, create a group, add yourself, and select the build.
4. Install **TestFlight** on your iPhone and iPad, open the invite, and install Word Pop Kids. Check every level, phonics mode and the progress report, with the silent switch off so you hear the letters.

### 2E. Store listing
App Store Connect → Word Pop Kids → **1.0 Prepare for Submission**:
1. **iPhone screenshots** (6.9" display): the five `iphone-6.9-...png` files.
2. **iPad screenshots** (13" display): the five `ipad-13-...png` files. These are required because the game runs on iPad.
3. **Text:** paste the App Store text from "Store text" below.
4. **Support URL:** your Cloudflare link. **Privacy Policy URL:** the privacy page link.
5. **Build:** tap **+** and choose the TestFlight build.
6. **App Review Information:** your name, phone, email. No sign-in needed.
7. **Age Rating:** answer "None" to everything. It comes out **4+**.
8. **App Privacy → Get Started →** "Do you or your third-party partners collect data from this app?" **No → Publish**.
9. **Pricing and Availability:** Free, choose countries.
10. **App Information → Category:** Games → Word, secondary Education.
11. **Kids Category (optional):** under App Information you can choose **Made for Kids → Ages 5 and under** or **6–8**. Word Pop Kids already meets Apple's kids rules (no ads, no tracking, no links out, no purchases). You can't easily undo this choice later, so decide before submitting.

### 2F. Submit
1. **Add for Review → Submit to App Review**.
2. Apple usually replies in a day or two. If they reject it, send me the message and I'll fix the issue.

---

## Store text

### Google Play
**App name:** `Word Pop Kids`

**Short description** (80 max):

    Pop letter bubbles to spell words. Phonics, 1,300 words, weekly progress report.

### App Store
**Name:** `Word Pop Kids`
**Subtitle** (30 max): `Pop letters, spell words`
**Keywords** (100 max):

    spelling,phonics,abc,alphabet,kids,reading,letters,words,toddler,preschool,kindergarten,autism,learn

**Promotional text:** `1,300 words, phonics mode and a week-by-week progress report for parents.`

### Full description (both stores)

    Word Pop Kids turns spelling into bubble popping. A picture and the word's empty letter boxes appear at the top, colorful bubbles float up, and your child pops the letters in order to spell the word.

    MADE FOR CALM LEARNING
    • No timer and no penalty for wrong taps, just a gentle wobble
    • Color-changing bubbles that are satisfying to pop
    • Calm mode slows everything down
    • Designed with kids who stim in mind

    HEAR EVERY LETTER
    • Each letter is spoken as it's popped, and the whole word is read at the end
    • Phonics mode says the letter sounds instead of their names ("sh" in ship, silent e in cake)
    • Tap the picture any time to hear the word again

    1,300 WORDS, FOUR LEVELS
    • Easy – 3 letters (cat, sun, bus)
    • Medium – 4 letters (frog, cake, ship)
    • Big – 5 letters (apple, train, sleep)
    • Huge – 6+ letters (rabbit, castle, turtle)
    Every word in a level comes up once before any repeat.

    PROGRESS REPORT FOR PARENTS AND TEACHERS
    • Week 1, Week 2 and on: words spelled, accuracy, speed and words spelled without hints
    • A letter chart showing which letters your child knows and which are still tricky
    • The most common mix-ups, like b and d
    • Copy the report to send to a teacher or therapist

    SAFE AND PRIVATE
    No ads, no purchases, no accounts and no data collected. Progress stays on your device. Works offline on phones and tablets.

---

## Files

| File | For |
|---|---|
| `word-pop.zip` | The game, both build files, this guide |
| `word-pop-kids-store-images.zip` | Icon, feature graphic, and screenshots for phone, Android tablet, iPhone and iPad |
| `word-pop-play-signing-key.txt`, `upload-keystore.jks` | Google signing key. **Private: never in GitHub.** Keep a backup. |
| `AuthKey_XXXXXXXXXX.p8` | Apple key you download in 2C. **Private: never in GitHub.** |

## If a build fails
**Actions** → the failed run → the job → the step with the red ❌. Send me the step's name and the red lines near the bottom. The iPhone build's signing step is the one most likely to need a fix on its first run.

## Costs
| | Google Play | App Store |
|---|---|---|
| Account | $25 once | $99 per year |
| Per game | Free | Free |
| GitHub builds | Free for public repositories | Free for public repositories |

---

## Android build file
Path: `.github/workflows/android-apk.yml`

```yaml
name: Build Android APK

# Runs every time the game changes on main, or when you press "Run workflow".
# Always makes WordPopKids.apk (to install on a phone directly).
# Also makes WordPopKids.aab (for Google Play) once the two KEYSTORE secrets are added.
on:
  push:
    branches: [main]
  workflow_dispatch:

permissions:
  contents: write

jobs:
  build:
    runs-on: ubuntu-24.04
    env:
      KEYSTORE_BASE64: ${{ secrets.KEYSTORE_BASE64 }}
      KEYSTORE_PASSWORD: ${{ secrets.KEYSTORE_PASSWORD }}
    steps:
      - uses: actions/checkout@v4

      - name: Unpack word-pop.zip
        run: |
          if [ -f word-pop.zip ]; then
            unzip -q -o word-pop.zip -d /tmp/wp
            rm -rf /tmp/wp/word-pop/.github
            cp -r /tmp/wp/word-pop/. .
            git rm -q word-pop.zip
            git add -A
            git config user.name "github-actions[bot]"
            git config user.email "41898282+github-actions[bot]@users.noreply.github.com"
            git commit -q -m "Unpack game files from word-pop.zip"
            git push
          fi

      - uses: actions/setup-node@v4
        with:
          node-version: 22

      - uses: actions/setup-java@v4
        with:
          distribution: temurin
          java-version: 21

      - name: Install Capacitor
        run: npm install --no-audit --no-fund --legacy-peer-deps

      - name: Create Android project
        run: npx cap add android

      - name: Copy the game into the app
        run: npx cap sync android

      - name: Allow access to the phone's speech engine
        run: |
          M=android/app/src/main/AndroidManifest.xml
          grep -q TTS_SERVICE "$M" || sed -i 's#</manifest>#    <queries>\n        <intent>\n            <action android:name="android.intent.action.TTS_SERVICE" />\n        </intent>\n    </queries>\n</manifest>#' "$M"

      - name: Add the Word Pop Kids app icon
        run: |
          R=android/app/src/main/res
          rm -f $R/mipmap-*/ic_launcher*.png $R/mipmap-*/ic_launcher*.webp
          cp -r android-res/. $R/

      - name: Set version number
        run: |
          G=android/app/build.gradle
          sed -i -E "s/versionCode [0-9]+/versionCode ${{ github.run_number }}/" $G
          sed -i -E "s/versionName \"[^\"]*\"/versionName \"1.2.${{ github.run_number }}\"/" $G
          grep -E "versionCode|versionName|targetSdk" $G android/variables.gradle || true

      - name: Build APK
        working-directory: android
        run: |
          chmod +x gradlew
          ./gradlew assembleDebug --no-daemon --stacktrace
          cp app/build/outputs/apk/debug/app-debug.apk ../WordPopKids.apk

      - name: Build Google Play file (.aab)
        if: env.KEYSTORE_BASE64 != ''
        working-directory: android
        run: |
          ./gradlew bundleRelease --no-daemon --stacktrace
          echo "$KEYSTORE_BASE64" | base64 -d > /tmp/upload.jks
          jarsigner -keystore /tmp/upload.jks -storepass "$KEYSTORE_PASSWORD" -keypass "$KEYSTORE_PASSWORD" \
            -signedjar ../WordPopKids.aab app/build/outputs/bundle/release/app-release.aab upload
          rm -f /tmp/upload.jks

      - name: Keep a copy on the run page
        uses: actions/upload-artifact@v4
        with:
          name: WordPopKids-android
          path: |
            WordPopKids.apk
            WordPopKids.aab
          if-no-files-found: ignore

      - name: Publish to Releases
        uses: softprops/action-gh-release@v2
        with:
          tag_name: latest
          name: Word Pop Kids (latest build)
          body: WordPopKids.apk installs straight on an Android phone. WordPopKids.aab is the file for Google Play.
          files: |
            WordPopKids.apk
            WordPopKids.aab
          make_latest: true
```

## iPhone and iPad build file
Path: `.github/workflows/ios-testflight.yml`

```yaml
name: Build iPhone and iPad app (TestFlight)

# Runs only when you press "Run workflow" (Mac machines take longer).
# Builds the iPhone and iPad app on a GitHub Mac, signs it, and uploads it to App Store Connect.
# It then shows up in TestFlight about 15-30 minutes later.
#
# Needs these repository secrets (Settings > Secrets and variables > Actions):
#   APPLE_TEAM_ID   - 10-character Team ID from developer.apple.com > Account > Membership details
#   ASC_KEY_ID      - Key ID of the App Store Connect API key
#   ASC_ISSUER_ID   - Issuer ID shown above the list of API keys
#   ASC_KEY_P8      - the whole text of the AuthKey_XXXX.p8 file you downloaded
on:
  workflow_dispatch:

jobs:
  ios:
    runs-on: macos-latest
    steps:
      - uses: actions/checkout@v4

      - uses: maxim-lobanov/setup-xcode@v1
        with:
          xcode-version: latest-stable

      - uses: actions/setup-node@v4
        with:
          node-version: 22

      - name: Install Capacitor
        run: npm install --no-audit --no-fund --legacy-peer-deps

      - name: Create iPhone project
        run: |
          npx cap add ios
          npx cap sync ios

      - name: Add the Word Pop Kids app icon
        run: |
          D=ios/App/App/Assets.xcassets/AppIcon.appiconset
          for f in $D/*.png; do cp ios-res/AppIcon-1024.png "$f"; done
          ls $D

      - name: Settings Apple asks about
        run: |
          P=ios/App/App/Info.plist
          # iPad: Apple requires all four rotations for apps that run side by side with other apps
          /usr/libexec/PlistBuddy -c "Delete :UISupportedInterfaceOrientations~ipad" $P || true
          /usr/libexec/PlistBuddy -c "Add :UISupportedInterfaceOrientations~ipad array" $P
          for o in Portrait PortraitUpsideDown LandscapeLeft LandscapeRight; do
            /usr/libexec/PlistBuddy -c "Add :UISupportedInterfaceOrientations~ipad: string UIInterfaceOrientation$o" $P
          done
          /usr/libexec/PlistBuddy -c "Add :ITSAppUsesNonExemptEncryption bool false" $P || \
          /usr/libexec/PlistBuddy -c "Set :ITSAppUsesNonExemptEncryption false" $P

      - name: Save the App Store Connect key
        env:
          ASC_KEY_P8: ${{ secrets.ASC_KEY_P8 }}
        run: |
          mkdir -p ~/private_keys
          printf '%s\n' "$ASC_KEY_P8" > ~/private_keys/AuthKey.p8

      - name: Build and sign
        env:
          TEAM: ${{ secrets.APPLE_TEAM_ID }}
          KEY_ID: ${{ secrets.ASC_KEY_ID }}
          ISSUER: ${{ secrets.ASC_ISSUER_ID }}
        run: |
          cd ios/App
          if [ -d App.xcworkspace ]; then SRC="-workspace App.xcworkspace"; else SRC="-project App.xcodeproj"; fi
          xcodebuild $SRC -scheme App -configuration Release \
            -destination "generic/platform=iOS" -archivePath $RUNNER_TEMP/App.xcarchive \
            -allowProvisioningUpdates \
            -authenticationKeyPath ~/private_keys/AuthKey.p8 \
            -authenticationKeyID "$KEY_ID" -authenticationKeyIssuerID "$ISSUER" \
            DEVELOPMENT_TEAM="$TEAM" CODE_SIGN_STYLE=Automatic \
            TARGETED_DEVICE_FAMILY="1,2" \
            CURRENT_PROJECT_VERSION=${{ github.run_number }} MARKETING_VERSION=1.2.${{ github.run_number }} \
            archive

      - name: Upload to App Store Connect
        env:
          TEAM: ${{ secrets.APPLE_TEAM_ID }}
          KEY_ID: ${{ secrets.ASC_KEY_ID }}
          ISSUER: ${{ secrets.ASC_ISSUER_ID }}
        run: |
          cat > $RUNNER_TEMP/ExportOptions.plist <<EOF
          <?xml version="1.0" encoding="UTF-8"?>
          <!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
          <plist version="1.0"><dict>
            <key>method</key><string>app-store-connect</string>
            <key>destination</key><string>upload</string>
            <key>teamID</key><string>$TEAM</string>
            <key>signingStyle</key><string>automatic</string>
          </dict></plist>
          EOF
          xcodebuild -exportArchive -archivePath $RUNNER_TEMP/App.xcarchive \
            -exportOptionsPlist $RUNNER_TEMP/ExportOptions.plist -exportPath $RUNNER_TEMP/export \
            -allowProvisioningUpdates \
            -authenticationKeyPath ~/private_keys/AuthKey.p8 \
            -authenticationKeyID "$KEY_ID" -authenticationKeyIssuerID "$ISSUER"

      - name: Remove the key
        if: always()
        run: rm -rf ~/private_keys
```

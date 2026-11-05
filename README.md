# The Last Mercy · iOS build

The whole game is `www/index.html`, with three.js and the fonts stored next to it, so it runs with no internet connection.
Capacitor wraps it as an iPhone and iPad app. Codemagic builds it and sends it to TestFlight.

| Setting | Value |
|---|---|
| Bundle ID | `com.reallygoodgame.thelastmercy` |
| App name on the home screen | The Last Mercy |
| Orientation | Landscape only (iPhone and iPad), full screen, status bar hidden |
| App icon | `resources/icon-1024.png` (1024 × 1024, no transparency) |
| Encryption export question | Answered "No" automatically (`ITSAppUsesNonExemptEncryption = false`) |

## One-time setup
1. **App Store Connect → Apps → + → New App.** Platform iOS, your app name, English (U.S.), bundle ID `com.reallygoodgame.thelastmercy`
   (register it first under Certificates, Identifiers & Profiles → Identifiers if it isn't in the list), SKU `thelastmercy`, Full Access.
2. Open the new app → **App Information** → copy the **Apple ID** number into `codemagic.yaml` (`APP_STORE_APPLE_ID`).
3. In `codemagic.yaml`, set `app_store_connect:` to the exact name of the API key you already use in Codemagic for your other games.
4. Create a GitHub repo (for example `the-last-mercy`) and upload everything in this folder, keeping the folders as they are.
5. **Codemagic → Add application →** pick that repo. It finds `codemagic.yaml` on its own. Start the **The Last Mercy iOS** workflow.
6. When the build finishes processing in App Store Connect (usually 10–30 minutes), add it to your internal testers' group in **TestFlight**.

## Updating the game later
Replace `www/index.html` with the new version and push to `main`. Codemagic builds and uploads a new TestFlight build with the next build number.

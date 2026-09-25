# HYROX Block

A 12 week HYROX Vancouver training calendar. Anyone with the link can use it. Each person enters their own name and division, and their changes stay their own.

Two ways to run it:

* **Without sign in:** works as soon as it is on GitHub. Each person's plan is saved on the device they use.
* **With Google sign in (optional):** each person's plan is saved to their Google account and syncs between phone and computer.

---

## Part 1: Put it on GitHub Pages (about 5 minutes)

1. Sign in at [github.com](https://github.com) (create a free account if needed).
2. Click **+** at the top right, then **New repository**.
   * Name: `hyrox-block`
   * Visibility: **Public**
   * Click **Create repository**.
3. On the new repository page, click **uploading an existing file**.
4. Drag in **all the files from this folder** (not the folder itself): `index.html`, `firebase-config.js`, `manifest.webmanifest`, `sw.js`, the three `.png` icons, `firestore.rules` and this `README.md`.
5. Click **Commit changes**.
6. Go to **Settings**, then **Pages** in the left menu.
   * Source: **Deploy from a branch**
   * Branch: **main**, folder **/ (root)**, then **Save**.
7. Wait 1 to 2 minutes and refresh that page. Your link appears at the top:
   `https://YOUR-USERNAME.github.io/hyrox-block/`

That link is what you share. The app works now, with each person's data kept on their own device.

---

## Part 2: Turn on "Sign in with Google" (about 10 minutes, optional)

### A. Create a Firebase project

1. Go to [console.firebase.google.com](https://console.firebase.google.com) and sign in with your Google account.
2. Click **Create a project**. Name it `hyrox-block`. You can switch Google Analytics off. Click **Create**.

### B. Turn on Google sign in

1. In the left menu: **Build**, then **Authentication**, then **Get started**.
2. Under **Sign-in method**, click **Google**, switch it **on**, pick your email as the support email and click **Save**.
3. Open the **Settings** tab (still in Authentication), then **Authorized domains**, then **Add domain**, and enter:
   `YOUR-USERNAME.github.io`

### C. Create the database

1. In the left menu: **Build**, then **Firestore Database**, then **Create database**.
2. Pick a location close to you (for Vancouver, `northamerica-northeast1` or `nam5` are fine) and start in **production mode**.
3. Open the **Rules** tab, delete what is there, paste in the contents of `firestore.rules`, and click **Publish**.
   These rules mean each person can only ever see and change their own plan.

### D. Connect the app to Firebase

1. Click the **gear icon** next to Project Overview, then **Project settings**.
2. Scroll to **Your apps** and click the **web icon** (`</>`). Give it a nickname and click **Register app**. You do not need Firebase Hosting.
3. Firebase shows a `firebaseConfig` block. Copy the values of `apiKey`, `authDomain`, `projectId` and `appId`.
4. Back on GitHub, open `firebase-config.js` in your repository, click the **pencil icon**, replace the four `PASTE...` values with yours, and click **Commit changes**.
5. Wait a minute, then open your link. A **Sign in with Google** button now appears at the top.

The `apiKey` in Firebase web config is designed to be public. Your data is protected by the rules from step C, not by keeping the key secret.

**Cost:** Firebase's free Spark plan covers far more than a group of friends will use. You do not need to add a card.

---

## Adding it to your home screen

Open your GitHub link in the browser (paste it into the address bar rather than tapping it inside another app).

* **Android (Chrome):** tap **⋮**, then **Add to Home screen** or **Install app**.
* **iPhone:** in Safari tap **Share**, then **Add to Home Screen**. Chrome on iOS 16.4 or newer also has it under the Share icon in the address bar.

On iPhone, the home screen app keeps its own storage separate from Safari. If you use Google sign in, sign in once inside the home screen app too.

---

## Updating the app later

Upload the changed files to the repository the same way. Then open `sw.js`, change `hyrox-v1` to `hyrox-v2` (and so on each time), and commit. That makes phones pick up the new version instead of the saved copy.

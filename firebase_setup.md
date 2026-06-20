# Google Firebase Realtime Database Setup Guide

This project features a **dual-mode database architecture**. By default, it falls back seamlessly to `localStorage` (so the website is fully functional out of the box). To enable global, real-time database sync across all customer devices and the admin dashboard, follow these simple steps to set up your free Google Firebase database.

---

## 1. Create a Firebase Project (100% Free)
1. Go to the [Firebase Console](https://console.firebase.google.com/).
2. Click **Add project** (or **Create a project**).
3. Enter a project name (e.g., `skyleaf-studios`) and click **Continue**.
4. Disable Google Analytics for this project (optional, speeds up creation) and click **Continue**.
5. Once your project is ready, click **Continue**.

---

## 2. Set Up the Realtime Database
1. In the left-hand sidebar menu, expand the **Build** tab and select **Realtime Database**.
2. Click **Create Database**.
3. Choose a database location closest to you (e.g., *United States (us-central1)* or *Singapore (asia-southeast1)*) and click **Next**.
4. Select **Start in test mode** (this allows reading and writing immediately for staging/development).
5. Click **Enable**.

---

## 3. Configure Database Security Rules
To make sure data can be loaded by customers and managed by the admin panel, verify the database rules are open for public prototype testing:
1. In the Realtime Database dashboard, switch to the **Rules** tab at the top.
2. Edit the JSON rules block to allow public reading and writing:
   ```json
   {
     "rules": {
       ".read": "true",
       ".write": "true"
     }
   }
   ```
3. Click **Publish**.
   > [!NOTE]
   > Firebase will show a warning about rules being defined as public. This is normal and expected for a client-side prototype.

---

## 4. Get Your Firebase Config Keys
1. Click the gear icon next to **Project Overview** in the left sidebar and select **Project settings**.
2. Under the **General** tab, scroll down to the *Your apps* section.
3. Click the Web icon (represented by `</>`).
4. Register your app by entering a nickname (e.g., `Skyleaf Web App`) and click **Register app**.
5. You will see a `firebaseConfig` object containing credentials. It looks like this:
   ```javascript
   const firebaseConfig = {
     apiKey: "AIzaSy...",
     authDomain: "your-project-id.firebaseapp.com",
     databaseURL: "https://your-project-id-default-rtdb.firebaseio.com",
     projectId: "your-project-id",
     storageBucket: "your-project-id.appspot.com",
     messagingSenderId: "1234567890",
     appId: "1:1234567890:web:abcdef..."
   };
   ```

---

## 5. Add Credentials to the Website
To enable sync, copy and paste your custom `firebaseConfig` object at the top of the javascript section (replacing the placeholders) in these three files:
1. [index.html](file:///c:/Users/harsh/OneDrive/Desktop/photoshop/index.html) (around line 1713)
2. [collections.html](file:///c:/Users/harsh/OneDrive/Desktop/photoshop/collections.html) (around line 583)
3. [admin.html](file:///c:/Users/harsh/OneDrive/Desktop/photoshop/admin.html) (around line 757)

### Verification & Fallback Behavior
* **Firebase Mode**: If `apiKey` is provided, the pages automatically connect to your Firebase database. All changes in the admin panel are saved instantly to the cloud and reflect on customer devices in real-time.
* **Offline Fallback**: If the credentials are left as `"YOUR_API_KEY"` (default), the website falls back seamlessly to saving and loading all dynamic categories, portfolio items, reels, and messages locally in the browser's `localStorage`.

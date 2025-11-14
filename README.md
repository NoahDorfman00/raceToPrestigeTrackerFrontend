# Race to Master Prestige Leaderboard Frontend

A simple HTML/CSS/JS frontend that displays a leaderboard by reading data from Firebase Storage.

## Setup

1. **Update Firebase Configuration**

   Open `index.html` and update the Firebase config (around line 356) with your actual Firebase project credentials:

   ```javascript
   const firebaseConfig = {
       apiKey: "YOUR_API_KEY",
       authDomain: "racetomasterprestige.firebaseapp.com",
       projectId: "racetomasterprestige",
       storageBucket: "racetomasterprestige.firebasestorage.app",
       messagingSenderId: "YOUR_SENDER_ID",
       appId: "YOUR_APP_ID"
   };
   ```

2. **Configure Firebase Storage Rules**

   Make sure your Firebase Storage allows public read access for the files:

   ```json
   rules_version = '2';
   service firebase.storage {
     match /b/{bucket}/o {
       match /{allPaths=**} {
         allow read: if true;
         allow write: if false; // Only backend can write
       }
     }
   }
   ```

3. **Configure Firebase Storage CORS (Important!)**

   Firebase Storage blocks cross-origin requests by default. You have two options:

   **Option A: Use CORS Proxy (Quick Fix - Already Enabled)**
   
   The CORS proxy is already enabled in `index.html` (line 374). This works for development but is not recommended for production.

   **Option B: Configure Firebase Storage CORS (Recommended for Production)**
   
   Run this command (requires Google Cloud SDK):
   
   ```bash
   gsutil cors set cors.json gs://racetomasterprestige.firebasestorage.app
   ```
   
   The `cors.json` file is already included in this project. After running this command, you can set `USE_CORS_PROXY = false` in `index.html` to disable the proxy.

## Running Locally

**Important:** You cannot open `index.html` directly in a browser (file:// protocol) due to CORS restrictions. You must use a local web server.

### Option 1: Python (Recommended)

```bash
cd /Users/noahdorfman/Documents/raceToPrestigeFront
python3 -m http.server 8000
```

Then open: http://localhost:8000

### Option 2: Node.js

```bash
cd /Users/noahdorfman/Documents/raceToPrestigeFront
npx http-server -p 8000
```

Then open: http://localhost:8000

### Option 3: PHP

```bash
cd /Users/noahdorfman/Documents/raceToPrestigeFront
php -S localhost:8000
```

Then open: http://localhost:8000

## How It Works

1. On page load, the frontend fetches `streams_data.json` from Firebase Storage
2. The leaderboard is calculated and sorted by prestige (highest first), then by level
3. Click the info icon (ℹ) on any entry to expand and see:
   - Latest annotated OCR frame
   - Recent OCR detection logs
4. Click "Refresh" to reload data from Firebase Storage

## Files Structure

- `index.html` - Main frontend file with all HTML, CSS, and JavaScript


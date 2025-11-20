# Call of Duty Black Ops 7: Race to Master Prestige

A real-time leaderboard tracking Call of Duty Black Ops 7 streamers racing to Master Prestige. This frontend displays streamer progress, prestige levels, and current ranks by fetching data from Firebase Storage.

## What is this?

This is a live leaderboard that tracks multiple Call of Duty Black Ops 7 streamers as they race to reach Master Prestige (Prestige 20). The leaderboard:

- Displays streamers ranked by prestige level and current level
- Shows real-time online/offline status
- Provides links to watch live streams
- Shows annotated detection frames and OCR logs for verification

The backend system uses OCR (Optical Character Recognition) to automatically detect prestige and level information from stream overlays, then updates this leaderboard in real-time.

## Quick Start

1. **Configure Firebase**: Update the Firebase configuration in `index.html` (around line 367) with your Firebase project credentials.

2. **Set up Firebase Storage CORS**: Configure CORS for Firebase Storage to allow cross-origin requests:
   ```bash
   gsutil cors set cors.json gs://your-storage-bucket
   ```

3. **Run locally**: Serve the files using a local web server (required due to CORS):
   ```bash
   python3 -m http.server 8000
   # or
   npx http-server -p 8000
   ```
   Then open `http://localhost:8000`

## How It Works

- Fetches `streams_data.json` from Firebase Storage on page load
- Calculates rankings based on prestige (highest first), then level
- Displays streamer information with online/offline status
- Click the info icon (ℹ) on any entry to view detection frames and OCR logs

## Project Structure

- `index.html` - Single-page application with all HTML, CSS, and JavaScript
- `cors.json` - CORS configuration for Firebase Storage
- `social.png` - Social media preview image

## License

This project is open source and available for public use.

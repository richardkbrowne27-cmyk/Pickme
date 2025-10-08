# Hiring Cafe Automation Bot Landing Page

This repo contains a single static HTML page (`Pick-me-Belay.html`) that showcases the Hiring Cafe automation bot concept.

## Prerequisites
- A modern web browser (Chrome, Edge, Firefox, Safari, etc.).
- Optionally, a lightweight HTTP server if you prefer to avoid opening the file directly from disk.

## Quick Preview
1. Locate the `Pick-me-Belay.html` file in the repository.
2. Double-click the file (or right-click → **Open With**) to open it in your browser.
3. Interact with the page:
   - Click **Generate Bot Gameplan** to populate the automation steps and trigger the toast message.
   - Use the resource links to see the confetti effect and toast messaging.
   - Paste text or a URL anywhere on the page to observe the clipboard toast behavior.

## Local Server Preview (Optional)
Serving the file over HTTP gives you a slightly more realistic environment and avoids some browsers' local file restrictions.

```bash
# From the repository root
python3 -m http.server 8000
```

Then visit [http://localhost:8000/Pick-me-Belay.html](http://localhost:8000/Pick-me-Belay.html) in your browser.

Stop the server with `Ctrl+C` when finished.

## Testing Checklist
- ✅ Button populates plan steps and shows toast.
- ✅ Clicking resource links shows toast/confetti before opening the destination.
- ✅ Pasting plain text vs. a URL shows distinct toast messages.
- ✅ Confetti animation renders smoothly without console errors.

If you encounter issues, check your browser's developer console for errors and ensure no extensions are blocking pop-ups.

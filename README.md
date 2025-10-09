# Hiring Cafe Automation Bot Landing Page

This repo contains a static HTML landing page (`index.html`) that showcases the Hiring Cafe automation bot concept.
For backwards compatibility, `Pick-me-Belay.html` now performs a zero-delay redirect to the refreshed experience so any
existing bookmarks continue to work.

## Prerequisites
- A modern web browser (Chrome, Edge, Firefox, Safari, etc.).
- Optionally, a lightweight HTTP server if you prefer to avoid opening the file directly from disk.

## Quick Preview
1. Locate the `index.html` file (or the legacy `Pick-me-Belay.html`, which will redirect).
2. Double-click the file (or right-click → **Open With**) to open it in your browser.
3. Interact with the page:
   - Drag and drop (or click to upload) a resume file to sync it with the automation workflow.
   - Add or remove target job titles in the **Target Roles** section.
   - Toggle the **Quick Apply** and **Employer website** pathways to see how the plan adjusts.
   - Update pre-filled screening answers so the bot can reuse them.
   - Click **Generate Bot Gameplan** or **Launch Automation** to see the toasts, typing animation, and confetti.

## Local Server Preview (Optional)
Serving the file over HTTP gives you a slightly more realistic environment and avoids some browsers' local file restrictions.

```bash
# From the repository root
python3 -m http.server 8000
```

Then visit [http://localhost:8000/index.html](http://localhost:8000/index.html) in your browser.

Stop the server with `Ctrl+C` when finished.

## Deploying to Netlify
Netlify can host the page directly from this repository or from a zipped download.

1. Sign in to [Netlify](https://app.netlify.com/) and choose **Add new site → Deploy manually**.
2. Drag the entire project folder (or just the `index.html` file) into the uploader.
3. After the deploy finishes, Netlify will give you a temporary `*.netlify.app` URL. Visit it to confirm the page loads and the interactions work.
4. Visit **Site configuration → Build & deploy → Build settings** and set **Build image selection** to a supported image such as **Ubuntu 20.04 (Focal)**. Netlify no longer supports the legacy **Trusty** image, so updating this now prevents deployment failures.
5. (Optional) Enable HTTPS by ensuring **Domain management → HTTPS** has an active certificate once your custom domain is connected.

### Connecting `richardkbrowne.com`
1. In the Netlify dashboard, open your site and go to **Domain management**.
2. Click **Add custom domain** and enter `richardkbrowne.com`.
3. Follow the prompts to verify ownership. Netlify will provide the DNS records to add at your registrar (typically `www` and apex `@` CNAME/ALIAS records pointing to Netlify).
4. Update the DNS settings with your domain registrar. Propagation can take up to 24 hours, but it often completes within minutes.
5. Back in Netlify, click **Verify** once the DNS changes have propagated. Netlify will automatically issue an SSL certificate for the domain.
6. Set `richardkbrowne.com` (or `www.richardkbrowne.com`) as the primary domain so all traffic redirects correctly.

## Testing Checklist
- ✅ Resume upload surface accepts drag-and-drop and file picker input.
- ✅ Added job titles render as removable chips and feed the automation steps.
- ✅ Pathway toggles (Quick Apply, Employer website) update the blueprint copy.
- ✅ Screening answers can be edited and are reflected in the plan summary.
- ✅ Buttons trigger toasts, typing animation, and confetti without console errors.
- ✅ Resource links still show toast/confetti before opening the destination.
- ✅ Pasting plain text vs. a URL shows distinct toast messages.

If you encounter issues, check your browser's developer console for errors and ensure no extensions are blocking pop-ups.

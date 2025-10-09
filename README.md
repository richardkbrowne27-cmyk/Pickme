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

If you do not see the confetti or toast notifications, check that your browser is not blocking pop-ups or JavaScript execution.

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

> **Tip:** The included `netlify.toml` file forces all traffic (including legacy `Pick-me-Belay.html` hits) to render `index.html` so the refreshed bot experience is always served.

### Resolving GitHub merge conflicts

If GitHub shows the "This branch has conflicts" banner (as in the screenshot that flags `Pick-me-Belay.html` and `README.md`), the deploy preview and redirect checks will keep failing until the conflicts are resolved locally. Use the following flow:

1. Ensure you have the latest default branch locally:
   ```bash
   git checkout main
   git pull origin main
   ```
2. Switch back to your working branch and merge in the latest default branch so you can address the conflicts on your machine:
   ```bash
   git checkout work
   git merge main
   ```
3. Git will pause at the conflicting files. Open each file, remove the `<<<<<<<`, `=======`, and `>>>>>>>` markers, and keep the desired content (the redirect shim plus the updated README guidance).
4. After editing, stage and commit the resolution:
   ```bash
   git add Pick-me-Belay.html README.md
   git commit -m "Resolve merge conflicts"
   git push origin work
   ```

Once GitHub sees a clean branch, the Netlify checks (Header rules, Deploy Preview, Pages changed, Redirect rules) will re-run automatically and should pass.

### Forcing a fresh deploy

If the live site still shows the legacy design after merging, trigger a clean deploy:

1. In Netlify, open your site dashboard and click **Deploys**.
2. Use **Trigger deploy → Clear cache and deploy site** to purge the CDN and redeploy the latest commit.
3. Wait for the deploy to finish, then reload `https://richardkbrowne.com` (hard refresh with `Cmd+Shift+R` / `Ctrl+Shift+R`) to pull the new assets.

Once the redeploy completes, the redirect and CDN cache clear ensure both `richardkbrowne.com` and `richardkbrowne.com/Pick-me-Belay.html` load the Trinidad & Tobago themed automation launch pad.

### Connecting `richardkbrowne.com`
1. In the Netlify dashboard, open your site and go to **Domain management**.
2. Click **Add custom domain** and enter `richardkbrowne.com`.
3. Follow the prompts to verify ownership. Netlify will provide the DNS records to add at your registrar (typically `www` and apex `@` CNAME/ALIAS records pointing to Netlify).
4. Update the DNS settings with your domain registrar. Propagation can take up to 24 hours, but it often completes within minutes.
5. Back in Netlify, click **Verify** once the DNS changes have propagated. Netlify will automatically issue an SSL certificate for the domain.
6. Set `richardkbrowne.com` (or `www.richardkbrowne.com`) as the primary domain so all traffic redirects correctly.

## Detailed Testing Walkthrough

Follow these steps to validate the interactive flow end-to-end:

1. **Open the page** using the quick preview steps above or by serving it locally.
2. **Upload a resume** by dragging a PDF or DOCX onto the upload drop zone. You should see the filename appear in the activity feed.
3. **Target roles** by typing two or three sample titles (e.g., *Staff Accountant*, *Treasury Analyst*). Each entry should become a removable chip and the blueprint summary should mention the chosen roles.
4. **Configure pathways:**
   - Toggle **Quick Apply** on and off and note the change in the automation steps (the plan should reference streamlined application handling when enabled).
   - Toggle **Employer website** and confirm the plan references navigating to external career portals when it is active.
5. **Screening answers** – Edit the pre-filled answers (e.g., availability, work authorization) and click **Save answers**. The saved confirmation toast and updated summary confirm the inputs were captured.
6. **Run the bot simulation** by pressing **Generate Bot Gameplan** followed by **Launch Automation**. Watch for the typing indicator, toasts, and confetti celebration to ensure the scripted reactions still fire.
7. **Resource validation** – Click each resource link in the footer. They should briefly show a toast/confetti before opening in a new tab.
8. **Clipboard handling** – Paste plain text into the notes field to see the friendly toast, then paste a URL to confirm the link-specific toast variant appears.

## Testing Checklist
- ✅ Resume upload surface accepts drag-and-drop and file picker input.
- ✅ Added job titles render as removable chips and feed the automation steps.
- ✅ Pathway toggles (Quick Apply, Employer website) update the blueprint copy.
- ✅ Screening answers can be edited and are reflected in the plan summary.
- ✅ Buttons trigger toasts, typing animation, and confetti without console errors.
- ✅ Resource links still show toast/confetti before opening the destination.
- ✅ Pasting plain text vs. a URL shows distinct toast messages.

If you encounter issues, check your browser's developer console for errors and ensure no extensions are blocking pop-ups.

## Troubleshooting Errors

When something is not working, try the quick checks below to isolate and fix the issue:

1. **Browser console diagnostics**
   - Open the page and use `Cmd+Option+I` / `Ctrl+Shift+I` to launch DevTools.
   - Review the **Console** tab for red error messages. Most issues will link to the exact line in `index.html` where the script stopped running.
   - If an extension is blocking scripts (ad blockers, privacy shields, etc.), temporarily disable it or open a private/incognito window and retest.
2. **Serve from a local server**
   - Some browsers restrict `fetch`, `FileReader`, or drag-and-drop events when loading straight from the filesystem.
   - Use the bundled `python3 -m http.server 8000` command (or any simple static server) so the automation flow runs under `http://localhost:8000`.
3. **Reset the interaction state**
   - Click the browser refresh button or press `Cmd+Shift+R` / `Ctrl+Shift+R` to force a hard reload that clears cached scripts.
   - If the resume uploader seems frozen, delete any partially added roles, refresh, and try uploading again—this clears in-memory state.
4. **Netlify deploy errors**
   - Open your Netlify site → **Deploys**. Failed deploys show a red ❌; click the deploy to view the log.
   - Common fixes include switching the build image to Ubuntu 20.04, confirming `index.html` exists at the repo root, and ensuring `netlify.toml` is present so redirects resolve correctly.
   - After fixing the root cause, trigger **Deploy site → Clear cache and deploy site** to rebuild with a clean cache.
5. **Domain still serving the old version**
   - Verify DNS propagation using a tool such as `https://dnschecker.org` for `richardkbrowne.com` and `www.richardkbrowne.com`.
   - Once DNS is correct, use Netlify → **Domain management → HTTPS** to provision/renew the certificate, then perform another hard refresh locally.

If an error persists after these steps, capture a screenshot of the console message and the action you were performing. That context makes it much easier to pinpoint the fix.

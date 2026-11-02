# Publish with GitHub Pages

1. Extract this ZIP on your computer.
2. Sign in to GitHub and open https://github.com/new.
3. Name the repository `marketplace-ops-copilot`. Choose Public for a public portfolio repository. Leave the options to add a README, .gitignore, and license unchecked; a README and .gitignore are already included.
4. Create the repository. Choose **uploading an existing file** on the empty repository screen (or **Add file → Upload files**).
5. Open the extracted `marketplace-ops-copilot` folder. Drag its CONTENTS into the upload area, including the `docs` folder. Do not upload the ZIP or its outer folder. `index.html` must appear directly at the repository root beside `app.js` and `style.css`. Include `.nojekyll` and `.gitignore` if your file picker shows them.
6. Commit the files to `main` with the message `Add Marketplace Ops Copilot prototype`.
7. Open **Settings → Pages**. Under **Build and deployment**, choose **Deploy from a branch**. Select **main** and **/(root)**, then **Save**.
8. Wait for the Pages deployment to finish. Check the **Actions** tab for progress. The Pages settings page will show the live URL.
9. With account `aishw-m` and the repository name above, the expected URL is https://aishw-m.github.io/marketplace-ops-copilot/ . Use the URL GitHub displays as authoritative.
10. Open the URL, confirm the demo loads, try the 14-day comparison, upload the included single-merchant CSV, and open/download a merchant brief.

GitHub Pages publishes the website publicly in this setup. This package does not change the existing private Site or publish anything automatically.

For later edits, upload changed files to the same repository and commit to main; Pages republishes the selected source. If the page is missing, check that index.html is at the root and Pages points to main / (root).

Official guidance: https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site

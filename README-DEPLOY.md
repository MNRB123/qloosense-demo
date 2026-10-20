# QlooSense AI — Option A standalone comparison demo

## What it does
A single-file responsive HTML demo calls `https://qloosense-ai.vercel.app/api/recommendations/compare` and displays baseline/Qloo results and execution logs. It does not contain an API key.

**Accuracy note:** “Without Qloo” is a deterministic baseline, not a real ChatGPT/LLM answer. The UI makes that explicit.

## 1. Extract and open
Extract this ZIP to `C:\QlooHackathon\qloosense-option-a`, then open that folder in VS Code.

## 2. Preview locally
Recommended: install the VS Code **Live Server** extension, right-click `index.html` → **Open with Live Server**.
Or in a terminal opened in this folder, run:
```powershell
python -m http.server 5500
```
Then visit `http://localhost:5500`.

## 3. Test
Keep the default `art gallery` / `Surat` values and click **Run live comparison**. The page sends a POST request to the production API.

If the browser shows a CORS error, backend CORS policy must allow the demo's origin. Do not put `QLOO_API_KEY` into HTML or any frontend file.

## 4. Publish as a separate Vercel static project
This is the lower-risk route because it does not change the working backend project.

1. Create a separate GitHub repository, e.g. `qloosense-demo`.
2. Add `index.html` and this README to the repository root. Never add `.env` or secrets.
3. Commit and push the files to `main`.
4. In Vercel, choose **Add New → Project**, import the new repository.
5. For a plain static HTML site, no build command is needed; set output directory to `.` if Vercel asks.
6. Deploy and open the generated URL.
7. Click **Run live comparison** and verify results and logs on the deployed page.

## Troubleshooting
- **CORS error:** update the Express backend CORS policy to permit the deployed static demo origin.
- **404/500:** test `POST https://qloosense-ai.vercel.app/api/recommendations/compare` and inspect the response.
- **Unexpected empty card:** open browser DevTools (F12 → Network → compare request → Response). If response keys differ from the mappings in `index.html`, adjust the mapping.
- Never log or publish the Qloo API key.


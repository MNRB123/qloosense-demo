# QlooSense AI — Taste-Aware City Discovery

**Live demo:** https://qloosense-demo.vercel.app  
**Backend API:** https://qloosense-ai.vercel.app/api/recommendations/compare  
**Demo repository:** https://github.com/MNRB123/qloosense-demo

QlooSense AI is a judge-friendly demo of taste-aware local discovery. Enter an interest and a city, then compare a transparent baseline with recommendations returned by the Qloo-powered backend. The interface displays returned place information and an execution trace so reviewers can inspect the request flow.

## What it demonstrates

- Interest and city inputs shared across both comparison panels.
- A `With Qloo` panel that calls the deployed backend and renders returned API data.
- Live execution logs supplied by the backend, including query planning and validation steps.
- A transparent `Without Qloo` baseline that does **not** invent venue names or claim verified venue data.
- A browser-only frontend that never needs the Qloo API key.

## Try the live demo

1. Open https://qloosense-demo.vercel.app.
2. Enter an interest such as `art gallery`.
3. Enter a city such as `Surat`.
4. Select a result limit and click **Run live comparison**.
5. Inspect the Qloo result card, status message, metrics, and live agent logs.

The demo has returned **Kaku Art Gallery** for `art gallery` in `Surat` during testing. Results depend on the upstream API response and may change.

## Architecture

```text
Browser (static index.html)
        |
        | POST /api/recommendations/compare
        v
QlooSense AI backend on Vercel
        |
        | server-side API request
        v
Qloo API
```

The static demo repository and the backend are deployed separately. The frontend calls the backend URL configured in `index.html`; the backend keeps the Qloo credential in its server-side environment.

## Run locally

This repository is a standalone HTML demo and does not require a Node.js build.

1. Clone the repository:

   ```bash
   git clone https://github.com/MNRB123/qloosense-demo.git
   cd qloosense-demo
   ```

2. Open `index.html` directly in a browser, or serve the folder with VS Code Live Server.
3. Use the live comparison form to call the deployed backend.

If you deploy a separate copy, ensure the backend allows browser requests from that demo's origin (CORS).

## Deploy the static demo to Vercel

- Import this repository into Vercel.
- Framework preset: **Other**.
- Root directory: repository root (`./`).
- Build command: leave blank.
- Install command: leave blank.
- Output directory: `.`.
- Deploy.

No Qloo API key is required in this frontend project.

## API and data handling

The comparison UI calls:

`POST https://qloosense-ai.vercel.app/api/recommendations/compare`

The request uses the same interest and city for the comparison. The backend is responsible for Qloo API access and response validation. Do not put `QLOO_API_KEY` or any other secret in `index.html`, browser JavaScript, or this repository.

## Fair-comparison note

**“Without Qloo” is a deterministic, no-venue-lookup baseline. It is not a ChatGPT or other LLM response.** This demo does not claim that the baseline is an AI-generated answer. A true LLM-versus-Qloo comparison would require a separate model integration and should be labeled accordingly.

## Known limitations

- The number and quality of returned places depend on Qloo's available data and the query.
- An empty result is shown as empty rather than replaced with invented venue data.
- The baseline is intentionally simple and is not a personalized recommendation engine.
- The displayed execution trace is the trace returned by the backend; it is not an independent audit of Qloo internals.

## Security

- Never commit `.env` files, API keys, access tokens, or other secrets.
- Keep `QLOO_API_KEY` only in the backend deployment's server-side environment variables.
- Do not add the backend's secret environment variables to this static frontend's Vercel project.

## License

This demo's original code is released under the MIT License. See [`LICENSE`](LICENSE). Third-party services, logos, trademarks, and API data remain subject to their respective owners' terms.

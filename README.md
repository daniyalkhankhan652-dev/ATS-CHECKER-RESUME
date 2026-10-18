# 📄 ATS Resume Checker

A Streamlit app that scores a resume for ATS (Applicant Tracking System) friendliness and suggests concrete improvements, using Google's Gemini Flash model.

## Features

- Upload a resume as **PDF or DOCX**
- Overall **ATS score (0-100)** with a weighted category breakdown
- Prioritised **improvements** with example rewrites
- **Strengths**, **missing keywords** and **ATS formatting warnings**
- Optional **job description** to check how well the resume matches a role
- Download the report as JSON

## How the score works

The model rates five categories from 0-100. The app then computes the overall score itself using fixed weights, so scoring is consistent:

| Category | Weight |
|---|---|
| Keywords & relevance | 30% |
| Content & impact | 25% |
| Formatting & parsability | 20% |
| Structure & sections | 15% |
| Readability & length | 10% |

> This is an AI-based estimate, not the score from any specific real ATS. Use it as guidance.

## Project files

```
app.py            # Streamlit app
requirements.txt  # Python dependencies
README.md         # This file
```

## Run locally

1. Install Python 3.10+.
2. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```
3. Get a free API key from [Google AI Studio](https://aistudio.google.com/apikey).
4. Provide the key, either way:
   - Paste it in the app sidebar, **or**
   - Set an environment variable:
     ```bash
     # macOS / Linux
     export GEMINI_API_KEY="your-key"
     # Windows (PowerShell)
     $env:GEMINI_API_KEY="your-key"
     ```
5. Start the app:
   ```bash
   streamlit run app.py
   ```

## Configuration

| Name | Purpose | Default |
|---|---|---|
| `GEMINI_API_KEY` | Your Gemini API key (env var or Streamlit secret) | none |
| `GEMINI_MODEL` | Gemini model name (env var, secret, or sidebar field) | `gemini-3.8-flash` |

If you get a "model not found" error, change the model name in the sidebar to a current Flash model listed at https://ai.google.dev/gemini-api/docs/models.

## Push to GitHub (using the website, no command line)

1. Sign in at [github.com](https://github.com) and click **+** (top right) → **New repository**.
2. Name it (e.g. `ats-resume-checker`), choose **Public** (needed for the free Streamlit Community Cloud) and click **Create repository**.
3. On the new repo page click **uploading an existing file**.
4. Drag and drop `app.py`, `requirements.txt` and `README.md` into the page.
5. Add a commit message such as `Initial commit` and click **Commit changes**.

**Never upload your API key.** Do not put it in any file in the repo.

## Deploy on Streamlit Community Cloud

1. Go to [share.streamlit.io](https://share.streamlit.io) and sign in with GitHub.
2. Click **Create app** → **Deploy a public app from GitHub**.
3. Choose your repository, branch `main`, and main file path `app.py`.
4. Click **Advanced settings** and in the **Secrets** box add:
   ```toml
   GEMINI_API_KEY = "your-key-here"
   ```
5. Click **Deploy**. After a minute or two you get a public URL like `https://your-app-name.streamlit.app`.

To update the app later, edit a file on GitHub (pencil icon → **Commit changes**); Streamlit redeploys automatically.

## Troubleshooting

- **"Very little text could be extracted"**: the PDF is probably a scan/image. Export a text-based PDF or a DOCX.
- **"Analysis failed"**: check the API key, model name and your Gemini quota.
- **ModuleNotFoundError on deploy**: make sure `requirements.txt` is in the repo root.

## Privacy

The resume text is sent to the Gemini API for analysis. The app does not save uploaded files.

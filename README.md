# Signal Path — Azure CFx Technical Coach

Deploy this in ~5 minutes to get a permanent daily-practice URL.

## 1. Create the repo
1. In GitLab, click **New project → Create blank project**.
2. Name it `signal-path` (or anything you like). Visibility: Public (required for free GitLab Pages) or Private if you're on a paid tier that supports private Pages.
3. Don't initialize with a README (you already have one here).

## 2. Add the files
Upload both files from this folder into the repo root:
- `index.html` (the app)
- `README.md` (this file)

Easiest path: on the new project's page, use **"Upload File"** in the GitLab web UI and drop both in — no git command line needed.

## 3. Add the CI file that builds Pages
Create one more file in the repo root named **`.gitlab-ci.yml`** with this content:

```yaml
pages:
  stage: deploy
  script:
    - mkdir .public
    - cp -r * .public
    - mv .public public
  artifacts:
    paths:
      - public
  rules:
    - if: $CI_COMMIT_BRANCH == $CI_DEFAULT_BRANCH
```

Commit it. GitLab will automatically run a pipeline (**CI/CD → Pipelines**) — wait for it to turn green (~1 minute).

## 4. Get your URL
Go to **Deploy → Pages** in the left sidebar. Your live URL will look like:

```
https://<your-username>.gitlab.io/signal-path/
```

Bookmark that URL — that's your daily practice link.

## How to use it day to day
- **Flashcards**: front = a telecom/5G term from your real background, back = the direct Azure translation, with the specific vocabulary to say out loud. Rate yourself honestly — "Got it" is what drives the mastery bar per module.
- **Quiz**: multiple-choice, scenario-style, tied to the actual JD language (resiliency, elasticity, escalation, platform feedback).
- **Architecture Drill**: short-form writing practice for the JD's "write architecture-level documents" line — each prompt asks you to translate one of your real stories (CNDP, PAPN, DevEdge slicing) into Azure-facing technical language. Responses save locally in your browser.
- **Progress**: per-module mastery %, cards reviewed, and your day streak.

Everything saves in your browser's local storage on whatever device you open the URL on — no login, no backend, no data leaves your machine. If you clear your browser data or switch devices, progress resets (there's also a manual reset link in the footer).

## A note on accuracy
The AI module uses **"Microsoft Foundry"** rather than "Azure AI Foundry" — Microsoft rebranded that product in 2026. Everything else reflects standard, stable Azure architecture vocabulary (Well-Architected Framework pillars, AKS, VNets, ExpressRoute, storage redundancy tiers). Azure product names shift fairly often — if anything in the app feels outdated by the time of your screen, it's worth a quick Microsoft Learn check on that specific term before the call.

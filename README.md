# action-repo

A GitHub repository used to trigger webhook events for testing and demonstration purposes. Any push or pull request activity on this repo is automatically sent to the [webhook-repo](https://github.com/devarshidubey/webhook-repo) endpoint for processing and storage.

---

## Purpose

This repository serves as the **event source**. It has no application code — its sole purpose is to generate GitHub events (push, pull request, merge) that are captured by the webhook receiver.

---

## Configured Webhook

| Field         | Value                                                                 |
|---------------|-----------------------------------------------------------------------|
| Payload URL   | `https://webhook-repo-nfnj.onrender.com/webhook/receiver`            |
| Content Type  | `application/json`                                                    |
| Events        | Push, Pull Request                                                    |

---

## How to Trigger Events

### Push Event
```bash
git clone https://github.com/devarshidubey/actions-repo.git
cd actions-repo
echo "change" >> README.md
git add .
git commit -m "trigger push event"
git push origin main
```

### Pull Request Event
```bash
git checkout -b feature/test-branch
echo "pr test" >> README.md
git add .
git commit -m "trigger pull request"
git push origin feature/test-branch
```
Then open a Pull Request on GitHub from `feature/test-branch` → `main`.

### Merge Event
On the open Pull Request, click **Merge pull request** on GitHub.

---

## Event Flow

```
Push / PR / Merge on action-repo
        ↓
GitHub sends webhook POST request
        ↓
webhook-repo receives and stores event
        ↓
UI polls and displays the event
```
# GCP CI/CD with Cloud Build

A small Flask web app containerized with Docker, with a **Google Cloud Build** pipeline that builds the container image on every Git push and tags it with the commit SHA.

## How It Works

```
git push → Cloud Build trigger → docker build → image tagged with $SHORT_SHA → pushed to container registry
```

1. A Cloud Build trigger is connected to this GitHub repository.
2. On each push, Cloud Build reads `cloudbuild.yaml`.
3. It builds the Docker image using the `Dockerfile`.
4. The image is tagged with the short commit SHA (`$SHORT_SHA`) and pushed to the registry.

## Tech Stack

- Python, Flask, Gunicorn
- Docker
- Google Cloud Build
- Google Container/Artifact Registry

## Project Structure

```
.
├── app.py             # Flask app (greeting form)
├── templates/
│   └── index.html     # UI template
├── Dockerfile         # Container image definition
└── cloudbuild.yaml    # Cloud Build pipeline
```

## Run Locally

```bash
docker build -t greeting-app .
docker run -p 5000:5000 greeting-app
# open http://localhost:5000
```

## Cloud Build Setup

1. Enable the **Cloud Build** and **Container/Artifact Registry** APIs in your GCP project.
2. Cloud Build → **Triggers** → connect this GitHub repo → trigger on push to `main`.
3. Push a commit and check the build in **Cloud Build → History**.
4. Find the pushed image in the registry, tagged with the commit SHA.

## Future Improvements

- Add a deploy step (Cloud Run or GKE)
- Add test/lint step before the build
- Use Artifact Registry and a dedicated service account

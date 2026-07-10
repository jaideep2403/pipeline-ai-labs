# Episode 2: CI Build & Test

This episode turns the basic pipeline into a real CI workflow.

## What you learn

- How to build a Docker image in CI
- How to run the app inside the pipeline
- Why a sleep-based check is not enough
- How to replace fake tests with a real health check

## What the workflow does

The workflow in [`.github/workflows/ci-build-test.yml`](../.github/workflows/ci-build-test.yml) does the following:

1. Checks out the code
2. Builds the Docker image
3. Runs the container on port `5000`
4. Waits for the app to respond
5. Performs a real `curl -f` health check
6. Cleans up the container

## Pipeline Explanation

- The checkout step pulls in the application source and Dockerfile.
- The compile step catches obvious code issues before the image is built.
- The Docker build step creates the runtime artifact the same way a release job would.
- The container run step starts the application in a controlled environment.
- The health check step verifies the app responds at `/healthz`, not just that the process exists.
- The cleanup step removes the container so the runner stays clean for future jobs.

## Why this episode matters

This is the first place where the pipeline starts behaving like a real CI system.

The key lesson is that a pipeline can be green for the wrong reasons. A command can succeed while the app is still unhealthy unless you test the real endpoint.

## Walkthrough

The application in [`app/app.py`](app/app.py) listens on `0.0.0.0:5000`.

The Dockerfile builds a Python 3.11 image, installs Flask, and launches the app.

The workflow then runs:

```bash
docker build -t cicd-prod .
docker run -d -p 5000:5000 --name prod-container cicd-prod
curl -f http://localhost:5000/healthz
```

The `-f` flag is important because it makes `curl` fail if the HTTP status is not successful.

## Practice exercises

1. Break the Flask route and see which step fails.
2. Change the app port and update the workflow to match.
3. Replace the wait loop with a retrying health check command.
4. Add a second test endpoint and verify both routes.
5. Make the health endpoint return `500` and confirm the pipeline fails.
6. Add an extra environment variable and see how it flows into the container.

For scenario-based interview practice, see [INTERVIEW-QA.md](./INTERVIEW-QA.md).

## Key takeaway

Episode 2 teaches that CI should validate behavior, not just execution.

## Stay Connected

- YouTube: [Learn With DevOps Engineer](https://www.youtube.com/@learnwithdevopsengineer)
- Instagram: [@learnwithdevopsengineer](https://www.instagram.com/learnwithdevopsengineer/)
- Newsletter: [Beehiiv updates](https://learnwithdevopsengineer.beehiiv.com/)
- Topmate: [Book a session](https://topmate.io/learnwithdevopsengineer)

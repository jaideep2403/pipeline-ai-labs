# Episode 4: Deployment Success But App Down

This episode shows how a pipeline can report success even when the application is not actually healthy.

## What you learn

- Why deployment success is not the same as application health
- Why `sleep` is not a real verification step
- How to add a real endpoint check
- How to think about false positives in CI

## What the workflow does

The workflow in [`.github/workflows/deploy-pipeline.yml`](../.github/workflows/deploy-pipeline.yml) does this:

1. Checks out the code
2. Cleans up any previous container
3. Builds the image
4. Runs the container
5. Sleeps for a few seconds
6. Prints a success message

The problem is that a sleep does not prove the app is actually responding.

## Pipeline Explanation

- The checkout step retrieves the source and Dockerfile used for deployment.
- The cleanup step removes any container left behind by a previous run.
- The build step produces the application image that the pipeline is about to ship.
- The container run step starts the app in the same shape the user would experience.
- The verification step checks `/healthz` so the job only passes when the app actually answers.
- The final cleanup keeps the host clean and prevents stale containers from hiding the next failure.

## Why this episode matters

This is the first failure story in the series.

The container may start, but:

- the app may still be unhealthy
- the port may be wrong
- the process may crash after startup
- the pipeline may still print "success"

## Walkthrough

The Flask app in `app/app.py` listens on `0.0.0.0:5000` and returns:

```text
Application is running
```

The pipeline builds the image and starts the container, but it does not verify the HTTP response. That is why the result can be misleading.

## Better pattern

Instead of relying on sleep, use a real health check:

```bash
curl -f http://localhost:5000/healthz
```

That way the pipeline fails if the app is not actually reachable.

## Practice exercises

1. Replace the sleep step with a retry loop.
2. Add `curl -f` and make the job fail if the endpoint is down.
3. Break the app route and observe the failure.
4. Add a cleanup step that always runs.
5. Change the container port and trace where the failure appears.
6. Modify the app response and confirm the pipeline catches it.

For scenario-based interview practice, see [INTERVIEW-QA.md](./INTERVIEW-QA.md).

## Key takeaway

Episode 4 shows that a green pipeline can still hide a broken app.

## Stay Connected

- YouTube: [Learn With DevOps Engineer](https://www.youtube.com/@learnwithdevopsengineer)
- Instagram: [@learnwithdevopsengineer](https://www.instagram.com/learnwithdevopsengineer/)
- Newsletter: [Beehiiv updates](https://learnwithdevopsengineer.beehiiv.com/)
- Topmate: [Book a session](https://topmate.io/learnwithdevopsengineer)

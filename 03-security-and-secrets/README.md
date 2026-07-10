# Episode 3: Security & Secrets

This episode shows how a working pipeline can still be insecure.

## What you learn

- Why secrets should not be hardcoded
- How environment variables move through CI jobs
- How logs can leak sensitive information
- How to think about least privilege in pipelines

## What the workflow does

The workflow in [`.github/workflows/security-pipeline.yml`](../.github/workflows/security-pipeline.yml) intentionally demonstrates a bad pattern:

1. Build the Docker image
2. Store a secret in the job environment
3. Pass the secret into the container
4. Print container logs

The log step is the problem. It shows how a secret can accidentally leak into output.

## Pipeline Explanation

- The checkout and compile steps confirm the code is syntactically valid before any security-sensitive work begins.
- The Docker build step creates the app image so the secret handling is tested in the same artifact path used for delivery.
- The container run step injects the secret through the job environment, which is the pattern you would replace with GitHub Secrets in real usage.
- The health check step proves the app is running without exposing sensitive values.
- The verification step confirms the secret exists only in the intended runtime context.
- The cleanup step removes the container and keeps the runner state predictable.

## Why this episode matters

A pipeline can be "successful" and still be unsafe.

This episode teaches you to notice:

- plain-text secrets
- unnecessary logging
- overexposed environment variables
- weak secret-handling habits

## Walkthrough

The app is still the same Flask app listening on `0.0.0.0:5000`.

The key lines in the workflow are:

```bash
echo "API_KEY=my-super-secret-key" >> $GITHUB_ENV
docker run -d -p 5000:5000 -e API_KEY=$API_KEY --name secure-container cicd-secure
docker logs secure-container
```

That final `docker logs` command is the intentional security mistake.

## Safer approach

In a real pipeline, you would:

1. Store secrets in GitHub Secrets or a secret manager
2. Inject them only when needed
3. Avoid printing them in logs
4. Rotate them if they ever leak

## Practice exercises

1. Replace the hardcoded secret with a GitHub secret.
2. Remove the log step and confirm the secret no longer appears.
3. Add a masking command to hide sensitive output.
4. Search the repository for other values that should not be committed.
5. Add a fake secret and verify it never appears in the logs.
6. Remove the secret entirely and see which parts of the workflow still pass.

For scenario-based interview practice, see [INTERVIEW-QA.md](./INTERVIEW-QA.md).

## Key takeaway

Episode 3 shows that a pipeline can be functional and still be insecure.

## Stay Connected

- YouTube: [Learn With DevOps Engineer](https://www.youtube.com/@learnwithdevopsengineer)
- Instagram: [@learnwithdevopsengineer](https://www.instagram.com/learnwithdevopsengineer/)
- Newsletter: [Beehiiv updates](https://learnwithdevopsengineer.beehiiv.com/)
- Topmate: [Book a session](https://topmate.io/learnwithdevopsengineer) 

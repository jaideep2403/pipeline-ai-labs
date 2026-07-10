# Episode 1: Pipeline Foundation

This episode starts the series with the simplest possible GitHub Actions workflow.

## What this episode teaches

- What a workflow is
- How push triggers work
- What jobs and steps are
- How to verify a runner is actually executing commands

## What the pipeline does

The workflow in [`.github/workflows/pipeline.yml`](../.github/workflows/pipeline.yml) runs on pushes to `main` and `dev`.

It performs three simple actions:

```yaml
- Checkout Code
- List Files
- Echo Message
```

That is intentional. The first episode is about understanding the pipeline shape before adding build, test, or deployment complexity.

## Pipeline Explanation

- The push trigger starts the workflow when code lands on the watched branches.
- The checkout step gives the runner access to the repository files.
- The validation step proves the workflow executed commands in the repo workspace.
- The build step shows how later episodes can turn the same code into a container artifact.
- The cleanup step keeps the runner ready for the next run.

## Walkthrough

1. A push happens on `main` or `dev`.
2. GitHub Actions starts the workflow on `ubuntu-latest`.
3. The repository is checked out.
4. The workflow lists files so you can confirm the workspace is available.
5. The workflow prints a message to prove the runner is executing commands.

## Why this matters

Many beginners assume the pipeline is "broken" when really the job is just too small to do meaningful work yet.

This episode shows the foundation:

- the trigger works
- the runner works
- the job executes steps in order

## Practice exercises

1. Add a fourth step that prints the current date.
2. Change the image name or build tag to your own naming convention.
3. Restrict the workflow to only run on `main` and observe the difference.
4. Add a step that prints the GitHub event name.
5. Add a step that fails on purpose and inspect the log output.
6. Change the workflow name and see how it appears in GitHub Actions.

For scenario-based interview practice, see [INTERVIEW-QA.md](./INTERVIEW-QA.md).

## Key takeaway

Episode 1 is about getting the CI/CD skeleton in place. Later episodes build on this foundation.

## Stay Connected

- YouTube: [Learn With DevOps Engineer](https://www.youtube.com/@learnwithdevopsengineer)
- Instagram: [@learnwithdevopsengineer](https://www.instagram.com/learnwithdevopsengineer/)
- Newsletter: [Beehiiv updates](https://learnwithdevopsengineer.beehiiv.com/)
- Topmate: [Book a session](https://topmate.io/learnwithdevopsengineer)

# Episode 3 Scenario Questions and Answers

## 1. A secret appears in the CI logs. What should you do first?

Treat it as compromised, stop using it, and rotate it immediately.

## 2. You need an API key in the pipeline. Where should it live instead of plain text?

Store it in GitHub Secrets or a secret manager and inject it only into the step or container that needs it.

## 3. A workflow writes a sensitive value into `$GITHUB_ENV`. What risk does that create?

It makes the value available to later steps, which increases the chance that it will be logged or reused unsafely.

## 4. `docker logs` shows more than you expected. Why is that dangerous?

Application logs can expose environment variables, tokens, or other sensitive data if the app prints them.

## 5. How do you apply least privilege to this pipeline?

Give the workflow only the permissions and secrets it truly needs, and avoid broad access that could leak or be abused.

## 6. A secret is masked in logs, but the job still has broad access. Is that enough?

No. Masking reduces accidental exposure, but least privilege still matters because the secret can be misused even if it is not printed.

## 7. Someone says, "it is only a demo secret." How do you respond?

Treat demo secrets with the same discipline as real ones, because the habit you build in demos is the habit you carry into production.

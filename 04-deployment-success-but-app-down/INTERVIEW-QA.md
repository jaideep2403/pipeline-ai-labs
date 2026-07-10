# Episode 4 Scenario Questions and Answers

## 1. The deployment job is green, but the app is still down. What do you check next?

Check the actual HTTP endpoint, not just the deployment status. A green job does not guarantee the app is reachable.

## 2. A container starts, but `curl -f` fails. What does that tell you?

The process may be running, but the application is not responding correctly to requests.

## 3. Why is a fixed sleep after deploy a weak check?

It only waits for time to pass. It does not verify that the app is healthy or serving traffic.

## 4. What would you add so the pipeline fails for the right reason?

Add a real health check against the app endpoint and keep cleanup in place so later runs are not affected.

## 5. How do you explain the difference between container success and user-visible success?

A container can start successfully while the application still fails from the user’s point of view. User-visible success requires a real request to work.

## 6. The endpoint returns `200`, but the content is wrong. What does that tell you?

It means the network path works, but the application logic may still be broken, so you need a stronger validation than status code alone.

## 7. Why should cleanup happen even when the deployment fails?

Because stale containers can hide the next failure or create false positives in later runs.

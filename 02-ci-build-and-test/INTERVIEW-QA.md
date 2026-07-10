# Episode 2 Scenario Questions and Answers

## 1. The image builds successfully, but the app still fails health checks. What is the likely issue?

The build step only proves the image can be created. You still need to check the runtime behavior, container port, and application endpoint.

## 2. A `sleep` step passes, but the endpoint is still broken. Why is that not enough?

Sleeping only waits for time to pass. It does not prove that the application started correctly or is serving requests.

## 3. `curl -f` fails during the test stage. What should that tell you?

The pipeline should fail because the app is not responding successfully. That is exactly what the health check is supposed to catch.

## 4. The container starts on the wrong port. Which parts of the workflow need attention?

Check the app port, the Docker run mapping, and the health check URL so the pipeline is testing the same port the app actually uses.

## 5. A teammate says the job is green, so the app must be fine. How do you respond?

Explain that CI is only as good as its checks. A green build means the steps ran, not automatically that the app behavior is correct.

## 6. The container starts and answers on the root path, but the health check still fails. What should you compare?

Compare the health URL, container port mapping, and the actual route the app exposes so you can spot a mismatch between runtime and test.

## 7. The workflow passes on one machine but fails on another. What does that usually mean?

That usually points to an environment difference, such as missing dependencies, port conflicts, or a different image/build cache state.

# Episode 6 Scenario Questions and Answers

## 1. `curl http://localhost:30007` fails after a successful deploy. What do you gather before asking AI?

Check the Service, pod status, and endpoint mapping so you can give AI the real state of the system.

## 2. AI gives a generic answer. What extra context would make the diagnosis better?

Include the exact command, the Service type, the port mapping, and any relevant pod or service output.

## 3. The app may be healthy, but the host still cannot reach it. How do you tell the difference?

If the pod is running and the app responds inside the cluster but host access fails, the problem is likely networking rather than the app itself.

## 4. Which Kubernetes commands help confirm whether traffic should work?

Use `kubectl get pods`, `kubectl get svc`, `kubectl describe svc prod-service`, and `kubectl get endpoints prod-service`.

## 5. Why is AI useful here, but not enough on its own?

AI helps speed up reasoning, but it still depends on real signals from logs, manifests, and cluster state.

## 6. The app works inside the cluster but not from the host. What is your best next hypothesis?

The host-to-kind networking path is likely broken or incomplete, so the Service may be fine while the external access layer is not.

## 7. What should you never leave out when asking AI to debug this kind of issue?

The exact command, the relevant `kubectl` output, and the environment details, because vague prompts lead to vague answers.

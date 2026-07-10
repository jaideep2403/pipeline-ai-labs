# Episode 5 Scenario Questions and Answers

## 1. The Deployment is applied, but the app is not reachable from your laptop. What do you inspect first?

Check the Service type, the node port, and whether the pod is actually running before changing the app code.

## 2. The pod is healthy, but traffic never reaches it. How do `port` and `targetPort` help you debug?

`port` is what the Service exposes, while `targetPort` must match the port the container listens on. A mismatch breaks traffic flow.

## 3. A local kind cluster cannot use your new image. What step is missing?

The image must be loaded into kind so the cluster can see it without pulling from a registry.

## 4. You want to scale the app from one replica to two. Which Kubernetes object do you change?

Update the Deployment, because it controls the number of pod replicas.

## 5. A teammate asks why NodePort was chosen here. How do you answer?

NodePort makes the app reachable from outside the cluster in a local demo, which is useful when you need a simple access path.

## 6. The pod is running but the Service has no endpoints. What is the likely issue?

The Service selector probably does not match the pod labels, so Kubernetes has nothing to route traffic to.

## 7. Why is it better to check the rollout before testing the endpoint?

Because a Service can exist before the Deployment is ready, and rollout status tells you when Kubernetes has actually finished placing the pods.

# Episode 5: Kubernetes Deployment

This episode moves the app from a single container to Kubernetes.

## What you learn

- What a Kubernetes Deployment does
- What a Service does
- Why `NodePort` matters in local clusters
- Why `kind load docker-image` is needed for local development

## What the workflow does

The workflow in [`.github/workflows/deploy-kubernetes.yaml`](../.github/workflows/deploy-kubernetes.yaml) does the following:

1. Checks out the code
2. Builds the Docker image
3. Loads the image into the kind cluster
4. Applies the Deployment and Service manifests
5. Waits for the rollout to finish

## Pipeline Explanation

- The checkout step gets the Kubernetes manifests and app source into the job workspace.
- The image build step creates the container artifact that Kubernetes will run.
- The kind load step makes the locally built image visible to the cluster.
- The manifest apply step declares the desired Kubernetes state for the app and Service.
- The rollout step waits until Kubernetes confirms the Deployment has finished converging.
- The service check step confirms traffic can actually reach the app through the NodePort.

## Why this episode matters

This is the first Kubernetes episode in the series.

It introduces the core objects:

- Deployment
- Pod template
- Service
- NodePort

## Walkthrough

The Deployment in `k8s/deployment.yaml` creates one replica of `prod-app`.

The Service in `k8s/service.yaml` exposes the app:

- service port: `80`
- targetPort: `5000`
- nodePort: `30007`

The app itself still listens on `0.0.0.0:5000`.

## Why `kind load docker-image` is necessary

When you build a Docker image locally, the kind cluster cannot use it automatically unless you load it into the cluster.

That step makes the local image available to Kubernetes without pushing it to a registry.

## Practice exercises

1. Scale the Deployment from 1 replica to 2.
2. Change the Service port and update the manifest.
3. Add a readiness probe to the Deployment.
4. Run `kubectl get pods`, `kubectl get svc`, and `kubectl describe svc prod-service`.
5. Break the Service selector and fix it using `kubectl describe svc`.
6. Change the `nodePort` and verify the external access path changes.

For scenario-based interview practice, see [INTERVIEW-QA.md](./INTERVIEW-QA.md).

## Key takeaway

Episode 5 introduces Kubernetes deployment and service basics, setting up the final debugging story in episode 6.

## Stay Connected

- YouTube: [Learn With DevOps Engineer](https://www.youtube.com/@learnwithdevopsengineer)
- Instagram: [@learnwithdevopsengineer](https://www.instagram.com/learnwithdevopsengineer/)
- Newsletter: [Beehiiv updates](https://learnwithdevopsengineer.beehiiv.com/)
- Topmate: [Book a session](https://topmate.io/learnwithdevopsengineer)

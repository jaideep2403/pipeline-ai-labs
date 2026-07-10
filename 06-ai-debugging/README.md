# Episode 6: AI Debugging the Kubernetes Curl Failure

This episode closes the series by showing how AI can help diagnose a Kubernetes networking issue.

## What you learn

- How to validate whether the app is actually reachable
- How to describe a Kubernetes problem to AI clearly
- How to separate app issues from networking issues
- Why local kind networking can make NodePort testing fail

## What was broken

The Kubernetes Service was a `NodePort` service on port `30007`, but the app was not reachable from the VM host.

That meant the pipeline could succeed while this command still failed:

```bash
curl http://localhost:30007
```

## What the episode demonstrates

1. Reproduce the failure with `curl`
2. Inspect the Deployment and Service
3. Ask AI with the exact setup
4. Confirm the root cause
5. Fix the networking
6. Test the endpoint again

## Pipeline Explanation

- The cluster setup step creates the kind environment with the correct port mapping.
- The image build and load steps place the app image inside the cluster boundary.
- The manifest apply step deploys the app and Service into Kubernetes.
- The rollout step ensures the Deployment stabilizes before access testing begins.
- The reachability step checks the NodePort from the host and confirms whether the issue is networking or application-related.
- The cleanup step tears down the kind cluster so the next run starts fresh.

## Files in this episode

- `app/app.py` - Flask app
- `Dockerfile` - container build
- `k8s/deployment.yaml` - Kubernetes deployment
- `k8s/service.yaml` - NodePort service
- `.github/workflows/deploy-kubernetes-ep6.yaml` - CI/CD workflow for episode 6

## Local demo flow

The live recording follows this idea:

```bash
curl http://localhost:30007
kubectl get pods
kubectl get svc
kubectl describe svc prod-service
kind create cluster --name k8s-deployment
kubectl apply -f k8s/deployment.yaml
kubectl apply -f k8s/service.yaml
kubectl rollout status deployment/prod-app
curl http://localhost:30007
```

The key lesson is that a successful Deployment does not always mean the app is reachable from the host.

## Practice exercises

1. Change the Service `nodePort` and see how it affects access.
2. Add `kubectl get endpoints prod-service` to your debugging checklist.
3. Write a shorter AI prompt that still gives enough context.
4. Explain the failure without mentioning the app code at all.
5. Compare the result of `curl` inside the cluster and from the host.
6. Ask AI to explain the problem using only the pod and Service output.

For scenario-based interview practice, see [INTERVIEW-QA.md](./INTERVIEW-QA.md).

## Key takeaway

Episode 6 shows that AI is most useful when you give it the right context and use it to confirm a real hypothesis.

## Stay Connected

- YouTube: [Learn With DevOps Engineer](https://www.youtube.com/@learnwithdevopsengineer)
- Instagram: [@learnwithdevopsengineer](https://www.instagram.com/learnwithdevopsengineer/)
- Newsletter: [Beehiiv updates](https://learnwithdevopsengineer.beehiiv.com/)
- Topmate: [Book a session](https://topmate.io/learnwithdevopsengineer)

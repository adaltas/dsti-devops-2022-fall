
## Pushing an image

- Install minikube registry addon
- Push the application you build in the previous lab on this registry

## Deploy your application

- Create a deployment (in .yaml) using this image
  - The web app should expose a NodePort
  - Add ConfigMap and/or Secret as you see fit
  - deploy with a replica set to 1
  - 
- Create a Github repository storing this .yaml file(s)
  - Push

## Argo CD

Install ArgoCD

```
kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
# ArgoCD is now installed on your cluster !

# The admin password can be found here:
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d && echo

# The Web UI and CLI are exposed by the service argocd-server, let's access it:
kubectl patch svc argocd-server -n argocd -p '{"spec": {"type": "LoadBalancer"}}'
# Or if no LoadBalancer provider is available
kubectl port-forward svc/argocd-server -n argocd 8080:443
# Or you can access the service using a NodePort
kubectl patch svc argocd-server -n argocd -p '{"spec": {"type": "NodePort"}}'
```

## Configure ArgoCD

Delete your deployments.

Using the UI, create a deployment using the GitHub OPS repository you created

Enable auto synchronisation



# PoC: Argo CD on k3d with Image Upload API Test

##  Prerequisites

- Docker installed and running
- `curl`, `kubectl`, and `wget` available

---

##  Step 1: Install k3d

```bash
curl -s https://raw.githubusercontent.com/k3d-io/k3d/main/install.sh | bash
```

---

##  Step 2: Create a New k3d Cluster

```bash
k3d cluster create argo
```


---

##  Step 3: Install Argo CD

Create the `argocd` namespace and install Argo CD:

```bash
kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
```

once all pods are up and running:

```bash
kubectl get pods -n argocd
```

---

## Step 4: Access ArgoCD GUI

Forward the Argo CD API server

```bash
kubectl port-forward svc/argocd-server -n argocd 8080:443
```

Then open in your browser:

```
https://localhost:8080
```

> By default ArgoCD works via HTTPS.
> Accept the self-signed certificate warning.

---

## Step 5: Retrieve Admin Password

```bash
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d; echo
```

Use:
- **Username**: `admin`
- **Password**: (output from the command above)

---

## Step 6: Forward API Service Port

> Replace the service name if needed.

```bash
kubectl port-forward -n argocd svc/envoy-argocd-eg-bcf9e388 8088:80
```
Make sure to check correct service API name.
This makes the sample service/API available on:

```
http://localhost:8088
```

---

## Step 7: Upload a Test Image via API

Download an image:

```bash
wget -O /tmp/logo.jpg https://yourlink.com/logo.jpg
```

Send the image to the API:

```bash
curl -H "Host: demo.example.com" -F 'image=@/tmp/logo.jpg' http://localhost:8088/api
```

---

## Cleanup (Optional)

To remove the entire k3d cluster:

```bash
k3d cluster stop argo && k3d cluster delete argo
```

---

## Summary

- A local k3d Kubernetes cluster created
- ArgoCD deployed and accessible via GUI
- Tested with 


[Watch the demo video](https://drive.google.com/file/d/12u2bqgVWWuNZbmMs6GjlxGlYx670b5Gn/view?usp=sharing)
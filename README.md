# Lab 2 — hello-app on Kubernetes

Your copy of this repository is your submission. The lab sheet is on the course site; this file is where you record what you did.

What's here:

| File | What it is |
|---|---|
| `src/`, `index.html` | a small React page that shows which Pod answered |
| `nginx.conf` | serves the page, and answers `/whoami` with the Pod name |
| `Dockerfile` | builds the page, then serves it with nginx on port 80 |

You don't change any of these. You add `hello-app.yaml` and fill in the sections below.

## Before you push, check

- [ ] `hello-app.yaml` is in the root of this repository
- [ ] `screenshot.png` is in the root of this repository
- [ ] every section below is filled in

---

## 1. My image

Docker Hub image I deployed (for example `ravi123/hello-app:v1`):

```
nidhie/hello-app:v1
```

## 2. Pods across nodes

Output of `kubectl get pods -o wide` after you applied `hello-app.yaml`:

```
NAME                         READY   STATUS    RESTARTS      AGE   IP            NODE              NOMINATED NODE   READINESS GATES
hello-app-86c99ddf7d-7q75z   1/1     Running   0             79s   10.244.2.6    desktop-worker2   <none>           <none>
hello-app-86c99ddf7d-w5498   1/1     Running   0             78s   10.244.1.10   desktop-worker    <none>           <none>
hello-app-86c99ddf7d-z4xjx   1/1     Running   0             79s   10.244.1.9    desktop-worker    <none>           <none>
web-7887448d46-rzvwz         1/1     Running   2 (34m ago)   16d   10.244.2.2    desktop-worker2   <none>           <none>
```

## 3. The Service and its endpoints

Output of `kubectl get service hello-app` and `kubectl get endpointslices -l kubernetes.io/service-name=hello-app`:

```
NAME        TYPE           CLUSTER-IP    EXTERNAL-IP   PORT(S)          AGE
hello-app   LoadBalancer   10.96.93.37   172.18.0.7    8080:30178/TCP   15m

get endpointslices -l kubernetes.io/service-name=hello-app
NAME              ADDRESSTYPE   PORTS   ENDPOINTS                           AGE
hello-app-cn4dc   IPv4          80      10.244.1.9,10.244.2.6,10.244.1.10   16m
```

## 4. Browser

Add `screenshot.png`: the page at `http://localhost:8080` with at least two Pods in the "Answers so far" table.

## 5. The four traps

For each trap, write what you saw and why it happened, in two or three lines of your own words.

**Trap 1 — the local image.**

**Trap 2 — the selector typo.**

**Trap 3 — the wrong targetPort.**

**Trap 4 — the EXTERNAL-IP address.**

## 6. Your YAML vs the generated YAML

Name two fields in the `--dry-run=client -o yaml` output that were not in your file. Why does your file still work without them?

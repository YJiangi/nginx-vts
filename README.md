demo_yaml:
```bash
----
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx
spec:
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
      annotations:
        prometheus.io/scrape: "true"
        prometheus.io/path: "/status/format/prometheus"
        prometheus.io/port: "80"
    spec:
      containers:
        - name: nginx
          image: nginx-vts:lts
          resources:
            requests:
              cpu: 100m
              memory: 100Mi
          ports:
            - containerPort: 80
```
---------
Build command:
```bash
docker buildx build --progress=plain --no-cache --build-arg ENABLED_MODULES="cachepurge"  --platform=linux/arm64,linux/amd64 -t nginx-vts:lts . --push
```

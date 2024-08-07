####### 1. Please refer to the official [website](https://github.com/nginxinc/docker-nginx/blob/master/modules/README.md)


###### 2. demo_yaml:
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
###### 3. Build command：
```bash
Multi-schema compilation image:
docker buildx build --progress=plain --no-cache --build-arg ENABLED_MODULES="cachepurge"  --platform=linux/arm64,linux/amd64 -t nginx-vts:lts . --push
```
```bash
Compile image:
docker  build --progress=plain --no-cache --build-arg ENABLED_MODULES="cachepurge"  -t nginx-vts:lts . 
```


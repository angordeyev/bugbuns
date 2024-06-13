# Troubleshooting

## A troubleshooting client container

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: debug-client
spec:
  containers:
  - name: ubuntu
    image: ubuntu
    command: ["sleep"]
    args: ["infinity"]
  hostNetwork: true
  dnsPolicy: Default
```

```shell
kubectl exec --stdin --tty debug-client -- /bin/bash
```

## A simplest http server

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: debug-server-http
spec:
  containers:
    - name: echo-server
      image: ealen/echo-server
      env:
        - name: PORT
          value: "8000"
```

```shell
kubectl port-forward pods/debug-server-http 8000:8000
```

## SSH into a container

```shell
kubectl apply -f https://k8s.io/examples/application/shell-demo.yaml
```

```shell
kubectl exec --stdin --tty shell-demo -- /bin/bash
```

## Test a connection to a DB

```shell
kubectl apply -f https://k8s.io/examples/application/shell-demo.yaml
```

```shell
kubectl exec --stdin --tty shell-demo -- /bin/b`ash
```

```shell
apt-get update
apt-get install -y postgresql-client
````

## Shell Demo

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: shell-demo
spec:
  volumes:
  - name: shared-data
    emptyDir: {}
  containers:
  - name: nginx
    image: nginx
    volumeMounts:
    - name: shared-data
      mountPath: /usr/share/nginx/html
  hostNetwork: true
  dnsPolicy: Default
```

## Resources

* [100 Kubernetes Diagnostics Commands with Kubectl](https://medium.com/stream-zero/100-kubernetes-diagnostics-commands-with-kubectl-a0cb7f9f0d6e)

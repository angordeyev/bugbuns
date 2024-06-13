# Deployment

## Getting Started

Start minikube:

```shell
minikube start
```

Create a simple deployment:

```shell
# kubectl create deployment echo-server --image=hashicorp/http-echo
kubectl create deployment hello-minikube --image=kicbase/echo-server:1.0
```

List deployments:

```shell
kubectl get deployments
```

```output
NAME             READY   UP-TO-DATE   AVAILABLE   AGE
echo-server       1/1     1            1           10s
```

## A simple deployment

```shell
kubectl create deployment echo-server --image=hashicorp/http-echo
```

```shell
kubectl get deployments
```

Create `pod.yml`:

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: first-pod
  labels:
    project: qsk-book
spec:
  containers:
    - name: web
      image: nigelpoulton/qsk-book:1.0
      ports:
        - containerPort: 8080
```

## Working with Deployments

Create a deployment:

```shell
kubectl create deployment hello-minikube --image=kicbase/echo-server:1.0
```

Get deployments:

```shell
kubectl get deployments
```

Delete a deployment:

```shell
kubectl delete deployment hello-minikube
```

## Resources

* [Get Started! minikube Documentation.](https://minikube.sigs.k8s.io/docs/start/)
* [Начало работы в Kubernetes с помощью Minikube](https://habr.com/ru/companies/flant/articles/333470/)

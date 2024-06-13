# minikube

## Commands

Open dashboard:

```shell
minikube dashboard
```

SSH to the minikube image:

```shell
minikube ssh
```

## Localhost

Use `host.minikube.internal` to access locahost.

### Test local DB connection

Install Postgres client:

```shell
sudo apt-get update
sudo apt-get install -y postgresql-client
```

## Resources

* [Proxying services into minikube. Vagmi Mudumbai.](https://blog.tarkalabs.com/proxying-services-into-minikube-8355db0065fd)
* [Connect to local database from inside minikube cluster](https://devpress.csdn.net/k8s/62fd61fcc677032930803744.html)

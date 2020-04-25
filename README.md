# k8s deployment for [locust.io](https://locust.io/) framework

master/slave deployment files to deploy locust.io framework on Kubernetes.

## Information

locust.io is a framework for testing your site in high loads. 

If you run more than one slave of Locust on the same computer or the same internet connection, you cannot get the correct results. With these files, you can run unlimited locust.io slave pods on DigitalOcean or Google Cloud.

Deployment files use [locustio/locust](https://hub.docker.com/r/locustio/locust) docker image to build containers. This ensures locust.io is always up to date when pods are created.

master-deployment.yaml includes a load balancer service for connecting externally to locust master web GUI.

## Usage

First of all, a [locust script file](https://docs.locust.io/en/stable/writing-a-locustfile.html) that is reachable from the web.

In master-deployment.yaml you should change the environment variables ##TARGET_URL## and ##LOCUST_SCRIPT_URL## with yours.

and run

```bash
kubectl apply -f master-deployment.yaml
```

and get master pod IP with:

```bash
kubectl get pods -o wide
```

edit slave-deployment.yaml, change replicas variable to how many slave pods you need. Also change ##TARGET_URL##, ##LOCUST_MASTER_HOST_IP## and ##LOCUST_SCRIPT_URL##

and apply slave-deployment.yaml file.

```bash
kubectl apply -f slave-deployment.yaml
```

get the load balancer's external IP to reach GUI.

```bash
kubectl get services
```

## License
[MIT](https://choosealicense.com/licenses/mit/)
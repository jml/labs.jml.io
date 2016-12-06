# labs.jml.io

```console
$ export PROJECT_ID=holborn-1248
```

## Accessing the cluster

```console
$ gcloud container clusters get-credentials labs --zone europe-west1-b --project $PROJECT_ID
```

## Deployment

Assumes `gcloud` and `kubectl`.

```console
$ cd frontend
$ docker build -t gcr.io/${PROJECT_ID}/frontend:v1 .
$ cd ..
$ kubectl create -f k8s/frontend-dep.yaml
$ kubectl create -f k8s/frontend-svc.yaml
```

Get external IP address with:

```console
$ kubectl get svc -o json frontend | jq -r .status.loadBalancer.ingress[].ip
130.211.97.232
```

(this might take some time after creating the service).

Update Route53 on [AWS console](https://mumak.signin.aws.amazon.com/console)
to point `labs.jml.io` at the IP.

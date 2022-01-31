# Apollo

The Apollo demo optimization application

## Simple deployment

```sh
kubectl create ns apollo
kubectl kustomize envoy/ | kubectl apply -f - -n apollo
```

## Istio metrics

```sh
# istioctl install ## if Istio isn't already installed
kubectl create ns apollo
kubectl label namespace apollo istio-injection=enabled --overwrite
kubectl kustomize base/ | kubectl apply -f - -n apollo
```

Then configure the opsani-manifest with:

```sh
NAMESPACE = apollo
DEPLOYMENT = apollo
CONTAINER = apollo
SERVICE = apollo
```

And then to start optimization with opsani-dev:
```sh
kubectl apply -f opsani-manifest.yaml -n apollo
```

## Cleanup

```sh
kubectl delete ns apollo
```

## Description

Apollo is a simple application that executes an md5 hash function to generate some
actual CPU work against at the compute level.

K6 is the loadgenerator that makes requests against the apollo application. Currently it is configured for static load.

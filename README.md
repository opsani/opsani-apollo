# Apollo

The Apollo demo optimization application

## Configure Metrics source

Select one of the following (mutually exclusive) configurations to provide metrics
to the Prometheus sidecar of ServoX

### Istio metrics (Required for Dashbase)

```sh
# brew install istioctl ## if istioctl isn't already installed
# istioctl install ## if Istio isn't already installed
kubectl create ns apollo
kubectl label namespace apollo istio-injection=enabled --overwrite
kubectl kustomize kubernetes/ | kubectl apply -f - -n apollo
```

Once Istio is installed, any prometheus server configured to scrape pods should
automatically scrape Istio generated metrics as well due to the default configuration
of [metrics merging](https://istio.io/latest/docs/ops/integrations/prometheus/#option-1-metrics-merging)

### Envoy sidecar metrics (Legacy solution, used in non-Istio environments)

```sh
kubectl create ns apollo
kubectl kustomize envoy/ | kubectl apply -f - -n apollo
```

## Opsani Manifests Configuration

Then configure the opsani-manifest with:

```sh
NAMESPACE = apollo
DEPLOYMENT = apollo
CONTAINER = apollo
SERVICE = apollo
```

And then to start optimization with opsani-dev:
```sh
kubectl apply -f servo_install/opsani-manifests.yaml -n apollo
```

## Cleanup

```sh
kubectl delete ns apollo
# kubectl delete ns istio-system ## if istio was installed, it will prevent nodes from draining which will block teardown of temporary test clusters
```

## Description

Apollo is a simple application that executes an md5 hash function to generate some
actual CPU work against at the compute level.

K6 is the loadgenerator that makes requests against the apollo application. Currently it is configured for static load.

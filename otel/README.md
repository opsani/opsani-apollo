# Kustomize the Bank-of-Anthos application for OpenTelemetry instrumentation

## Deployment

The otel-patch changes the container start command to add the requred OpenTelemetry attributes.

## OpenTelemetry Instrumentation

The `otel.yaml` is a OpenTelemetry Instrumentation custom resource that sets up an OpenTelemetry collector

## Application

```sh
kubectl kustomize  -k otel/
```


https://opentelemetry.io/docs/kubernetes/operator/automatic/


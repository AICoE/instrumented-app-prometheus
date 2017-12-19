# Prometheus and the Instrumented App

## Installing Prometheus

Prometheus app template is based off the 3.6.1 version of origin

```
NAMESPACE=urandom
oc new-app -f ./prometheus.yaml -p NAMESPACE=$NAMESPACE
```

## Delete Prometheus
```
oc delete all -l app=prometheus
```

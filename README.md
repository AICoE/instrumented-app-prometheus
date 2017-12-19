# Prometheus and the Instrumented App

## Installing

Prometheus app template is based off the 3.6.1 version of origin

```
NAMESPACE=urandom
oc new-app -f ./prometheus.yaml -p NAMESPACE=$NAMESPACE
oc new-app -f ./instrumented-app.yaml
```

## Delete
```
oc delete all,sa,secrets,svc,cm -l app=prometheus
oc delete all -l app=instrumented-app
```

# Prometheus and the Instrumented App

## Installing Prometheus

Prometheus app template is based off the 3.6.1 version of origin

```
NAMESPACE=urandom
oc new-app -f ./prometheus.yaml -p NAMESPACE=$NAMESPACE
```

label for easy deletion

```
oc label svc/prometheus app=prometheus
oc label configmap/prometheus app=prometheus
oc label secret/prometheus-proxy app=prometheus
oc label secret/prometheus-tls app=prometheus
oc label sa/prometheus app=prometheus
oc label routes/prometheus app=prometheus
```

## Delete Prometheus
```
oc delete sa,route,svc,secret,deployment,configmap -l app=prometheus
```

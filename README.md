# Prometheus and the Instrumented App

## Installing Prometheus

Prometheus app template is based off the 3.6.1 version of origin

```
NAMESPACE=urandom
oc new-app -f ./prometheus.yaml -p NAMESPACE=$NAMESPACE
oc expose svc/prometheus --name=prometheus --hostname=prometheus --tls=reencrypt --port=prometheus -l app=prometheus -n $NAMESPACE
```

label for easy deletion

```
NAMESPACE=urandom
oc label svc/prometheus app=prometheus -n $NAMESPACE
oc label configmap/prometheus app=prometheus -n $NAMESPACE
oc label secret/prometheus-proxy app=prometheus -n $NAMESPACE
oc label secret/prometheus-tls app=prometheus -n $NAMESPACE
oc label sa/prometheus app=prometheus -n $NAMESPACE
oc label routes/prometheus app=prometheus -n $NAMESPACE
```

## Delete Prometheus
```
NAMESPACE=urandom
oc delete sa,route,svc,secret,deployment,configmap -l app=prometheus -n $NAMESPACE
```

# Prometheus and the Instrumented App

## Installing Prometheus

Prometheus app template is based off the 3.6.1 version of origin

```
oc new-app -f ./prometheus.yaml --labels='app=prometheus' -p NAMESPACE=myproject
```

### Delete prometheus
```
oc delete all,sa,secrets,svc,cm -l app=prometheus
```

## Installing the instrumented app

### via images hosted on docker hub

```
oc new-app -f ./instrumented-app.yaml
```


### via s2i

#### build s2i-go images on openshift

```
oc new-build --strategy=docker --to=s2i-go --context-dir=1.8 --labels='build=s2i' https://github.com/durandom/s2i-go
```

#### add a s2i build

```
oc new-app s2i-go~https://github.com/durandom/instrumented-app.git --labels='app=instrumented-app'
oc expose service instrumented-app
```

Go to 'Builds -> instrumented-app -> Configuration' and add the GitHub Webhook URL to your repo to trigger new builds.

#### create another binary build for local testing

this removes the need to push to github

```
oc new-build --binary s2i-go --name=instrumented-app-dev --to=instrumented-app-dev
```

Upload the current dir for building and create the application

```
oc start-build instrumented-app-dev --from-dir=~/src/instrumented-app --follow 
oc new-app instrumented-app-dev
oc expose service instrumented-app-dev
```

### Delete the instrumented app

```
oc delete all -l app=instrumented-app
```


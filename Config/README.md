### ConfigMaps provides a way to store configuratiob infornation and provide it to containers


- configmaps can be accessed in a pod either through a environment or through voulme

> Create a config map through yml. The filename will be used as the key for the configuration data


```
$ kubectl create -f <NameofConfigMapyaml>
```

> Create a configMap from a file

```
$ kubectl create cm <ConfigName> --from-file=<fileName>
```

> Create a configMap from an env file
```
$ kubectl create cm < configName> --from-env-file=<fileName>
```

1. Using a k8s ConfigMap manifest:  `kubectl create -f settings.configmap.yml`
2. Load settings from a file: `kubectl create cm app-settings --from-file=settings.properties`. Will add file name as key into ConfigMap data. Will NOT add quotes around non-string values.
3. Load settings from an env file: `kubectl create cm app-settings --from-env-file=settings.properties`. Will NOT add file name as key into ConfigMap data. Will add quotes around non-string values.
4. Define settings in kubectl command: `kubectl create cm app-settings --from-literal=apiUurl=https://my-api  --from-literal=otherKey=otherValue --from-literal=count=50`. Will add quotes around non-string values.

## To Run Node Server and Access ConfigMap Data

Demo of accessing ConfigMap data in a Pod container through environment variables and direct settings.

1. Delete any ConfigMaps you added into k8s above via:

`kubectl delete cm app-settings`

2. Build image: `docker build -t node-configmap .`
3. Create ConfigMap: 

`kubectl create cm app-settings --from-env-file=settings.config`

4. Create deployment: 

`kubectl apply -f node.deployment.yml`

5. Port forward the Pod: 

`kubectl port-forward [pod-name] 9000`

6. Visit `http://localhost:9000` and view the ConfigMap settings output






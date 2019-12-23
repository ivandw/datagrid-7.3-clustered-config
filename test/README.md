env variables to add to DC (not added to template, if config is not set, dc crashes):

- name: JAVA_OPTS_APPEND
  ​    value: "-javaagent:/opt/datagrid/jmx-prometheus.jar=9404:/opt/datagrid/prometheus/config.yaml"

add this to expose 9404 svc (already done at template):

- ```yaml
  - containerPort: 8778
         name: jolokia
         protocol: TCP
  - containerPort: 9404
         name: prometheus
         protocol: TCP
  ```

  ​    

Create the ConfigMap with JMX Exporter config:



```bash
oc create configmap datagrid-jmx --from-file=config.yaml
```

add this to set jmx configmap as a volume:
 volumeMounts (or use the GUI):

```yaml
mountPath: /opt/datagrid/prometheus
name: prometheus-volume
         terminationGracePeriodSeconds: 60
         volumes:

name: prometheus-volume
configMap:
defaultMode: 420
name: datagrid-prometheus
```

 commands to push IS:

 Build the custom Data Grid image including JMX Exporter Prometheus(previous you have to download this repo, and enter test folder):

```bash
oc new-build . --name=datagrid72-prometheus --strategy=docker
```

lauch the build:

```bash
oc start-build datagrid71-prometheus --from-file=./Dockerfile
```



now use this custom image with prometheus agent to use s2i from the original img and upload openshift-clustered.xml from this repo (or yours). 



enjoy persistent datagrid with prometheus/grafana monitoring

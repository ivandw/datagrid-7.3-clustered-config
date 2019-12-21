# datagrid-7.1-clustered-config based on original application template for ocp https://github.com/jboss-openshift/application-templates/blob/master/docs/datagrid/datagrid71-postgresql-persistent.adoc

config file to s2i datagrid official img

1- create "datagrid-app-secret" containing certs .jceks andthe keystore needed for this template.
2- import template "template.yaml"

Create the app using Openshift web console (from catalog) or using `oc` CLI (replace credentials with yours) and replace your onw repo with custom openshift-clustered.xml.

```bash
oc new-app --template='template": "custom-datagrid71-persistent-template' \
--param=APPLICATION_NAME='datagrid-app' \
--param=SOURCE_REPOSITORY_URL='https://github.com/ivandw/datagrid-clustered-config' \
--param=USERNAME='admin' \
--param=PASSWORD='Data@grid1' \
--param=JAVA_OPTS_APPEND='-Dcustom_opts_mark=custom-dg-cluster -Xms512m -Xmx512m'
```

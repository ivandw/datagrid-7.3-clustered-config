# datagrid-7.1-clustered-custom-config 

Config file to s2i datagrid official img (see more: based on original application template for ocp https://github.com/jboss-openshift/application-templates/blob/master/docs/datagrid/datagrid71-postgresql-persistent.adoc)
and datagrid documentation: https://access.redhat.com/documentation/en-us/red_hat_data_grid/7.1/pdf/data_grid_for_openshift/Red_Hat_JBoss_Data_Grid-7.1-Data_Grid_for_OpenShift-en-US.pdf

1- create secret "datagrid-app-secret" containing certs .jceks andthe keystore needed for this template.

2- import template "template.yaml"

3- Create the app using Openshift web console (from catalog) or using `oc` CLI (replace credentials with yours) and replace your onw repo with custom openshift-clustered.xml.

```bash
oc new-app --template='template": "custom-datagrid71-persistent-template' \
--param=APPLICATION_NAME='datagrid-app' \
--param=SOURCE_REPOSITORY_URL='https://github.com/ivandw/datagrid-clustered-config' \
--param=USERNAME='admin' \
--param=PASSWORD='Data@grid1' \
--param=JAVA_OPTS_APPEND='-Dcustom_opts_mark=datagrid-app -Xms512m -Xmx512m'
```

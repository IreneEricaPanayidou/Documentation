# OpenShift CLI

Commands:

![](<../.gitbook/assets/image (2).png>)

* Set log level for more details: `oc --loglevel <logLevelNumber> get pod`
* See the logs of a pod: `oc logs <podName>`
* Execute command as user: `oc --as=<userName> get pods`
* Execute command as group: `oc --as-group=<groupName> get pods`
* View namespace: `oc get namespaces`
* Create debug shell for pod: `oc debug <podName>`
* Man of openshift resources: `oc explain pod/deployment etc`
* Format command output: `oc get pods-o=json (or yaml or wide etc)`
* View routes: `oc get routes`
* View projects: `oc get projects`
* View deployments: `oc get deployments`
* View pods: `oc get pods`
* View current project: `oc project`
* Connect to project: `oc project <projectName>`
* Create new project: `oc new-project <projectName>`
* View the status of the current project: `oc status`
* View configuration of a pod/deployment: `oc describe pod/<podName>` or `oc describe deployment/<deploymentName>`
* Edit a deployment configuration: `oc edit deploymentconfig/<deploymentConfigName>`
* Create a pod from a configuration: `oc create -f <configurationName>`
* Apply a configuration to a resource: `oc apply -f <configurationName>`
* Delete a resource: `oc delete pod/<podName> or oc delete deployment/<deploymentName>`
* Scale pods (autoscale): `oc autoscale deploymentconfig/<deploymentConfigName> --min=<minNumberOfPods> --max=<maxNumberOfPods>`

# openshift-hpa-demo

This repository was adapted from the upstream Kubernetes HPA test document at:
https://kubernetes.io/docs/tasks/run-application/horizontal-pod-autoscale-walkthrough/

1. Create the HPA example app.

```oc process -f https://raw.githubusercontent.com/georgegoh/openshift-hpa-demo/master/ocp-hpa-example.yaml | oc apply -f -```

2. Open a separate window to view the HPA

```oc get hpa hpa-app -w```

3. Create some load in another window:

```ROUTE=`oc get route hpa-app -o template --template={{.spec.host}}`; while true; do wget -q -O- ${ROUTE}; done```

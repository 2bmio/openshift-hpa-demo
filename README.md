# openshift-hpa-demo

This repository was adapted from the upstream Kubernetes HPA test document at:
https://kubernetes.io/docs/tasks/run-application/horizontal-pod-autoscale-walkthrough/

1. Create the HPA example app.

```oc process -f https://raw.githubusercontent.com/georgegoh/openshift-hpa-demo/master/ocp-hpa-example.yaml | oc apply -f -```

2. Open a separate window to view the HPA

```oc get hpa hpa-app -w```

3. Create some load in another window:

```ROUTE=`oc get route hpa-app -o template --template={{.spec.host}}`; while true; do wget -q -O- ${ROUTE}; done```

4. Watch the output in the window from (2) to observe load measurements changing and autoscaling taking place.

## Note

*metrics-server* is required for HPA to work.

To install *metrics-server*, run the following on bastion:

```ansible-playbook -i <INVENTORY_FILE> /usr/share/ansible/openshift-ansible/playbooks/metrics-server/config.yml -e openshift_metrics_server_install=true```

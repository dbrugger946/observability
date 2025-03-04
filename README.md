# observability

Demo Flows


COO Cluster Observability Operator

### Prometheus - Alertmanager -Thanos Querier

#### Python web server   – metrics displayed in Thanos in project  
https://developers.redhat.com/articles/2024/07/09/get-started-openshift-cluster-observability-operator#

project: coo-demo

curl http://$(oc get route coo-demo -o jsonpath='{.spec.host}')/

curl http://$(oc get route coo-demo -o jsonpath='{.spec.host}')/notfound



#### Node.js   – metrics displayed in OCP console panes  
https://developers.redhat.com/blog/2021/03/22/monitor-node-js-applications-on-red-hat-openshift-with-prometheus#

project: node-prom

https://kubebyexample.com/learning-paths/developing-nodejs/containerizing-application

//multi arch  
podman build --platform linux/amd64,linux/arm64 -t quay.io/dbrugger946/node-prom:latest -f Dockerfile .

podman push quay.io/dbrugger946/node-prom:latest

podman run -p 3000:3000 quay.io/dbrugger946/node-prom:latest

oc new-app  quay.io/dbrugger946/node-prom:latest --name=node-prom --as-deployment-config=false

(http route) oc expose service/node-prom OR
(https route) oc create route edge --service=node-prom
(if need be:) oc delete all -l app=node-prom

Apache benchmarking tool  (https://httpd.apache.org/docs/2.4/programs/ab.html)  
ab -n 10000 -c 100 https://node-prom-node-prom.apps.cluster-7f4n9.dynamic.redhatworkshops.io/api/greeting  

rate(http_request_duration_seconds_sum[5m])/rate(http_request_duration_seconds_count[5m])


### OpenTelemetry

OpenTelemetryCollector
project: otel-collector1

Tempo Install  
OpenShift Project :  tempo-monolithic

#### Quarkus
https://quarkus.io/guides/opentelemetry-tracing

project: quarkus-otel

mvn package -DskipTests  
podman build --platform linux/amd64,linux/arm64 -f src/main/docker/Dockerfile.jvm -t quay.io/dbrugger946/opentelemetry-quickstart-jvm:latest .

podman push quay.io/dbrugger946/opentelemetry-quickstart-jvm:latest

oc new-app  quay.io/dbrugger946/opentelemetry-quickstart-jvm:latest --name=quarkus-opentelemetry --as-deployment-config=false

(http route) oc expose service/quarkus-opentelemetry OR  
(https route) oc create route edge --service=quarkus-opentelemetry  
(if need be:) oc delete all -l app=quarkus-opentelemetry


curl https://quarkus-opentelemetry-quarkus-otel.apps.cluster-7f4n9.dynamic.redhatworkshops.io/hello



What’s New OCP 4.17

https://developers.redhat.com/blog/2024/11/12/whats-new-developers-openshift-417?sc_cid=RHCTG0240000432454#

https://docs.google.com/presentation/d/1rGlJApPS920iZmpQl0LALIj4ZzCUCv0VDQr6rkwcRiQ/edit#slide=id.g301f4e57cf2_8_2473

















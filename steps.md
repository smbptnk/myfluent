Fluent

https://www.youtube.com/watch?v=j76ozzIbuO8&t=1949s

https://docs.fluentbit.io/manual/pipeline/outputs/azure_blob

https://github.com/fluent/helm-charts/blob/main/charts/fluent-bit/values.yaml

https://github.com/kubesphere-sigs/fluent-operator-walkthrough#how-to-check-the-configuration-and-data
https://github.com/kubesphere-sigs/fluent-operator-walkthrough/blob/master/deploy-fluent-operator.sh

https://github.com/kubesphere-sigs/fluent-operator-walkthrough#using-fluent-bit-to-collect-k8s-application-logs-and-output-to-kafka-elasticsearch-and-loki
https://docs.fluentbit.io/manual/administration/configuring-fluent-bit
https://docs.fluentbit.io/manual/pipeline/outputs/azure_blob

Extras:

https://github.com/kubesphere-sigs/sample-admission-webhook/blob/master/deploy/sample-admission-webhook/templates/webhook.yaml
https://docs.fluentbit.io/manual/installation/kubernetes#installation

Steps:

> helm upgrade --install fluent-operator --create-namespace -n fluent https://github.com/fluent/fluent-operator/releases/download/v3.0.0/fluent-operator.tgz
> helm status  fluent-operator  -n  fluent
> helm get  fluent-operator  -n fluent

> kubectl  get all -n fluent
NAME                                   READY   STATUS    RESTARTS   AGE
pod/fluent-bit-shk4b                   1/1     Running   0          77s
pod/fluent-operator-67b97cf796-8x8jl   1/1     Running   0          2m28s

NAME                 TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)    AGE
service/fluent-bit   ClusterIP   10.104.204.59   <none>        2020/TCP   77s

NAME                        DESIRED   CURRENT   READY   UP-TO-DATE   AVAILABLE   NODE SELECTOR   AGE
daemonset.apps/fluent-bit   1         1         1       1            1           <none>          77s

NAME                              READY   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/fluent-operator   1/1     1            1           2m28s

NAME                                         DESIRED   CURRENT   READY   AGE
replicaset.apps/fluent-operator-67b97cf796   1         1         1       2m28s

> kubectl  get pods -n fluent
NAME                               READY   STATUS    RESTARTS   AGE
fluent-bit-shk4b                   1/1     Running   0          9m40s
fluent-operator-67b97cf796-8x8jl   1/1     Running   0          10m
> kubectl -n fluent get daemonset
NAME         DESIRED   CURRENT   READY   UP-TO-DATE   AVAILABLE   NODE SELECTOR   AGE
fluent-bit   1         1         1       1            1           <none>          17m
> kubectl -n fluent get fluentbit
NAME         AGE
fluent-bit   18m
> kubectl -n fluent get clusterfluentbitconfig
NAME                AGE
fluent-bit-config   19m
> kubectl -n fluent get clusterinput.fluentbit.fluent.io
NAME     AGE
docker   19m
tail     19m
> kubectl -n fluent get clusterfilter.fluentbit.fluent.io
NAME         AGE
containerd   20m
kubernetes   20m
systemd      20m
> kubectl -n fluent get clusteroutput.fluentbit.fluent.io
No resources found

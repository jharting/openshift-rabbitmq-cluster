# openshift-rabbitmq-cluster

Deploys a RabbitMQ cluster in Openshift.

[rabbitmq-peer-discovery-k8s](https://github.com/rabbitmq/rabbitmq-peer-discovery-k8s) is used for peer discovery. [StatefulSet](https://kubernetes.io/docs/concepts/workloads/controllers/statefulset/) is used to give RabbitMQ instances stable names and persistent volumes.

## Usage

Run

`oc create -f rabbitmq-cluster-template.yaml`

to install the template. Then, use the OpenShift UI to locate the template and use it to create a new RabbitMQ cluster.

Alternatively, run

`oc process -f rabbitmq-cluster-template.yaml NAMESPACE="$(oc project --short)" | oc create -f -`

to process the template and create a new cluster in the current project with the default settings. There are several [parameters that can be used to customize the cluster](/rabbitmq-cluster-template.yaml#L10).

Expected outcome:

```
Cluster status of node rabbit@rabbitmq-cluster-0.rabbitmq-cluster.delta.svc.cluster.local ...
[{nodes,
     [{disc,
          ['rabbit@rabbitmq-cluster-0.rabbitmq-cluster.delta.svc.cluster.local',
           'rabbit@rabbitmq-cluster-1.rabbitmq-cluster.delta.svc.cluster.local']}]},
 {running_nodes,
     ['rabbit@rabbitmq-cluster-1.rabbitmq-cluster.delta.svc.cluster.local',
      'rabbit@rabbitmq-cluster-0.rabbitmq-cluster.delta.svc.cluster.local']},
 {cluster_name,
     <<"rabbit@rabbitmq-cluster-0.rabbitmq-cluster.delta.svc.cluster.local">>},
 {partitions,[]},
 {alarms,
     [{'rabbit@rabbitmq-cluster-1.rabbitmq-cluster.delta.svc.cluster.local',
          []},
      {'rabbit@rabbitmq-cluster-0.rabbitmq-cluster.delta.svc.cluster.local',
          []}]}]
```

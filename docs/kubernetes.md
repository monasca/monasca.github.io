# Kubernetes

Monasca can be deployed into Kubernetes to monitor containers, services and Kubernetes itself.

## Monitoring Kubernetes

A deamonset/deployment of the [monasca-agent][1] will be brought up when deploying Monasca into Kubernetes. The
daemonset will monitor pod/node workloads and the deployment will monitor Kubernetes status/health. They both do
autodetection on Prometheus endpoints to scrape metrics from and send into the Monasca pipeline.

<img class="img-responsive"
        src="{{ '/assets/images/kubernetes_agent.png' | relative_url }}"
        alt="Monasca architecture diagram"/>

### Daemonset Monasca Agent

The Daemonset monasca-agent runs on every node in the cluster and collects metrics on pod/node workloads and autodetects
prometheus endpoints on pods.

#### Pod Usage Monitoring

Pod monitoring is accomplished by first querying Kubelet on each node to grab all running pods and their associated
metadata and then querying cAdvisor for container usage (memory, cpu, network, etc.). The agent then correlates the
container data from cAdvisor to the running pods to report usage metrics on each pod (container data is aggregated up
to the pod level).

The agent can be configured to report container metrics on top of the pod metrics if desired.

More information on the metrics we are collecting for pods can be seen in the plugin's [documentation][2]

#### Node Usage Monitoring

Node monitoring is accomplish by querying cAdvisor for the nodes usage metrics. The complete metric list can be found in
the plugin's [documentation][3]

#### Prometheus Endpoint Monitoring on Pods

The monasca agent on each node will autodetect Prometheus endpoints to scrape metrics from by querying the Kubelet for 
each running pod and looking at their annotations.

These annotations being:

* prometheus.io/scrape: Only scrape pods that have a value of 'true'
* prometheus.io/path: If the metrics path is not '/metrics' override this.
* prometheus.io/port: Scrape the pod on the indicated port instead of the default of '9102'.

If the pod contains the scrape annotation the agent will attempt to scrape metrics from it and send through Monasca.

### Deployment Monasca Agent

The Deployment monasca-agent collects metrics on the Kubernetes cluster and autodetects prometheus endpoints on
services.

#### Kubernetes Cluster Monitoring

The monasca agent queries the Kubernetes API for metrics such as component health, replica counts 
(on deployments/replicaton controllers), host status flags.

The full list of the metrics being collected can be seen in the plugin's [documentation][4]

#### Prometheus Endpoint Monitoring on Services

The monasca agent queries the Kubernetes API for services and then looks at the annotations correlated with each
service to determine to scrape or not.

These annotations being:

* prometheus.io/scrape: Only scrape services that have a value of 'true'
* prometheus.io/path: If the metrics path is not '/metrics' override this.
* prometheus.io/port: Scrape the service on the indicated port instead of the default of '9102'.

If the service contains the scrape annotation the agent will attempt to scrape metrics from it to send through Monasca.

## Future Work
* Iterate on the Prometheus autodetection to match what Prometheus Server does for autodetection
* Intergrate Monasca in Kubernetes Custom Metric API
* Look into integrating Kubernetes RBAC into Monasca.

[1]: https://github.com/openstack/monasca-agent
[2]: https://github.com/openstack/monasca-agent/blob/master/docs/Plugins.md#kubernetes
[3]: https://github.com/openstack/monasca-agent/blob/master/docs/Plugins.md#cadvisor_host
[4]: https://github.com/openstack/monasca-agent/blob/master/docs/Plugins.md#kubernetes_api

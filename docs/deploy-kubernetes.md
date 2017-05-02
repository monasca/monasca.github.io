# Installing Monasca via Helm

We have a Helm chart for Monasca and all of its microservices. This can be found at [Monasca Helm][1]. The charts are
hosted via github pages on [monasca.io][2]

# Quick Start

To install Monasca on a running Kubernetes cluster follow the following steps: 
{% highlight bash %}
helm repo add monasca http://monasca.io/monasca-helm-repo
helm install monasca/monasca --name monasca --namespace monitoring
{% endhighlight %}

More detailed configuration for installing Monasca can be found in the charts' [README][3]

## Default Grafana graphs

Grafana is deployed when bringing up Monasca and by default is configured with the Monasca datasource. Default
dashboards are also created for Deployments, Namespaces, Pod, Daemonset and Nodes.

Grafana can be accessed by port-forwarding the grafana service to localhost.

Setting up grafana port-forward:
```bash
$ kubectl get pods -n monitoring -l component=grafana
$ kubectl port-forward {{ grafana_pod_name_from_output_above }} -n monitoring 3000
```

After the above is set up you can visit [grafana][4] with the default credentials mini-mon/password.

## Future Work
* Expand on Default graphs that are being created
* Include default Kubernetes alarms on deploy
* Intergrate Helm work into official charts

[1]: https://github.com/monasca/monasca-helm
[2]: http://monasca.io/monasca-helm-repo/
[3]: https://github.com/monasca/monasca-helm/blob/master/monasca/README.md
[4]: http://localhost:3000

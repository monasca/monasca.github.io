---
layout: page
title: Architecture
---

Monasca Architecture
====================

<object class="img-responsive"
        data="{{ '/assets/images/architecture.svg' | relative_url }}"
        alt="Monasca architecture diagram"></object>

Components
----------

Main components:
 * [`monasca-api`][1]: The Monasca REST API
 * [`monasca-persister`][2]: Writes metrics to a time-series database
 * [`monasca-thresh`][3]: Thresholding engine, processes metrics and determines
   alarm states
 * [`monasca-notification`][4]: Delivers notifications when an alarm state
   transitions
 * [`monasca-agent`][5]: Collects metrics from a node, service, application,
   Prometheus endpoint, ...
 * [`monasca-log-api`][6]: API for working with log data in Monasca
 * [`monasca-aggregator`][7]: Near real-time continuous aggregation of Monasca metrics

Deployment methods:
 * [`monasca-docker`][8]: Docker containers and the `docker-compose` development
   environment
 * [`monasca-helm`][9]: Helm charts for deployment in Kubernetes
 * [`puppet-monasca`][10]: puppet modules for deploying Monasca in OpenStack
 * [`os_monasca`][11], [`os_monasca-agent`][12], [`os_monasca-ui`][13]: Ansible
   modules for deployment in an OpenStack environment

Client libraries:
 * [`python-monascaclient`][14]: CLI and Python library for interating with the
   Monasca API
 * [`monasca-statsd`][15]: statsd-compatible library for sending metrics from
   instrumented applications to Monasca

Integrations with other tools:
 * [`grafana`][21]: Forked version of Grafana that adds support for Keystone authentication
 * [`monasca-grafana-datasource`][16]: Monasca data source for Grafana
 * [`monasca-grafana-app`][17]: Application plugin for Grafana
 * [`monasca-kibana-plugin`][18]: Keystone authentication support and multi-tenancy for Kibana 4.6.x
 * [`monasca-ui`][19]: Monasca UI for [OpenStack Horizon][20]

[1]: https://github.com/openstack/monasca-api
[2]: https://github.com/openstack/monasca-persister
[3]: https://github.com/openstack/monasca-thresh
[4]: https://github.com/openstack/monasca-notification
[5]: https://github.com/openstack/monasca-agent
[6]: https://github.com/openstack/monasca-log-api
[7]: https://github.com/monasca/monasca-aggregator
[8]: https://github.com/monasca/monasca-docker
[9]: https://github.com/monasca/monasca-helm
[10]: https://github.com/openstack/puppet-monasca
[11]: https://github.com/openstack/openstack-ansible-os_monasca
[12]: https://github.com/openstack/openstack-ansible-os_monasca-agent
[13]: https://github.com/openstack/openstack-ansible-os_monasca-ui
[14]: https://github.com/openstack/python-monascaclient
[15]: https://github.com/openstack/monasca-statsd
[16]: https://github.com/openstack/monasca-grafana-datasource
[17]: https://github.com/stackhpc/monasca-grafana-app
[18]: https://github.com/openstack/monasca-kibana-plugin
[19]: https://github.com/openstack/monasca-ui
[20]: https://wiki.openstack.org/wiki/Horizon
[21]: https://github.com/sapcc/grafana/tree/keystone

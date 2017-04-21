---
layout: page
---

# About Monasca

Monasca is an open-source monitoring-as-a-service solution under the
[OpenStack "Big Tent"][1]. It aims to be highly performant, scalable, and
fault-tolerant.

## Features

Core principles:
 * multi-tenant
 * highly scalable
 * performant
 * fault-tolerant

Features:
 * accepts arbitrary metrics with key/value pair metadata (dimensions)
 * alarming and notification engines output to email, PagerDuty, webhooks,
   Slack, and HipChat

## Architecture

<img class="img-responsive"
     src="{{ '/assets/images/architecture.svg' | relative_url }}"
     alt="Monasca architecture diagram">

## Community

Monasca discussion usually occurs on IRC at irc.freenode.net #openstack-monasca

Many major companies are also involved in developing or deploying Monasca:

 * Hewlett-Packard Enterprise
 * Time Warner Cable (TWC)
 * Fujitsu
 * Cisco
 * Cray
 * Rackspace
 * SAP
 * NEC

## Presentations

Several overviews of Monasca can be found at the following:

- [Monasca Bootcamp][2] - Austin OpenStack Summit, 2016
- [Introducing Using Monasca for Production OpenStack Monitoring][3] - Tokyo OpenStack Summit, 2015
- [Monasca Deep Dive][4] - Paris OpenStack Summit, 2014
- [ELK and Monasca Crossing: Logging as an OpenStack Service][5] - Paris OpenStack Summit, 2014

## Licensing

Monasca is licensed under the [Apache 2.0 license][6].

[1]: https://governance.openstack.org/tc/reference/projects/
[2]: https://www.openstack.org/videos/austin-2016/monasca-bootcamp
[3]: https://www.openstack.org/videos/tokio-2015/tokyo-3230
[4]: https://www.openstack.org/videos/paris-2014/monasca-deep-dive-monitoring-at-scale
[5]: https://www.openstack.org/videos/tokio-2015/elk-and-monasca-crossing-logging-as-an-openstack-service
[6]: http://www.apache.org/licenses/LICENSE-2.0

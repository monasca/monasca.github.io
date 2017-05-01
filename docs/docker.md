---
layout: page
title: Docker
---

Docker Development Environment
==============================

[`docker-compose`][1] is the recommended way to quickly experiment with and
develop against Monasca. To get started, you'll need a Docker environment with:
 * Docker 1.13 or later, 17.04.0-ce or later recommended
 * docker-compose 1.9.0 or later
 * At least 4 GiB of memory available to Docker
 * At least 2 CPUs (cores)
 * `git`

Quickstart
----------

Clone the [`monasca-docker`][2] repository and run `docker-compose`:

{% highlight bash %}
git clone https://github.com/monasca/monasca-docker
cd monasca-docker
docker-compose up
{% endhighlight %}

If all goes well, the full Monasca pipeline should start within (roughly) one
minute. The following services should be exposed on your host machine:
 * keystone on ports 5000 and 35357
 * monasca-api on port 8070
 * grafana on port 3000 - log in using `mini-mon` and `password`

Note that the docker-compose environment currently does not start any Agent
instances. There will be few (if any) metrics going through the pipeline, though
it should otherwise be working.

You can the status of each component by running `docker-compose ps` (you will
probably need to run this in a separate shell unless you ran
`docker-compose up -d`). If everything started successfully, it should look like
so:

<figure><pre>
% docker-compose ps                                                                                                                                                                                                                               ✖ ✹ ✭
                Name                              Command               State                         Ports                       
---------------------------------------------------------------------------------------------------------------------------------
monascadocker_alarms_1                 /start.sh                        Exit 0                                                    
monascadocker_grafana-init_1           python /grafana.py               Exit 0                                                    
monascadocker_grafana_1                /go/bin/grafana-server -co ...   Up       0.0.0.0:3000->3000/tcp                           
monascadocker_influxdb-init_1          /init.sh                         Exit 0                                                    
monascadocker_influxdb_1               /entrypoint.sh influxd           Up       8086/tcp                                         
monascadocker_kafka_1                  /start.sh                        Up       9092/tcp                                         
monascadocker_keystone_1               /bin/sh -c /start.sh             Up       0.0.0.0:35357->35357/tcp, 0.0.0.0:5000->5000/tcp
monascadocker_monasca-notification_1   /start.sh                        Up                                                        
monascadocker_monasca-persister_1      /start.sh                        Up                                                        
monascadocker_monasca-sidecar_1        /bin/sh -c hug -p 4888 -f  ...   Up       4888/tcp                                         
monascadocker_monasca_1                /start.sh                        Up       0.0.0.0:8070->8070/tcp                           
monascadocker_mysql-init_1             /init.sh                         Exit 0                                                    
monascadocker_mysql_1                  docker-entrypoint.sh mysqld      Up       3306/tcp                                         
monascadocker_storm-nimbus_1           /entrypoint.sh storm nimbus      Up                                                        
monascadocker_storm-supervisor_1       /entrypoint.sh storm super ...   Up                                                        
monascadocker_thresh-init_1            /entrypoint.sh /submit.sh        Exit 0                                                    
monascadocker_zookeeper_1              /docker-entrypoint.sh zkSe ...   Up       2181/tcp, 2888/tcp, 3888/tcp
</pre></figure>

Note that several initialization jobs are run on new deployments, so it's normal
to see containers with an `Exit 0` state. See below for troubleshooting failed
containers.

Troubleshooting
---------------

### An init job failed!

Failed init jobs will appear in `docker-compose ps` with a nonzero exit code.
Occasionally jobs will fail due to timeouts, especially on systems with limited
CPU. In these cases it is probably safe to re-run the job by simply running
`docker-compose up` again. This will re-run all of the jobs, but only those that
failed to complete will actually modify the deployment.

If the jobs are still failing, you can view the log output of each job using
`docker-compose logs [job name]`, where `[job name]` is one of
`mysql-init`, `grafana-init`, `thresh-init`, `influxdb-init`, or `alarms`. The
log output should provide some reason for the failure that can be included in a
[GitHub issue][3].


[1]: https://docs.docker.com/compose/
[2]: https://github.com/monasca/monasca-docker
[3]: https://github.com/monasca/monasca-docker/issues

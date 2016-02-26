# MessageBusOps

Tools for managing and operating message bus based systems. Facilities include
searching, analysis and message replay.

The application is based on the ELK stack and uses Docker for easy deployment.

Based on the official images:

* [elasticsearch](https://registry.hub.docker.com/_/elasticsearch/)
* [logstash](https://registry.hub.docker.com/_/logstash/)
* [kibana](https://registry.hub.docker.com/_/kibana/)

# Requirements

## Setup

1. Install [Docker](http://docker.io).
2. Install [Docker-compose](http://docs.docker.com/compose/install/).
3. Clone this repository

## SELinux

On distributions which have SELinux enabled out-of-the-box you will need to either re-context the files or set SELinux into Permissive mode in order for docker-elk to start properly.
For example on Redhat and CentOS, the following will apply the proper context:

````bash
.-root@centos ~
-$ chcon -R system_u:object_r:admin_home_t:s0 fig-elk/
````

# Usage

Start the MessageBusOps stack using *docker-compose*:

```bash
$ docker-compose up
```

You can also choose to run it in background (detached mode):

```bash
$ docker-compose up -d
```

If you want to start the stack including a RabbitMQ, use:

```bash
docker-compose -f docker-compose-rabbit.yml up
```

Or, for detached mode:

```bash
docker-compose -f docker-compose-rabbit.yml up -d
```

Once you startup the containers, you can access the various services as follows:

* Kibana: http://localhost:5601
* Kibana Sense: http://localhost:5601/app/sense
* Rabbit Management Console (if you started it with your stack): http://localhost:15672

The stack exposes the following ports:

* 5000: Logstash TCP input
* 5602: Kibana
* 5672: RabbitMQ AMQP/TCP (If started)
* 9200: Elasticsearch HTTP
* 9300: Elasticsearch TCP
* 15672: RabbitMQ Management (If started)

_Note that if you are using docker toolbox, substitute the docker-machine host name or IP for localhost._

_Note that if you are using boot2docker, substitute the boot2docker IP address for localhost._

# Credits

* This project is based on the Docker ELK stack provided in the [docker-elk](https://github.com/deviantony/docker-elk)
project.

# JetGatling: gatling load testing make easy

[![Docker Stars](https://img.shields.io/docker/stars/scw1109/jet-gatling.svg)](https://hub.docker.com/r/scw1109/jet-gatling/)
[![Docker Pulls](https://img.shields.io/docker/pulls/scw1109/jet-gatling.svg)](https://hub.docker.com/r/scw1109/jet-gatling/)
[![Docker Automated build](https://img.shields.io/docker/automated/scw1109/jet-gatling.svg)](https://hub.docker.com/r/scw1109/jet-gatling/)

[![License](https://img.shields.io/badge/license-Apache%202.0-blue.svg)](http://www.apache.org/license/LICENSE-2.0.txt)

-----

## Overview

JetGatling provides a scenario DSL and package with [Gatling](http://gatling.io/), make the use of [Gatling](http://gatling.io/) without the trouble of writing the DSL.

### Background

[Gatling](http://gatling.io/) is a great load testing tool.
However it requires one to write the scenario in DSL to start a load testing.

This is not as convenient as using simple benchmarking tool like [ab](https://httpd.apache.org/docs/2.4/programs/ab.html) or [wrk](https://httpd.apache.org/docs/2.4/programs/ab.html).

Hence, JetGatling provides a scenario DSL which covers simple common use cases, make the usage of [Gatling](http://gatling.io/) as easy as [ab](https://httpd.apache.org/docs/2.4/programs/ab.html).

### Usage

 * Assuming you are familiar with the usage of [Docker](https://docs.docker.com/)

#### Run a simple load test (Fixed RPS mode)

```bash
docker run --rm scw1109/jet-gatling -r 5 -d 30 -u "https://google.com"
```

This will start a test that running **5 RPS** (requests per second) with a **30 seconds** duration against ```google.com```

Note that no matter how long the response take, the tool will send 5 requests in each second.

#### Run a simple load test (Fixed concurrent mode)

```bash
docker run --rm scw1109/jet-gatling -c 5 -d 30 -u "https://google.com"
```

This will start a test that running **5 concurrent clients** with a **30 seconds** duration against ```google.com```

Note that each client will send next request as soon as it receive a response.
Which acts more like [ab](https://httpd.apache.org/docs/2.4/programs/ab.html)

#### To keep the generated report

Gatling report is generated under path ```/jet-gatling/results``` in the docker.
To keep the report in host machine, we could use volume function of docker.

```bash
docker run --rm -v /tmp/jet-gatling/results:/jet-gatling/results scw1109/jet-gatling -r 5 -d 30 -u "https://google.com"
```

This command will keep the Gatling reports under ```/tmp/jet-gatling/results``` of the host machine.

#### Providing user files

JetGaling allows user to provide input file for some function.
For example, to provide multiple paths for the load testing.

In order to provide the file to JetGatling, one should use volume to allow the docker runtime to see the file.

```bash
docker run --rm -v /tmp/user-files:/jet-gatling/user-files -r 5 -d 30 -u "https://google.com" -p "/jet-gatling/path"
```

This command will read the path file under ```/tmp/jet-gatling/user-files```.

#### Show usage

For other parameters, use the following command to check the details.

```bash
docker run --rm scw1109/jet-gatling -h
```

## Developer Guide

See [developer.md](developer.md)

## License

The license is Apache 2.0, see [LICENSE-2.0.txt](LICENSE-2.0.txt)

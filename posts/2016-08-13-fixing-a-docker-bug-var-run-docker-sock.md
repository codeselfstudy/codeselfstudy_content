---
title: Fixing a Docker Bug: /var/run/docker.sock
date: 2016-08-13
path: "/blog/fixing-a-docker-bug-varrundockersock/"
---

I encountered a Docker bug that took a long time to fix. Every time I tried to run Docker on Ubuntu 14.04, I would see this error:

```text
$ docker ps
An error occurred trying to connect: Get http://%2Fvar%2Frun%2Fdocker.sock/v1.24/containers/json: read unix @->/var/run/docker.sock: read: connection reset by peer
```

This bug was quite time consuming to figure out.

tl;dr The solution for me was to purge docker-engine and then delete <code>/var/lib/docker</code>, reboot, and then reinstall docker-engine. The answer was buried in <a href="https://github.com/docker/docker/issues/17846">this discussion</a>.

```text
$ sudo apt-get autoremove --purge docker-engine

# Nothing worked until I added this step
$ sudo rm -rfv /var/lib/docker

# Reboot here

$ sudo apt-get update
$ sudo apt-get install docker-engine
```

Purging docker-engine, rebooting, and reinstalling, didn't work. The fix required removing the <code>/var/lib/docker</code> directory.

Here is more system information for anyone else who encounters this problem.

```text
$ docker version
Client:
 Version:      1.12.0
 API version:  1.24
 Go version:   go1.6.3
 Git commit:   8eab29e
 Built:        Thu Jul 28 22:00:36 2016
 OS/Arch:      linux/amd64
An error occurred trying to connect: Get http://%2Fvar%2Frun%2Fdocker.sock/v1.24/version: read unix @->/var/run/docker.sock: read: connection reset by peer

$ docker info
An error occurred trying to connect: Get http://%2Fvar%2Frun%2Fdocker.sock/v1.24/info: read unix @->/var/run/docker.sock: read: connection reset by peer

$ dpkg -l | grep docker
ii  docker-engine                                               1.12.0-0~trusty                                     amd64        Docker: the open-source application container engine
rc  docker.io                                                   1.6.2~dfsg1-1ubuntu4~14.04.1                        amd64        Linux container runtime

# Ubuntu 14.04
$ uname -a
Linux z84302 3.13.0-93-generic #140-Ubuntu SMP Mon Jul 18 21:21:05 UTC 2016 x86_64 x86_64 x86_64 GNU/Linux
```

This recommended solution didn't work:

```text
$ sudo service docker stop
docker stop/waiting

$ sudo rm /var/lib/docker/network/files/local-kv.db
rm: cannot remove /var/lib/docker/network/files/local-kv.db: No such file or directory

$ sudo service docker start
docker start/running, process 26994
```
More info:

```text
$ tail /var/log/syslog
Aug 13 15:28:37 z84302 kernel: [ 3185.793539] init: docker main process ended, respawning
Aug 13 15:28:38 z84302 kernel: [ 3186.898659] type=1400 audit(1471127318.303:912): apparmor="STATUS" operation="profile_replace" profile="unconfined" name="docker-default" pid=16862 comm="apparmor_parser"
Aug 13 15:28:38 z84302 kernel: [ 3186.963235] init: docker main process (16837) terminated with status 1
Aug 13 15:28:38 z84302 kernel: [ 3186.963244] init: docker main process ended, respawning
Aug 13 15:28:39 z84302 kernel: [ 3188.074909] type=1400 audit(1471127319.479:913): apparmor="STATUS" operation="profile_replace" profile="unconfined" name="docker-default" pid=16911 comm="apparmor_parser"
Aug 13 15:28:39 z84302 kernel: [ 3188.148967] init: docker main process (16888) terminated with status 1
Aug 13 15:28:39 z84302 kernel: [ 3188.148996] init: docker main process ended, respawning
Aug 13 15:28:40 z84302 kernel: [ 3189.296377] type=1400 audit(1471127320.699:914): apparmor="STATUS" operation="profile_replace" profile="unconfined" name="docker-default" pid=16960 comm="apparmor_parser"
Aug 13 15:28:40 z84302 kernel: [ 3189.387307] init: docker main process (16937) terminated with status 1
Aug 13 15:28:40 z84302 kernel: [ 3189.387316] init: docker main process ended, respawning

$ docker images
Cannot connect to the Docker daemon. Is the docker daemon running on this host?

$ sudo service docker start
start: Job is already running: docker
```

I hope that this info helps someone else fix the problem.

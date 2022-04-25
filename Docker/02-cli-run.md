# Docker CLI - run

```bash
$ docker run [OPTIONS] IMAGE[:TAG|@DIGEST] [COMMAND] [ARG...]
```
<br/>

### detached( -d )
```bash
$ docker run -d -p 80:80 my_image service nginx start
```
* Detach right away from the generated session after run commands.
* Case
  * Some of the process must be run as daemons.
* [LINK](https://docs.docker.com/engine/reference/run/#detached--d)

<br/>

### Foreground( -it )
```bash
$ docker run -a stdin -a stdout -i -t ubuntu /bin/bash
# OR
$ docker run -a stdin -a stdout -it ubuntu /bin/bash
```
* The opposite case of the detached mode. User enter in interpreter mode.
* Case
  * Interaction mode( Normal shell )
* [LINK](https://docs.docker.com/engine/reference/run/#foreground)

<br/>

### clean up( --rm )
```bash
$ docker run --rm -v /foo -v awesome:/bar busybox top
```
* Clean up all files and relatives when the container termintated.
* Case
  * Debugging
  * Dry run
  * Test
* [LINK](https://docs.docker.com/engine/reference/run/#clean-up---rm)

<br/>

### user( --user )
```bash
$ docker run --rm --user whoami -v awesome:/bar busybox top
```
* Run as a specific user. 
* Case
  * User with permissions.
* [LINK](https://docs.docker.com/engine/reference/run/#user)

<br/>

### name( --name )
```bash
$ docker run --rm --name whatismyname -v awesome:/bar busybox top
```
* Set the unique name to the running container.
* Case
  * Specify the name for variaous purpose.
* [LINK](https://docs.docker.com/engine/reference/run/#name---name)

<br/>

### environment( -e )
```bash
$ docker run --rm -e PYTHONPATH=/where/is/the/python/bin -v awesome:/bar busybox top
```
* Set environments to the container.
* Case
  * Set different environments to each containers born by the one image.
* [LINK](https://docs.docker.com/engine/reference/run/#env-environment-variables)

<br/>

### volume( -v )
```bash
# -v location_in_real_world:alias_in_container
$ docker run --rm -e PYTHONPATH=/where/is/the/python/bin -v awesome:/bar busybox top
```
* Attach the volume in the real world to the container( as aliased name )
* Case
  * Store or Share the data with real world.
* [LINK](https://docs.docker.com/engine/reference/run/#volume-shared-filesystems)

<br/>

### Open port from the container to out( -p )
```bash
$ docker run --rm -p 3306:3306 -v awesome:/bar busybox top
# OR
$ docker run --rm --publish "0.0.0.0:8888:8888" busybox top
```
* Open port from container to outside.
* Case
  * Specific port open to run container as MW( i.e. redis, MariaDB, Web apps... )
* [LINK](https://docs.docker.com/engine/reference/run/#expose-incoming-ports)

<br/>

### Restart policy( --restart )
```bash
$ docker run --restart=always redis
```
* To make container is rebooted( or is restarted ) when docker service is restarted.
* possible option
  * no: default
  * on-failure[:max-retries]
  * always
  * unless-stopped
* Case
  * Something important service container. ( i.e. Database, Cache, Webapp )
* [LINK 1](https://docs.docker.com/engine/reference/run/#restart-policies---restart)
* [LINK 2](https://jamesu.dev/posts/2019/12/19/starting-container-automatically/)

## Working directory( -w )
```bash
$ docker run --rm -it -w /home/whoami/oneoff someofimage:version /bin/bash
```
* Go to working directory after the container is started.
* Case
  * Interpreter mode
* [LINK](https://docs.docker.com/engine/reference/run/#workdir)

<br/><br/>

## Reference
  * [#1](https://docs.docker.com/engine/reference/run/)
  * [#2](https://nicewoong.github.io/development/2017/10/09/basic-usage-for-docker/)
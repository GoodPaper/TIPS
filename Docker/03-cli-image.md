# Docker CLI - About Image

<br/>

### save
```bash
# docker save {option} filename imagename:version
$ docker save -o whatisthis.tar imagename:version
```
* Save image to a file.
* [LINK](https://docs.docker.com/engine/reference/commandline/save/)

<br/>

### load
```bash
# docker load -i filename
$ docker load -i thisiswhat.tar
```
* Load image from a file.
* [LINK](https://docs.docker.com/engine/reference/commandline/load/)

<br/>

### export
```bash
# docker export {option} container
$ docker export -o hahaha.tar panda
```
* Export image to a file.
* [LINK](https://docs.docker.com/engine/reference/commandline/export/)

<br/>

### import
```bash
# docker import {option} file - {repository}
$ docker import https://somewhere.repo.com/sample.tgz
```
* Import image from the source.
* [LINK](https://docs.docker.com/engine/reference/commandline/import/)

<br/><br/>

## Reference
  * [#1](https://www.leafcats.com/240)

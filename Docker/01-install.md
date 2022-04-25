# Docker

#### Install
```bash
# 1. Uninstall older version.
$ sudo apt-get remove docker docker-engine docker.io containerd runc

# 2. Setup repository
$ sudo apt-get update

$ sudo apt-get install ca-certificates curl gnupg  lsb-release

$ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg

$ echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

# 3. Install
$ sudo apt-get update

$ sudo apt-get install docker-ce docker-ce-cli containerd.io

# 4. Verify as run
$ sudo docker run hello-world
```

* Reference
  * [ #1 ](https://docs.docker.com/engine/install/ubuntu/)
# Installation on Ubuntu
## APT Repository
### Install the repository for stable releases
```sh
sudo add-apt-repository "deb https://packages.grafana.com/oss/deb stable main"
```
### Optional for beta releases
There is a separate repository if you want beta releases. If you dont want beta release then you dont need to execute below command.

```sh
sudo add-apt-repository "deb https://packages.grafana.com/oss/deb beta main"
```

Use the above line even if you are on Ubuntu or another Debian version. Then add our gpg key. This allows you to install signed packages.

```sh
curl https://packages.grafana.com/gpg.key | sudo apt-key add -
```

### Update your Apt repositories and install Grafana
```sh
sudo apt-get update
sudo apt-get install grafana
```

![Installation](https://github.com/HuangMarco/knowledge-hub/blob/dev/zResources/grafana/installation.jpg)



# Reference Links
https://grafana.com/docs/installation/
<br>
https://grafana.com/docs/installation/debian/
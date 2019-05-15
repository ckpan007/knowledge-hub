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


# Intasllation Output

## Environment file
* systemd service file and init.d script are both use the file located at **/etc/default/grafana-server** for environment variables used when starting the back-end

You can overide below configuration:
* log directory
* data directory
* other variables


![ETC Default Grafana](https://github.com/HuangMarco/knowledge-hub/blob/dev/zResources/grafana/etc-default-grafana.jpg)

## Logging 
By default Grafana will log to /var/log/grafana.

## Database
The default configuration specifies a sqlite3 database located at **/var/lib/grafana/grafana.db**. **Please backup this database before upgrades**. You can also use MySQL or Postgres as the Grafana database, as detailed on the configuration page.


# Start the server (init.d service)
```sh
sudo service grafana-server start
```

This will start the grafana-server process as the grafana user, which was created during the package installation. 
* The default HTTP port is 3000 and default user and group is admin
* Default login and password admin/ admin

## Configure the Grafana server to start at boot time
```sh
sudo update-rc.d grafana-server defaults
```

# Start the server (via systemd)
```sh
systemctl daemon-reload
systemctl start grafana-server
systemctl status grafana-server
```

## Enable the systemd service so that Grafana starts at boot
```sh
sudo systemctl enable grafana-server.service
```


# Configuration
The configuration file is located at **/etc/grafana/grafana.ini**. For more detail related with [configuration](https://grafana.com/docs/installation/configuration/).

![Grafana Configuration](https://github.com/HuangMarco/knowledge-hub/blob/dev/zResources/grafana/grafana-configuration.jpg)




# Reference Links
https://grafana.com/docs/installation/
<br>
https://grafana.com/docs/installation/debian/
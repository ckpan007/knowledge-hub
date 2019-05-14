# Installation - Unbuntu Deb
```sh
curl -L -O https://artifacts.elastic.co/downloads/beats/filebeat/filebeat-7.0.1-amd64.deb
sudo dpkg -i filebeat-7.0.1-amd64.deb

```

![Installation](https://github.com/HuangMarco/knowledge-hub/blob/dev/zResources/filebeat/installation.jpg)


# Installation Output
* The filebeat will be installed at **/usr/share/filebeat**
* The configuration files stored at **/etc/filebeat/filebeat.yml**

# Configuration
```
filebeat.inputs:
- type: log
  enabled: true
  paths:
    - /var/log/*.log
    #- c:\programdata\elasticsearch\logs\*
```

Above is the sample of the filebeat section of the filebeat.yml file.

# Start a behavior of configuring filebeat

## Define the path (or paths) to your log files.
```
filebeat.inputs:
- type: log
  enabled: true
  paths:
    - /var/log/*.log

```
The input in this example harvests all files in the path /var/log/*.log, which means that Filebeat will harvest all files in the directory /var/log/ that end with .log. All patterns supported by [Go Glob](https://golang.org/pkg/path/filepath/#Glob) are also supported here.

```
/var/log/*/*.log

```
This fetches all .log files from the subfolders of /var/log. It does not fetch log files from the /var/log folder itself.
<br>
**Notice**: Currently it is not possible to recursively fetch all files in all subdirectories of a directory.


# Reference Link
https://www.elastic.co/guide/en/beats/filebeat/current/filebeat-getting-started.html



# JVM Settings
Usually you will not to change the JVM settings, because of that Elasticsearch is developed by Java programming language. So usually you dont need to change any settings related with ES anymore. As you know about the jvm performance tuning, the most likely change is setting the _heap size_.

# Changement
* The default location of this file is config/jvm.options (when installing from the tar or zip distributions) 
* /etc/elasticsearch/jvm.options (when installing from the Debian or RPM packages)

# Tuning Options
* -Xmx2g - JVM option applies independent of the version of the JVM
* 8:-Xmx2g - JVM option applies of Java 8, maximum size of heap size is 2g
* 8-:-Xmx2g - JVM option applies of Java version greater than 8
* 8-9:-Xmx2g - JVM option applies of Java 8 and Java 9

# Tuning by ES_JAVA_OPTS
```
export ES_JAVA_OPTS="$ES_JAVA_OPTS -Djava.io.tmpdir=/path/to/temp/dir"
./bin/elasticsearch
```
You can also use _ES_JAVA_OPTS_ to tuning the ES JVM. Much more detail about this please refer to [System Configuration File](https://www.elastic.co/guide/en/elasticsearch/reference/current/setting-system-settings.html#sysconfig).



# Secure Settings

## Why you need secure settings?
You still remember that we run ES by a new user named _elsearch_, acturally this user should be naturally created by ES as user _elasticsearch_. For more detail you can go to check [ES Config](https://github.com/HuangMarco/knowledge-hub/blob/dev/elk/Elasticsearch/03-elasticsearch-config.md#create-elasticsearch-user-to-run-es).

<br>
Under this situation, Elasticsearch provides a keystore and the elasticsearch-keystore tool to manage the settings in the keystore.

## Note for secure settings
* All commands here should be run as the user which will run Elasticsearch
* Only some settings are designed to be read from the keystore. See documentation for each setting to see if it is supported as part of the keystore
* All the modifications to the keystore take affect only after restarting Elasticsearch
* The elasticsearch keystore currently only provides obfuscation. In the future, password protection will be added


## Create the keysotre
According to the official documentation, user can call command _bin/elasticsearch-keystore create_ to create _elasticsearch.keystore_. But when follow the installation in my guide, you will find that the _elasticsearch.keystore_ is already created there.

```sh
./bin/elasticsearch-keystore create
```

## List the settings in the keystore
```sh
./bin/elasticsearch-keystore list # This will list all the settings here

```

## Add the settings into the keystore
```sh
./bin/elasticsearch-keystore add <the.setting.name.to.set>


cat /file/containing/setting/value | bin/elasticsearch-keystore add --stdin the.setting.name.to.set # 暂时不知道要怎样用这种命令添加
```

Sensitive string settings, like authentication credentials for cloud plugins, can be added using the add command.

## Remove the settings
```sh
bin/elasticsearch-keystore remove the.setting.name.to.remove
```

## Reload the secure settings to make the changes work - important
This is for a node that is running, if you want to make a running node use the settings you set, you need to do below.<br>

Just like the settings values in elasticsearch.yml, changes to the keystore contents _are not automatically applied to the running elasticsearch node_. _Re-reading settings requires a node restart_. However, certain secure settings are marked as _reloadable_. Such settings can be re-read and applied on a running node by using below command:

```sh
POST _nodes/reload_secure_settings
```

Above command will decrypt and re-read the entire keystore, on every cluster node, but _only the reloadable secure settings will be applied_. Changes to other settings will not go into effect until the next restart. Once the call returns, the reload has been completed, meaning that all internal datastructures dependent on these settings have been changed. Everything should look as if the settings had the new value from the start.

When changing multiple reloadable secure settings, modify all of them, on each cluster node, and then issue a reload_secure_settings call, instead of reloading after each modification.





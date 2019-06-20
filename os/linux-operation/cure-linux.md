# 良方啊哈哈哈
## apt-get
### 无法获得锁
```
Could not get lock /var/lib/dpkg/lock-frontend

Solution:

a. ps -e|grep apt-get
   sudo kill <pid>

b. sudo rm /var/lib/dpkg/lock-frontend
```

### Invalid operation package
```sh
root@ubuntu:/opt# apt package index
# E: Invalid operation package

# 如果上述情况，执行：

sudo apt update && sudo apt full-upgrade # 让系统进行更新即可。注意：不要再随意运行apt autoremove命令了！
```



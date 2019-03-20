# What is it?
This is for linux operation usage.

# Linux Operation

## Linux version

```sh
cat /etc/*-release

hostnamectl
# find out the linux kernel
uname -a
uname -mrs

#check is 32bit or 64bit
uanme -i

cat /proc/version
```


## Switch directory using pushd&dirs
```sh
# pushd to go to directory not cd
pushd <directoryname>

# dirs to select all parameters
dirs -v # 显示索引
dirs -p #每行显示一条记录
dirs -c 清空目录桟

pushd #不加任何参数代表在索引1和索引2中间切换

pushd +/-n #一般要先dirs -v，然后再用索引切换
```










# Software Operation

## docker
```sh
# docker iamge all
docker image ls -a
#docker container -a
docker contaienr ls -a

```
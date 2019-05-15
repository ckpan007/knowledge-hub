# Encoding Convention
```
git有个自动转换换行符功能，在文件commit时会自动转换换行符格式；
不想使用，也可以通过 git config --global core.autocrlf false 关闭

git-windows自带有dos2unix.exe
执行 find . -type f -exec dos2unix {} \; 批量转换
```

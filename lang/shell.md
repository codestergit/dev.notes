# Shell

### 获取当前正在执行脚本的绝对路径
```
basepath=$(cd `dirname $0`; pwd)
```
dirname $0，取得当前执行的脚本文件的父目录   
cd `dirname $0`，进入这个目录(切换当前工作目录)   
pwd，显示当前工作目录(cd执行后的)   
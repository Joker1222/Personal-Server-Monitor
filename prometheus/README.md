# Prometheus Install and Deploy
[最新版本请到官方下载](https://prometheus.io/download/)

> 建议将此工具链放到/opt目录下,root权限执行即可,以下命令默认在/opt目录下安装部署

# Linux
~~~bash
# Download
$ cd /opt/ && wget https://github.com/Joker1222/Personal-Server-Monitor/blob/master/prometheus/prometheus-2.23.0-linux_amd64.tgz

# Decompression
$ tar -zxvf prometheus-2.23.0.linux-amd64.tgz

# Change dir name
$ mv prometheus-2.23.0.linux-amd64 prometheus
~~~

~~~bash
# run.sh 这里自己封装了一套启停服务脚本,以及守护进程脚本。
# param list: 
#             - start   以守护进程的方式启动,启动守护进程,通过守护进程启动prometheus,日志输出在./log/目录下
#             - stop    终止守护进程、终止prometheus进程
#             - status  查看prometheus进程状态
#             - restart 如果守护进程不存在,则启动守护进程,如果守护进程存在则直接关掉prometheus进程,等待5s后prometheus被守护进程自动拉起
$ cd prometheus/ && ./run.sh start 
~~~




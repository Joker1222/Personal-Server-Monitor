# My personal server monitoring tools

> The following are common server monitoring tools,back up the available packages and the deployment process.

### tools list:
| Tools Name | Version |
|-|-|
| Prometheus| 2.23.0 |
| Grafana| 7.3.4 |
| Node_Exporter| 1.0.1 |
| Process_Exporter|  |

# Deploy in sequence
1. [Prometheus click here ](https://github.com/Joker1222/Personal-Server-Monitor/tree/master/prometheus) <br>

2. [Grafana click here ](https://github.com/Joker1222/Personal-Server-Monitor/tree/master/grafana) <br>

3. [NodeExporter click here ](https://github.com/Joker1222/Personal-Server-Monitor/tree/master/node_exporter) <br>

4. [ProcessExporter click here ](https://github.com/Joker1222/Personal-Server-Monitor/tree/master/process_exporter) <br>

# 上述工具安装部署成功后,下面将各个工具连接起来 
> 大致思路: exporter采集数据 -> prometheus服务接收数据 -> grafana调用prometheus服务的相关接口获取数据源

### 1. Prometheus服务配置exporterIP:端口 
~~~bash

$ vim /opt/prometheus/prometheus.yml
# my global config
global:
  scrape_interval:     15s # Set the scrape interval to every 15 seconds. Default is every 1 minute.
  evaluation_interval: 15s # Evaluate rules every 15 seconds. The default is every 1 minute.
  # scrape_timeout is set to the global default (10s).

# Alertmanager configuration
alerting:
  alertmanagers:
  - static_configs:
    - targets:
      # - alertmanager:9093

# Load rules once and periodically evaluate them according to the global 'evaluation_interval'.
rule_files:
  # - "first_rules.yml"
  # - "second_rules.yml"

# A scrape configuration containing exactly one endpoint to scrape:
# Here it's Prometheus itself.
scrape_configs:
  # The job name is added as a label `job=<job_name>` to any timeseries scraped from this config.
  - job_name: 'prometheus'   # 主要是以下三行,如果启动了exporter就把相应的地址配置进去
    static_configs:
      - targets: ['localhost:9090']
      
  # 这里举两个例子
  - job_name: 'node_exporter'   # node_exporter是部署在被监控服务机器上的,填写被监控机器的IP端口(9100)
    static_configs:
      - targets: ['ServerIP:9100'] #node_exporter端口默认为9100
     
  - job_name: 'process_exporter'   # process_exporter是部署在被监控服务机器上的,填写被监控机器的IP端口(9256)
    static_configs:
      - targets: ['ServerIP:9256']
$ cd /opt/prometheus/ && ./run.sh restart # 保存后重启prometheus即可生效.
~~~
#### 浏览器验证
http://ServerIP:9090 <br>
- 如果成功能看到以下效果
![PrometheusTargetShow](https://raw.githubusercontent.com/Joker1222/remote_png/master/prometheus/PrometheusTargetShow.png)

### 2. 

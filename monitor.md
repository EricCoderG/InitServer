# 炫酷的监控界面

## 安装PROMETHEUS和GRAFANA

`docker-compose.yml`

```dockerfile
version: '2'

networks:
    monitor:
        driver: bridge

services:
    prometheus:
        image: prom/prometheus
        container_name: prometheus
        hostname: prometheus
        restart: always
        volumes:
            - ./prometheus.yml:/etc/prometheus/prometheus.yml
        ports:
            - "9090:9090"
        networks:
            - monitor

    alertmanager:
        image: prom/alertmanager
        container_name: alertmanager
        hostname: alertmanager
        restart: always
        ports:
            - "9093:9093"
        networks:
            - monitor

    grafana:
        image: grafana/grafana
        container_name: grafana
        hostname: grafana
        restart: always
        ports:
            - "3000:3000"
        networks:
            - monitor

    node-exporter:
        image: quay.io/prometheus/node-exporter
        container_name: node-exporter
        hostname: node-exporter
        restart: always
        ports:
            - "9100:9100"
        networks:
            - monitor

    cadvisor:
        image: google/cadvisor:latest
        container_name: cadvisor
        hostname: cadvisor
        restart: always
        volumes:
            - /:/rootfs:ro
            - /var/run:/var/run:rw
            - /sys:/sys:ro
            - /var/lib/docker/:/var/lib/docker:ro
        ports:
            - "8899:8080"
        networks:
            - monitor
```

新建prometheus的配置文件`prometheus.yml`

```
global:
  scrape_interval:     15s
  evaluation_interval: 15s
scrape_configs:
  - job_name: 'prometheus'
    static_configs:
    - targets: ['ip:9090']  
  - job_name: 'cadvisor'
    static_configs:
    - targets: ['ip:8899']  
  - job_name: 'node'
    static_configs:
    - targets: ['ip:9100']
```

（这里要注意端口，按自己配置的来,ip也要填写为自己的）

把这份prometheus.yml的配置往/etc/prometheus/prometheus.yml 路径下复制一份。随后在目录下docker-compose up -d启动，于是我们就可以分别访问：

●http://ip:9100/metrics( 查看服务器的指标)

●http://ip:8899/metrics（查看docker容器的指标）

●http://ip:9090/(prometheus的原生web-ui)

●http://ip:3000/(Grafana开源的监控可视化组件页面)

进到Grafana首页，配置prometheus作为数据源

![img](https://ericcoder-oss.oss-cn-hangzhou.aliyuncs.com/markdown_images/1649397907474-ce924cf6-c84f-4e5a-9045-0cd6a8330cf7.jpeg)



进到配置页面，写下对应的URL，然后保存就好了。



![img](https://ericcoder-oss.oss-cn-hangzhou.aliyuncs.com/markdown_images/1649397911594-d89b08c9-00e7-4e71-8909-af58fc501e48.jpeg)



相关监控的模板可以在 https://grafana.com/grafana/dashboards/ 这里查到。



![img](https://ericcoder-oss.oss-cn-hangzhou.aliyuncs.com/markdown_images/1649397916124-6b2a05a2-d59f-4fb4-bf0c-6fb39bab13af.jpeg)



服务器的监控直接选用**8919**的就好了



![img](https://ericcoder-oss.oss-cn-hangzhou.aliyuncs.com/markdown_images/1649397920489-10839045-d582-4acd-810f-8aec483c99ed.jpeg)



![img](https://ericcoder-oss.oss-cn-hangzhou.aliyuncs.com/markdown_images/1649397925152-30e1781f-c601-4170-8076-05bb3a10ba09.jpeg)



import后就能直接看到高大上的监控页面了：



![img](https://ericcoder-oss.oss-cn-hangzhou.aliyuncs.com/markdown_images/1649397930129-f2da9c4b-14a9-4638-a913-fe8a104d19c8.jpeg)



使用模板**893**来配置监控docker的信息：



![img](https://ericcoder-oss.oss-cn-hangzhou.aliyuncs.com/markdown_images/1649397939031-37d000fa-3e26-41eb-bfac-734af6823bd0.jpeg)



![img](https://ericcoder-oss.oss-cn-hangzhou.aliyuncs.com/markdown_images/1649397944329-7b496ff6-3e20-4823-b5e7-3e8dc301b5f0.jpeg)


# Docker-LogStash
Docker LogStash

## 介绍用Docker 发布LogStash

**重点要求是 配置文件外放 configs配置 / 挂载外部日志文件路径方便读取 / 每个节点部署一个**


      version: "3.3"
      services:
        logstash:
          image: www.hbasesoft.com:8134/logstash
          hostname: logstash
          container_name: logstash
          restart: always
          deploy:
            mode: global    
          volumes:
            - /home:/home 
          configs:
             -  my_first_config
          command: logstash -f my_first_config
          networks:
             - outside          
      networks:
        outside:
          external:
            name: hbasesoft-network    
      configs:
        my_first_config:
          external:
            name: logstash   
        


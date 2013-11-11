ansible-elasticsearch
=====================

项目目的：通过ansible实现fluentd+es+kibana架构的实现  
elasticsearch...开源分布式搜索引擎  cool  
kibana3...日志分析，可视化接口  
fluentd...日志收集系统 

ansible...自动化管理工具  

系统环境
-----
CentOS 5.8 64bit 

服务器端环境
-----
    $ ansible --version  
    ansible 1.4

    $ ruby -v  
    ruby 1.9.3p194 (2012-04-20 revision 35410) [x86_64-darwin11.4.2]

    $ gem list |grep serverspec  
    serverspec (0.7.12)

使用工具
------
+ elasticsearch  
 - plugin bigdesk --集群监控工具 
 - plugin head    --集群管理工具
+ kibana3
+ fluentd
+ nginx

使用方法
-----
1. 修改hosts  
git clone之后记得修改hosts文件里的主机IP

2. SSH秘钥 
客户端和服务器端密钥进行认证

3. es-server赋值
在/etc/hosts里面手动绑定es-server IP,一般绑定为服务器端IP

4. ansible playbook 执行  
执行命令如下：  
```
$ ansible-playbook setup.yml -i hosts  
```

当出现yum失败时 请重新执行命令。

5. 编写测试  
  
spec/default spec/xxx.xxx.xxx.xxx 请按此规格变更。

6. 运行测试  
运行如下命令：  
```
$ rake spec
```

7. kibana3访问地址  
```
http://IP/  
```

9. elasticsearch的集群监控工具bigdesk访问地址 
  
```
http://IP地址:9200/_plugin/bigdesk  
```

10. elasticsearch的集群管理工具head的访问地址  
  
``` 
http://IP地址:9200/_plugin/head  
```

注意点
-----
1. es-server  
在/etc/hosts记得手动绑定IP地址
  
```
$ find ./  |xargs grep -n es-server  
./roles/es/templates/elasticsearch.yml:202:    network.bind_host: es-server  
./roles/nginx/templates/nginx.conf:4:          server_name           es-server;  
./roles/td-agent/templates/td-agent.conf:14:   host es-server  
./roles/kibana/vars/main.yml:3:                 servername: es-server  
```

2. fluntd收集对象  
本项目默认设置的是fluentd収集/var/log/nginx/access.log日志。    

工具地址
-----
+ [elasticsearch](http://www.elasticsearch.org/)
 - plugin [bigdesk](https://github.com/lukas-vlcek/bigdesk/)
 - plugin [head](http://mobz.github.io/elasticsearch-head/)
+ [kibana3](http://three.kibana.org/)
+ [fluentd](http://fluentd.org/)
+ [nginx](http://nginx.org/ja/)

kibana增加中国地图  作者：kindle
------
1.将map.cn.js文件放到/panels/map/lib/目录下。

2.修改/panels/map/editor.html

将['world','europe','usa']修改成['world','europe','usa','cn']即可

这时候增加地图的下拉列表里就有个cn名字的地图

增强:

1.增加了台湾地图

2.完善了内部编号和geoip数据库的编号对应关系
作者地址：http://blog.sectop.org/



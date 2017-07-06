https://floodlight.atlassian.net/wiki/display/floodlightcontroller/Installation+Guide

git clone git://github.com/floodlight/floodlight.git
git submodule init
git submodule update
ant

sudo mkdir /var/lib/floodlight
sudo chmod 777 /var/lib/floodlight
java -jar target/floodlight.jar

配置文件:
floodlight/src/main/resources/floodlightdefault.properties
floodlight/src/main/resources/learningswitch.properties

http://10.1.50.176:8080/ui/pages/index.html


导入Eclipse运行

curl http://localhost:8080/wm/core/controller/switches/json
请求该控制器上所有的switch的DPID

curl -d '{"switch":"00:00:de:c1:43:9b:64:46", "name":"Open_vSwitch", "cookie":"0", "priority":"32768","ingress-port":"1","active":"true","actions":"output=2"}' http://localhost:8080/wm/staticflowentrypusher/json
加入流表项

curl http://localhost:8080/wm/staticflowentrypusher/list/all/json
读取流表项

curl -X DELETE –d '{"name":"Open_vSwitch"}' http://localhost:8080/wm/staticflowentrypusher/json
删除流表项

curl http://localhost:8080/wm/staticflowentrypusher /clear/<dpid>/json
删除所有的流表项


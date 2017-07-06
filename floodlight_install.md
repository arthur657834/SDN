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


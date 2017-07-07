```
安装java

wget https://nexus.opendaylight.org/content/repositories/public/org/opendaylight/integration/distribution-karaf/0.6.0-Carbon/distribution-karaf-0.6.0-Carbon.tar.gz

tar zxvf distribution-karaf-0.6.0-Carbon.tar.gz 

cd /opt/software/distribution-karaf-0.6.0-Carbon/bin/
./karaf 
feature:install odl-restconf
feature:install odl-l2switch-switch
feature:install odl-openflowplugin-flow-services-ui
feature:install odl-mdsal-apidocs
feature:install odl-dlux-core
feature:install odl-dluxapps-nodes 
feature:install odl-dluxapps-yangui

feature:list

#list the installed Karaf features
feature:list -i 

feature:list | grep openflowplugin

 
重新安装:
删除data目录：rm –r data，进入bin目录：cd bin，执行./karaf clean，再次重复上面的安装组件操作。

按ctrl+d ,退出容器和中止服务


http://[ODL_host_ip]:8181/dlux/index.html
admin/admin
```




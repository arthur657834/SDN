```
java -jar target/floodlight.jar

mn --custom /home/mininet/fattree.py --topo mytopo --controller=remote,ip=10.0.0.20,port=6633 --switch ovsk,protocols=OpenFlow10

--mac指定虚拟主机的mac地址顺序编号，若不带此参数则随机编号
--controller指定of交换机的控制器
--switch指定虚拟交换机的类型，ovsk表示虚拟交换机为ovs Kernel mode
--custom指定自定义拓扑文件
--topo指定加载拓扑的名字

python fullfattree.py
```
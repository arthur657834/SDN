方法1:
使用vm安装
默认密码:mininet/mininet

方法2:
源码安装
git clone git://github.com/mininet/mininet
/opt/software/mininet/util/install.sh -a

sudo mn --test pingall
mn --version

sudo mn --switch ovs,protocols=OpenFlow13 --controller=remote,ip=10.1.50.175,port=6633

sudo ovs-ofctl dump-flows -O openflow13 s1

图形化配置:
/home/mininet/mininet/examples/miniedit.py

通过选择File-Export Level 2 Script，将其保存为python脚本，以后直接运行python脚本即可重现拓扑，重现拓扑后可在命令行直接操作

mn --controller=remote,ip=10.1.50.175,port=6633 --topo tree,3 
//表示该mininet远程连接控制器，控制器的IP为10.40.150.148，默认控制器端口为6633，并且建立一个三层树形的网络拓扑结构

mn -c
//清mininet的缓存

mininet> links 
//查看链接连接状态，显示OK

mininet> pingall

nodes
dump
net

opendaylight-user@root>log:display

报错:Exception: Error creating interface pair (s2-eth12,s1-eth19): RTNETLINK answers: File exists

解决办法:mn -c

最小的网络拓扑，一个交换机下挂两个主机
mn --topo minimal

每个交换机连接一个主机，交换机间相连接。本例：4个主机，4个交换机。
mn --topo linear,4

```py
from mininet.net import Mininet
from mininet.topo import LinearTopo
Linear4 = LinearTopo(k=4)    #四个交换机，分别下挂一个主机
net = Mininet(topo=Linear4)
net.start()
net.pingAll()
net.stop()
```

每个主机都连接到同一个交换机上。本例：3个主机，一个交换机。
mn --topo single,3
```py
from mininet.net import Mininet
from mininet.topo import SingleSwitchTopo
Single3 = SingleSwitchTopo(k=3)   #一个交换机下挂3个主机
net = Mininet(topo=Single3)
net.start()
net.pingAll()
net.stop()
```

定义深度和扇出形成基于树的拓扑。本例：深度2，扇出2。
mn --topo tree, fanout=2,depth=2
```py
from mininet.net import Mininet
from mininet.topolib import TreeTopo
Tree22 = TreeTopo(depth=2,fanout=2)
net = Mininet(topo=Tree22)
net.start()
net.pingAll()
net.stop()
```

s1.attach(s1,net.get('h3'))
net.get('h3').cmd('ifconfig h3-eth0 10.3')
h1 ping -c1 h3
dumpNodeConnections(net.hosts)


screen mn --custom /opt/fattree.py --topo mytopo --controller=remote,ip=10.1.50.176,port=6653 --switch ovsk,protocols=OpenFlow13


screen mn --topo linear --mac --switch ovsk --controller=none


打开交换机s1和交换机s2的二层                      
ovs-vsctl del-fail-mode s1 

                     
ovs-ofctl dump-flows s1


Quagga软件原名是Zebra是由一个日本开发团队编写的一个以GNU版权方式发布的软件。Quagga项目开始与1996年，当前版本是0.98.4版 可以使用Quagga将Linux机器打造成一台功能完备的路由器。


在BGP消息通告中把BGP邻居作为完全可信的实体，并认为所有从邻居学习到的路由信息都是当前网络拓扑的真实状况。因此当一个攻击者将不属于自己的IP前缀宣告到其他的组织，接收到通告的组织也只是依据自身策略决定到达该IP前缀的下一跳AS，没有机制可以用来验证发布该前缀的组织是否真的拥有该IP前缀。如果选择了攻击者AS作为到达该IP前缀的下一跳地址，则所有到达该IP前缀的流量都会被劫持到攻击者AS，并且受到感染的AS会把该攻击信息继续向其他的AS传播，使得更多的AS受到感染，逐渐形成了BGP劫持攻击。

ex1:
```py
from mininet.net import Mininet
from mininet.node import CPULimitedHost
from mininet.link import TCLink
net = Mininet(host=CPULimitedHost, link=TCLink)
c0 = net.addController()
s0 = net.addSwitch('s0')
h0 = net.addHost('h0')
h1 = net.addHost('h1', cpu=0.5)
h2 = net.addHost('h1', cpu=0.5)
#设置带宽bw、延迟delay、最大队列的大小max_queue_size、损耗率loss。
net.addLink(s0, h0, bw=10, delay='5ms',max_queue_size=1000, loss=10, use_htb=True)
net.addLink(s0, h1)
net.addLink(s0, h2)
net.start()
net.pingAll()
net.stop()
```
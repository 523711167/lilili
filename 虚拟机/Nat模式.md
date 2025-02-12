### Nat模式	

​	Nat模式内网主机通过具有Nat功能路由器（已分配公网IP）连接互联网，内网工具访问互联网，IP数据报文的内网IP+端口会被Nat路由器转化为公网IP+随机端口访问互联网，响应报文通过Nat功能路由器，公网IP+端口会被转换为内网IP+端口。	

​	创建VM虚拟机中使用Nat模式，虚拟机、虚拟DHCP服务器、宿主机（VMnet8的网卡）、Nat适配器通过虚拟交换机连接，组成局域网，虚拟机的IP、网关配置通过DHCP服务器自动配置内网IP，通过虚拟Nat转换IP（192.168.1.101）连接互联网。

![image-20250210200917760](/Users/xixipeng/Library/Application Support/typora-user-images/image-20250210200917760.png)

### 参考链接

[1]: https://blog.csdn.net/A79800/article/details/139777513	"CSND"

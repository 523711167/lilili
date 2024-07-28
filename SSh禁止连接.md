### SSh禁止连接

1. 用户名密码错误

2. ssh服务没有启动

   ```shell
   systemctl status sshd
   ```

3. ssh配置文件禁止Root用户连接

   ```shell
   cd /etc/ssh/
   vi sshd_config
   手动添加
   PermitRootLogin yes
   ```

   
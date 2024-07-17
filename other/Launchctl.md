### Launchctl

​	macOS操作系统的命令行管理工具，对系统服务进行统一的管理，负责启动、停止和管理系统级和用户级的应用程序、脚本、守护进程和其他进程。

##### 配置

launchd 通过 .plist 配置文件来管理任务。这些文件通常位于以下目录：

- /System/Library/LaunchDaemons/：存放系统级守护进程配置文件，由系统所有者或管理员管理。
- /Library/LaunchDaemons/：存放第三方应用程序的系统级守护进程配置文件。
- /System/Library/LaunchAgents/：存放系统级代理配置文件。
- /Library/LaunchAgents/：存放第三方应用程序的用户级代理配置文件。
- ~/Library/LaunchAgents/：存放用户级代理配置文件，只影响当前用户
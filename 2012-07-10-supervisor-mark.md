#Supervisor常用命令
- date: 2012-7-10

---
初始启动：`supervisord`
启动进程：`supervisorctl start <name>`
停止进程：`supervisorctl stop <name>`
重启进程：`supervisorctl restart <name>`
重新载入：`supervisorctl reload`
重新载入会读取最新配置并重新启动所有进程。
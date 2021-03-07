# MySQL

密码root

**卸载：**

​		卸载MySQL后残留数据在：datadir="C:/ProgramData/MySQL/MySQL Server 5.5/Data/"必须卸载后才能重新安装。

**服务启动：**

​		方式一：cmd-->services。msc 打开服务窗口，手动开关

​		方式二：以管理员身份运行cmd，使用net start mysql启动服务，使用net stop mysql停止服务

**MySQL登录：**

​		1.mysql -uroot -p（password）：直接(输入密码)登录

​		2.mysql -h(IP) -uroot -p(连接目标的密码)

​		3.mysql --host=IP --user==root --password=连接目标的密码

**MySQl退出：**

​		1.exit

​		2.quit


# 1 安装chrome

链接: http://pan.baidu.com/s/1c0eY66c 密码: o58b

chrome要求在非root用户下使用。

`sudo yum localinstall google-chrome-stable-39.0.2171.71-1.x86_64.rpm`


# 2 安装switchysharp

将goagent/local目录下的SwitchySharp.crx拖到设置->扩展程序。安装成功后导入goagent/local的SwitchyOptions.bak。

# 3 安装goagent

goagent设置请参照常规设置，请自行搜索。

将设置好的goagent放置fedora上。

`cd /home/wisely/goagent/local`

`python proxy.py`  启动goagent



# 4 goagent自启动

为了避免每次手动启动goagent，特编制systemd的service。

在root用户下：

`cd /etc/systemd/system`

`vi goagent.service`

--------------------------------------------------

```
[Unit]
Description=goagent
After=network.target

[Service]
Type=simple
ExecStart=/bin/sh -c 'cd /home/wisely/goagent/local/;python proxy.py'
ExecStop=/bin/kill -15 $MAINPID
StandardOutput=null

[Install]
WantedBy=multi-user.target
```
----------------------------------------------------

`systemctl enable goagent.service`

`systemctl start goagent.service`


这时goagent会开机启动了

停止goagent

`systemctl stop goagent.service`


# 5 错误

遇到安装错误，请用`yum install 缺少的包名`




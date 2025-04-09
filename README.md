## 部署VPS服务器
下载[FinalShell](https://www.hostbuf.com/t/988.html)，输入VPS的IP地址、用户名（通常是root）和密码，进行连接。
![连接图片](https://github.com/0594/rustdesk-server/blob/master/FinalShell.png)
如果系统开通了防火墙，如Vultr服务器，就要通过：sudo ufw disable 关闭VPS的防火墙。

访问RustDesk的服务端下载页面，采用wget 分别下载hbbr和hbbs文件。
通过SSH客户端上传这两个文件到VPS，解压并安装RustDesk服务端。

```bash
wget https://github.com/0594/rustdesk-server/releases/download/1.1.14/rustdesk-server-hbbr_1.1.14_amd64.deb 
wget https://github.com/0594/rustdesk-server/releases/download/1.1.14/rustdesk-server-hbbs_1.1.14_amd64.deb
```
## 安装RustDesk客户端
下载完客户端后，我们可以使用管理员权限安装，安装代码如下：

```bash
sudo dpkg -i rustdesk-server-hbbr_1.1.14_amd64.deb 

sudo dpkg -i rustdesk-server-hbbs_1.1.14_amd64.deb
```

安装完成后，可以测试服务是否生效。
```bash
sudo systemctl status rustdesk-hbbr.service 

sudo systemctl status rustdesk-hbbs.service 
```

## 获取秘钥key
测试生效后，可以通过以下代码获取秘钥key。
```bash
sudo cat /lib/systemd/system/rustdesk-hbbr.service
sudo cat /lib/systemd/system/rustdesk-hbbs.service
sudo cat /var/log/rustdesk-server/hbbs.log
```
秘钥key在hbbs.log第二行
这个key是配置我们RustDesk服务器的关键，所以一定要保存好备用。
## 客户端下载
[https://github.com/rustdesk/rustdesk/releases](https://github.com/rustdesk/rustdesk/releases)

## 配置RustDesk客户端
打开 RustDesk 客户端，在客户端设置-网络-解锁网络设置-ID/中继服务器。
ID服务器和中继服务器填写VPS IP，API服务器留空，Key填写上面获取到的密钥，最后再点击应用。

![配置RustDesk客户端](https://github.com/0594/rustdesk-server/blob/master/rustdesk.set.png)

## 连接其他电脑
确保其他电脑的 RustDesk 客户端也进行同样配置，并保证IP和Key配置正确，注意要使用相同的 ID 服务器和密钥，否则无法连接。

## 注意事项

- 确保VPS的安全性，定期更新系统和软件。
- 考虑到隐私和数据安全，建议使用加密连接。
- 如果需要在公网环境下使用，确保VPS的端口正确开放。
- 对于大规模使用，可能需要考虑负载均衡和更高级的网络配置。

## 总结
通过上述步骤，你可以成功搭建并使用自己的RustDesk服务器，从而实现快速、稳定的远程桌面连接。
这不仅能够避免使用官方服务器可能带来的速度慢和连接失败的问题，还能节省成本，尤其是在连接海外网络时。
希望这篇文章能够帮助你顺利搭建自己的RustDesk服务器


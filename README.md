#介绍

使用 `curl -sSL https://shipyard-project.com/deploy | bash -s` 创建shipyad管理界面，但是非加密传输，而通过自签证书，很多游览器有提醒不安全，使用此前端代理，就可以使用认证的证书在前端反向代理

假设你购买的证书后，通过下面命令建立pem,注意：这里的pem 文件是下面两个文件合并而成：

	cat servername.crt servername.key |tee servername.pem 

#用法

	docker run -d --restart=always \
          -p 443:443 -p 80:80 \
          --name shipyard-haproxy \
          --link shipyard-controller:controller \
          -v /path/to/youdomain.pem:/servername.pem  lihaixin/shipyard-haproxy

或者使用我自己的证书，通过https://ssl.lihaixin.name 访问

	docker run -d --restart=always \
          -p 443:443 -p 80:80 \
          --name shipyard-haproxy \
          --link shipyard-controller:controller lihaixin/shipyard-haproxy


步骤1： 服务器端一键部署v2ray服务 bash <(curl -L https://raw.githubusercontent.com/v2fly/fhs-install-v2ray/master/install-release.sh)

步骤2： 找到v2ray的配置目录 cd /usr/local/etc/v2ray/

步骤3:编辑配置文件 config.json 备注：inbounds就是入站规则，其中的"id": "b831381d-6324-4d53-ad4f-8cda48b30333"这里的id是客户端连接服务器的主要凭证 客户端连接时要用到这个id 
{
	"log": {
		"access": "/var/log/v2ray/access.log",
		"error": "/var/log/v2ray/error.log",
		"loglevel": "warning"

	},
	"inbounds": [{
		"port": 10086,
		"protocol": "vmess",
		"tag": "10086端口",
		"settings": {
			"clients": [{
				"id": "b831381d-6324-4d53-ad4f-8cda48b30333"
			}]
		}
	}],
	"outbounds": [{
		"protocol": "freedom"
	}]
}

步骤4：配置端口 启动服务 iptables -I INPUT -p tcp --dport 10086 -j ACCEPT

iptables -L

systemctl start v2ray


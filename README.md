# 247.Streams.360
Playing with Ant-media server and the nginx rtmp module to make live broadcasts of mp4 files.
Working well on ubuntu server 16.04 had package issues on 18.

Installing Ant-Media Server

You will need a fresh install of Ubuntu 16.04, I'm using a cheap VPS for messing about

sudo apt-get update && apt-get upgrade

Download the Ant-media server install zip

wget https://github.com/ant-media/Ant-Media-Server/releases/download/ams-v1.7.2/ant-media-server-community-1.7.2-20190602_1447.zip

Download the install .sh into the same folder as the install zip

wget https://raw.githubusercontent.com/ant-media/Scripts/master/install_ant-media-server.sh

then run the following command 

./install_ant-media-server.sh ant-media-server-community-1.7.2-20190602_1447.zip

it will install in a few minutes, you will need to open the following ports 

sudo ufw allow ssh

sudo ufw allow 22

sudo ufw allow 5000:65000/tcp

sudo ufw allow 5000:65000/udp

sudo ufw allow 1935/tcp

sudo ufw allow 5080/tcp

sudo ufw allow 5443/tcp

sudo ufw allow 5554/tcp

ufw enable 

Its also a requirement for Ant-media server to reroute a couple of ports using iptables and make them persistant

sudo iptables -t nat -A PREROUTING -p tcp --dport 80 -j REDIRECT --to-port 5080

sudo iptables -t nat -A PREROUTING -p tcp --dport 443 -j REDIRECT --to-port 5443

sudo apt-get install iptables-persistent

sudo sh -c "iptables-save > /etc/iptables/rules.v4"

Thats it, now open a browser and navigate to your IP and make a user and login .

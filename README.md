apt update && apt upgrade -y

apt install -y curl apt-transport-https gnupg

curl -fsSL https://repos.pufferpanel.com/key.asc | gpg --dearmor -o /usr/share/keyrings/pufferpanel.gpg

echo "deb [signed-by=/usr/share/keyrings/pufferpanel.gpg] https://repos.pufferpanel.com/ubuntu $(lsb_release -cs) main" | tee /etc/apt/sources.list.d/pufferpanel.list

apt update
apt install -y pufferpanel

systemctl enable pufferpanel
systemctl start pufferpanel

pufferpanel user add


netstat -tuln | grep 8080

systemctl restart pufferpanel

systemctl status pufferpanel

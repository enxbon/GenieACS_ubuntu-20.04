`GenieACS ubuntu 20.04`

=========== Virtual Parameter ACS ===============

# Install NodeJS (v18.0)
```
apt update && sudo apt upgrade -y
```
```
apt install -y curl git build-essential redis-server
```
```
systemctl enable redis
```
```
systemctl start redis
```
```
curl -fsSL https://deb.nodesource.com/setup_18.x | sudo -E bash -
```
```
apt install -y nodejs
```
# Install MongoDB (v6.0)
```
wget -qO - https://pgp.mongodb.com/server-6.0.asc | sudo gpg --dearmor -o /usr/share/keyrings/mongodb-server-6.0.gpg
```
```
echo "deb [ signed-by=/usr/share/keyrings/mongodb-server-6.0.gpg ] https://repo.mongodb.org/apt/ubuntu focal/mongodb-org/6.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-6.0.list
```
```
apt update
```
```
apt install -y mongodb-org
```
```
systemctl enable mongod
```
```
systemctl start mongod
```
# Install GenieACS (v6.0)
```
sudo adduser --system --group genieacs
```
```
cd /opt
```
```
sudo git clone https://github.com/genieacs/genieacs.git
```
```
sudo chown -R genieacs:genieacs genieacs
```
```
cd genieacs
```
```
sudo -u genieacs npm install
```
```
sudo -u genieacs npm run build
```
Create systemd service files
1. genieacs-cwmp.service :
```
sudo nano /etc/systemd/system/genieacs-cwmp.service
```
```
[Unit]
Description=GenieACS CWMP
After=network.target

[Service]
User=genieacs
WorkingDirectory=/opt/genieacs
ExecStart=/usr/bin/node /opt/genieacs/dist/bin/genieacs-cwmp
Restart=always

[Install]
WantedBy=multi-user.target
```
2. genieacs-nbi.service
```
sudo nano /etc/systemd/system/genieacs-nbi.service
```
```
[Unit]
Description=GenieACS NBI
After=network.target

[Service]
User=genieacs
WorkingDirectory=/opt/genieacs
ExecStart=/usr/bin/node /opt/genieacs/dist/bin/genieacs-nbi
Restart=always

[Install]
WantedBy=multi-user.target
```
3. genieacs-fs.service
```
sudo nano /etc/systemd/system/genieacs-fs.service
```
```
[Unit]
Description=GenieACS FS
After=network.target

[Service]
User=genieacs
WorkingDirectory=/opt/genieacs
ExecStart=/usr/bin/node /opt/genieacs/dist/bin/genieacs-fs
Restart=always

[Install]
WantedBy=multi-user.target
```
4. genieacs-ui.service
```
sudo nano /etc/systemd/system/genieacs-ui.service
```
```
[Unit]
Description=GenieACS UI
After=network.target

[Service]
User=genieacs
WorkingDirectory=/opt/genieacs
ExecStart=/usr/bin/node /opt/genieacs/dist/bin/genieacs-ui
Restart=always

[Install]
WantedBy=multi-user.target
```
# Enable and start services
```
systemctl enable genieacs-cwmp
```
```
systemctl enable genieacs-nbi
```
```
systemctl enable genieacs-fs
```
```
systemctl enable genieacs-ui
```
```
systemctl start genieacs-cwmp
```
```
systemctl start genieacs-nbi
```
```
systemctl start genieacs-fs
```
```
systemctl start genieacs-ui
```
```
systemctl status genieacs-cwmp
```
```
systemctl status genieacs-nbi
```
```
systemctl status genieacs-fs
```
```
systemctl status genieacs-ui
```
```
systemctl status mongod.service
```
```
systemctl
```
```
systemctl
```


============== info 085 ==================

🌐 Access GenieACS
```
[systemctl](http://<your-server-ip>:3000)
```
🤝 Kontribusi
Kontribusi selalu diterima! Silakan buat pull request atau laporkan issue jika menemukan bug.

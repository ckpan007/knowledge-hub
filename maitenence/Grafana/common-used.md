# Common used command
```sh
# Start the Grafana
systemctl daemon-reload
systemctl start grafana-server
systemctl status grafana-server

# Enable the systemd service so that Grafana starts at boot
sudo systemctl enable grafana-server.service
```

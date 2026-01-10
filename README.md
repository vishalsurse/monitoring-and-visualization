# PromGraf

In this repository Grafana, Loki, Promtail, Prometheus, and cAdvisor for monitoring and visualization purposes. Below are the steps to install and configure these tools.



## Install Grafana on AWS Using EC2
```bash
sudo yum install -y apt-transport-https
sudo yum install -y software-properties-common wget
sudo wget -q -O /etc/pki/rpm-gpg/RPM-GPG-KEY-grafana https://rpm.grafana.com/gpg.key
```

```bash
# Use dnf instead of yum:
sudo dnf install -y wget grafana
sudo systemctl start grafana-server
sudo systemctl enable grafana-server
sudo systemctl status grafana-server
Install Loki and Promtail using Docker
```
# Download Loki Config
```
wget https://raw.githubusercontent.com/grafana/loki/v2.8.0/cmd/loki/loki-local-config.yaml -O loki-config.yaml
```
# Run Loki Docker container
```
docker run -d --name loki -v $(pwd):/mnt/config -p 3100:3100 grafana/loki:2.8.0 --config.file=/mnt/config/loki-config.yaml
```
# Download Promtail Config
```
wget https://raw.githubusercontent.com/grafana/loki/v2.8.0/clients/cmd/promtail/promtail-docker-config.yaml -O promtail-config.yaml
```
# Run Promtail Docker container
```
docker run -d --name promtail -v $(pwd):/mnt/config -v /var/log:/var/log --link loki grafana/promtail:2.8.0 --config.file=/mnt/config/promtail-config.yaml
```
Install Prometheus and cAdvisor
# Download the prometheus config file

```bash
wget https://raw.githubusercontent.com/prometheus/prometheus/main/documentation/examples/prometheus.yml
```
# Install Prometheus using Docker
```
docker run -d --name=prometheus -p 9090:9090 -v <PATH_TO_prometheus.yml_FILE>:/etc/prometheus/prometheus.yml prom/prometheus --config.file=/etc/prometheus/prometheus.yml
```

# Verify
```
docker ps
```

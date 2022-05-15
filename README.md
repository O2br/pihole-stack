# Pi-hole Stack


- **[Pi-hole](https://pi-hole.net/)**: bloqueador de anúncios em nível de rede que atua como um buraco negro de DNS e, opcionalmente, um servidor DHCP.

- **[Prometheus](https://prometheus.io/)**: sistema de monitoramento para serviços e aplicações que coleta as métricas de seus alvos em determinados intervalos.

- **[Node exporter](https://github.com/prometheus/node_exporter)**: exportador do Prometheus para hardware e métricas de sistema operacional

- **[Pi-hole exporter](https://github.com/eko/pihole-exporter)**: exportador do Prometheus para as métricas do Pi-hole

- **[Grafana](https://grafana.com/)**: plataforma para visualizar e analisar métricas por meio de gráficos.

- **[AlertManager (opcional)](https://github.com/prometheus/alertmanager)**: trabalha de forma integrada com a Prometheus para avaliar regras de alerta e enviar notificações por e-mail, Jira, Slack, e outros sistemas suportados. 

## Pré-requisitos

- [Docker](https://docs.docker.com/get-docker/)
- [Docker Compose](https://docs.docker.com/compose/install/)

## Como usar?
```sh
git clone https://github.com/marcelobaptista/pihole-stack.git && cd pihole-stack
```

## No arquivo *docker-compose.yml* editar a seguinte linha caso esteja usando plataforma ARM
```sh
 onedr0p/pihole-exporter:v1.0.0 por ekofr/pihole-exporter
```

### Editar a variável ROOT no arquivo .env para o caminho desejado
```sh 
nano .env

TZ=America/Sao_Paulo
PUID=1000
PGID=1000
ROOT=/etc/pihole-stack
```
### Copiar os arquivos necessários para o caminho escolhido anteriormente 
```sh 
cp -r {alertmanager,prometheus} /etc/pihole-stack/
```
### Editar o arquivo pihole.env para escolher a senha do frontend e os DNS
```sh 
nano pihole.env

WEBPASSWORD=123 #senha do frontend Pi-hole
PIHOLE_DNS_=1.1.1.3;1.0.0.3
```
### Editar o arquivo pihole-exporter.env 
```sh 
nano pihole-exporter.env

PIHOLE_HOSTNAME=IP_AQUI #IP do Pi-hole
PIHOLE_PASSWORD=123456 #senha do frontend Pi-hole
INTERVAL=30s
PORT=9617
```
### Editar o arquivo grafana.env 
```sh 
nano grafana.env

GF_SECURITY_ADMIN_USER=admin #usuário admin no frontend
GF_SECURITY_ADMIN_PASSWORD=passw0rd #senha do usuário admin no frontend
GF_USERS_DEFAULT_THEME=dark #tema padrão
GF_USERS_ALLOW_SIGN_UP=false
GF_USERS_ALLOW_ORG_CREATE=false
GF_AUTH_ANONYMOUS_ENABLED=true
GF_INSTALL_PLUGINS=alexanderzobnin-zabbix-app,camptocamp-prometheus-alertmanager-datasource,grafana-piechart-panel
```
### Executar os containers
```sh 
docker-compose up -d
```

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
### Executar os containers
```sh 
docker-compose up -d
```

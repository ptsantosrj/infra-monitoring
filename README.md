
# 📊 Infraestrutura de Monitoramento e Observabilidade

Este projeto entrega uma stack completa de **monitoramento e observabilidade**, ideal para ambientes modernos, com componentes integrados via Docker Compose.

---

## 🔧 Componentes da Stack

| Componente         | Função                                                  |
|--------------------|----------------------------------------------------------|
| **Zabbix**         | Monitoramento tradicional (SNMP, agente, hosts)          |
| **Prometheus**     | Coleta de métricas (Node Exporter, Blackbox, etc.)       |
| **Grafana**        | Dashboards unificados com dados do Prometheus, Loki etc. |
| **Grafana Loki**   | Coleta e consulta de logs                                |
| **Promtail**       | Envio de logs para o Loki                                |
| **Alertmanager**   | Gerenciamento de alertas do Prometheus                   |
| **Node Exporter**  | Métricas básicas dos sistemas operacionais               |
| **Blackbox Exporter** | Teste de endpoints HTTP, TCP, ICMP                  |
| **PostgreSQL**     | Banco de dados do Zabbix                                 |

---

## 🚀 Subindo o Ambiente

> Pré-requisitos: Docker e Docker Compose instalados.

```
*Clone o repositorio
bash
git clone https://github.com/seuusuario/infra-monitoring.git
cd infra-monitoring

*Configure o arquivo `.env` com os dados do banco MySQL gerenciado no Azure:
cp .env.example .env

*Edite `.env` e insira:
- Host do banco (ex: `meubanco.mysql.database.azure.com`)
- Usuário/senha
- Nome do banco (ex: `zabbix`)

*Suba a stack:
docker-compose up -d

* Ip dos containers
docker inspect -f '{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}' nome_ou_id_do_container
```
---

## 🌐 Acesso aos Serviços

| Serviço         | URL                       | Usuário / Senha          |
|----------------|----------------------------|--------------------------|
| Grafana        | http://localhost:3000      | `admin` / `admin`        |
| Prometheus     | http://localhost:9090      | -                        |
| Alertmanager   | http://localhost:9093      | -                        |
| Zabbix UI      | http://localhost:8080      | `Admin` / `zabbix`       |
| Node Exporter  | http://localhost:9100/metrics | -                     |
| Loki           | http://localhost:3100      | -                        |
| Promtail       | http://localhost:9080      | -                        |
| Blackbox Exporter | http://localhost:9115  | -                        |

---

## 📁 Estrutura dos Diretórios

```
infra-monitoring/
├── .env.example
├── docker-compose.yml
├── prometheus/
│   ├── prometheus.yml
│   ├── alert.rules.yml
│   └── alertmanager.yml
├── grafana/
│   └── provisioning/
│       └── datasources/
│           └── all.yml
├── loki/
│   └── config.yml
├── promtail/
│   └── config.yml
```

---

## 📌 Notas

- O plugin do Zabbix para Grafana precisa ser ativado via UI.
  - docker exec -it nome_do_container_grafana /bin/bash
  - grafana-cli plugins install alexanderzobnin-zabbix-app
  - docker restart nome_do_container_grafana
  
- As configurações estão com foco em ambiente de **desenvolvimento**. Para produção, recomenda-se:
  - Configurações persistentes de volumes
  - TLS e autenticação
  - Hardening de acesso às interfaces
  - Monitoramento de logs e métricas de aplicações específicas

---

## 📃 Licença

Este projeto está licenciado sob a [MIT License](LICENSE).

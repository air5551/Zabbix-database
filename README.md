# Postgres with Zabbix

> [!WARNING]
> This Repo is for testing and I work on it **WHEN** I feel like it

A little note that I only intend to support podman while docker comes second


### Installation
```yaml
services:
    zabbix-web:
        image: zabbix/zabbix-web-nginx-pgsql:ol-7.4-latest
        environment:
            - PHP_TZ="America/New_York"
            - ZBX_SERVER_HOST="zabbix-server"
            - POSTGRES_USER="postgres"
            - POSTGRES_PASSWORD=${PG_PASS}
            - DB_SERVER_HOST=zabbix-database
            - ZBX_SERVER_NAME=Zabbix
        container_name: zabbix-web-nginx-pgsql
      
    
    db:
      image: postgres
      restart: "unless-stopped"
      container_name: zabbix-database 
      volumes:
        - ./server.sql.gz:/docker-entrypoint-initdb.d/server.sql.gz
      ports:
        - 5432:5432
      environment:
        - POSTGRES_PASSWORD=${PG_PASS}
      
    
    zabbix-server:
      container_name: zabbix-server
      image: zabbix/zabbix-server-pgsql:ol-7.4.0
      environment:
        - DB_SERVER_HOST=zabbix-database
        - POSTGRES_PASSWORD=${PG_PASS}
      ports:
        - 10051:10051
        
    

```

Before running the container a Postgres password has to be generated
```bash
echo "PG_PASS=$(openssl rand -base64 36 | tr -d '\n')" >> .env

```
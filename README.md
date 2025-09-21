# Postgres with Zabbix

> [!WARNING]
> This Repo is for testing and I work on it **WHEN** I feel like it




### Installation
```yaml


```

Before running the container a Postgres password has to be generated
```bash
echo "PG_PASS=$(openssl rand -base64 36 | tr -d '\n')" >> .env

```


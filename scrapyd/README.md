scrapyd
=======

[Scrapyd](https://scrapyd.readthedocs.io/) — это сервис для развертывания и запуска [Scrapy](https://docs.scrapy.org/en/latest/index.html#)-проектов. Позволяет вам развертывать(загрузить) ваши проекты и
управлять ими с помощью JSON API

Этот образ основан `debian:bookworm`, предустановлены следующие пакеты:

- [scrapy](https://docs.scrapy.org/en/latest/index.html#)
- [scrapyd](https://scrapyd.readthedocs.io/)
- [scrapy-poet](https://scrapy-poet.readthedocs.io/en/stable/#)
- [scrapy-playwright](https://github.com/scrapy-plugins/scrapy-playwright)

Также предустановлен fitefox и все зависимости

## docker-compose.yml

```yaml
services:

  scrapyd:
    image: suvorinov/scrapyd
    container_name: scrapyd
    env_file:
      - .env
    ports:
      - "6800:6800"
    volumes:
      - ${HOME}/var/www/assets:/root/var/www/assets  
      - ${HOME}/.cache/scrapyd:/var/lib/scrapyd
      - /usr/local/lib/python3.11/dist-packages
    restart: unless-stopped
```

## Запустить сервис

Следующая команда запустит scrapyd:

```bash
docker compose up -d
```

После развертывания scrapyd сервис доступен `http://your-ip:6800`.
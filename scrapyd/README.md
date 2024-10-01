scrapyd
=======

[Scrapyd](https://scrapyd.readthedocs.io/) — это приложение для развертывания и запуска [Scrapy](https://docs.scrapy.org/en/latest/index.html#)-проектов. Оно позволяет вам развертывать(загружать) ваши проекты и
управлять ими с помощью JSON API

Этот образ основан `debian:bookworm`, предустановлены следующие пакеты:

- scrapy
- scrapyd
- scrapy-poet
- scrapy-playwright


## Запустить сервис

Следующая команда запустит scrapyd:

```bash
docker compose up -d
```

После развертывания scrapyd сервис доступен `http://your-ip:6800`.
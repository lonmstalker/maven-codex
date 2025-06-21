# Maven Codex Setup

![CI](https://github.com/lonmstalker/maven-codex-setup/actions/workflows/build.yml/badge.svg)
![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)

> Пошаговое руководство по установке фиксированной версии Apache Maven
> и настройке прокси для OpenAI Codex.
# Что делает скрипт

* Скачивает актуальную стабильную версию Maven 3 напрямую с `dlcdn.apache.org`;
* распаковывает её в `/opt` и создаёт симлинк `/usr/local/bin/mvn`, чтобы Maven был в `$PATH`;
* генерирует `~/.m2/settings.xml`, подставляя значения прокси из **переменных окружения**;
* выводит итоговый `settings.xml` в stdout — удобно для логов CI.

---

## Быстрый старт

```bash
git clone https://github.com/<your-org>/maven-codex-setup.git
cd maven-codex-setup

# при необходимости переопределите переменные окружения
export PROXY_HOST=proxy
export PROXY_PORT=8080

chmod +x setup-maven.sh
sudo ./setup-maven.sh
```

*(вставьте как есть ― внутри README будет двойной блок-код)*

---

### Переменные прокси

| Переменная        | Значение по умолчанию | Что означает |
|-------------------|-----------------------|--------------|
| `PROXY_HOST`      | `proxy`               | DNS-имя или IP прокси-сервера |
| `PROXY_PORT`      | `8080`                | Порт прокси |
| `PROXY_SCHEME`    | `http`                | `http` или `https` |
| `PROXY_ID`        | `corp-proxy`          | Уникальный идентификатор прокси |
| `NON_PROXY_HOSTS` | `localhost\|*.local\|127.0.0.1\|::1` | Шаблоны хостов, минующих прокси |

## Разрешённые домены для репозиториев

Домен | Оставить? | Почему
------|-----------|-------
`repo.maven.apache.org` | **Да** | Maven Central (основной адрес)
`repo1.maven.org`       | **Да** | CNAME старого Central, встречается в зависимостях
`repository.apache.org` | **Да** | Release / snapshot репозитории Apache-проектов
`maven.pkg.github.com`  | **Да** | GitHub Packages — артефакты ваших приватных модулей
`sonatype.org`          | **Да** | OSSRH staging перед выкладкой в Central
`github.io`             | По ситуации | Иногда размещают статические JAR; не нужно — удалите
`core.telegram.org`     | **Нет** | Maven-артефактов нет
`telegram.org`          | **Нет** | То же
`nist.gov`              | **Нет** | Не используется как Maven-репозиторий

## Файловая структура репозитория
.
├── setup-maven.sh     # Скрипт установки Maven + settings.xml
├── README.md          # Этот файл
└── LICENSE            # MIT-лицензия

---

### Лицензия

Проект распространяется под лицензией **MIT** — см. файл `LICENSE`.

## Как опубликовать на GitHub

1. **Создать репозиторий**
   В веб-интерфейсе GitHub нажмите **New → Repository**, задайте имя
   (`maven-codex-setup`), выберите публичный/приватный, добавьте лицензию.

2. **Залить код**

```bash
cd /path/to/maven-codex-setup       # папка со скриптом и README
git init -b main
git add setup-maven.sh README.md LICENSE
git commit -m "Initial commit: Maven setup script and docs"
git remote add origin git@github.com:<your-name>/maven-codex-setup.git
git push -u origin main
```


---

## [LICENSE](LICENSE)

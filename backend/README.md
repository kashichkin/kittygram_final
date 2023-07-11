# Kittygram - социальная сеть для владельцев котиков

Kittygramm владельцам котиков позволяет размещать фото, кличку, цвет, год рождения и разнообразные достижения своих питомцев.

## URL
Проект развернут на сайте:
https://romainkashichkin.ddns.net/
## Технологии

Проект - Django, Django REST framework.

Развертывание - Linux, Nginx, Gunicorn, HTTPS, Docker,  GitHub Actions.

## Установка

### Вручную

Установите Git. Установите Docker.

Для клонирования репозитория по SSH выполните команду git clone git@github.com:kashichkin/kittygram_final.git.

Создайте в папке kittygram_final файл .env. Заполните по образцу, размещенному в файле .env.example

В папке kittygram_final выполните команду docker compose up -d.

Выполните миграции и сбор статики:

```yaml
docker compose -f docker-compose.production.yml exec backend python manage.py migrate
docker compose -f docker-compose.production.yml exec backend python manage.py collectstatic
```
### Автоматическая доставка и развертывание на сервере

В файле kittygram_workflow.yml записан сценарий автоматического тестирования, доставки и развертывания проекта. Сценарий активируется при сохранении коммита в ветку main. Для использования сценария необходимы нижеописанные действия.

Зарегиструйтесь на сервисах Github https://github.com/ и DockerHub https://hub.docker.com/

Создайте на сервере папку kittygram.

Сделайте форк проекта. Создайте в репозитории папку kittygram_final/.github/workflows/. Скопируйте содержимое файла kittygram_workflow.yml в файл main.yml в этой папке.

В настройках своего репозитория в разделе Secrets and variables -> Actions создайте следующие Secrets:

DOCKER_USERNAME - имя пользователя на DockerHub

DOCKER_PASSWORD - пароль пользователя на DockerHub

HOST - адрес вашего сервера

SSH_KEY - секретный ssh-ключ для дорступа к вашему серверу

HOST_USER - пользователь на вашем сервере (необходимы права на выполнение команды sudo)

SSH_PASSPHRASE - пароль пользователя

TELEGRAM_TO - id пользователя Телеграм, которому будет отправлено сообщение об успешном исполнении сценария.

TELEGRAM_TOKEN - токен бота, от имени которого будет отпарвлено сообщение.

POSTGRES_DB= имя базы данных

POSTGRES_USER=пользователь базы данных

POSTGRES_PASSWORD=пароль пользователя базы данных

DB_HOST=имя контейнера базы данных
DB_PORT=порт базы данных

SECRET_KEY=секретный ключ Джанго

ALLOWED_HOSTS=разрешенные хосты, 127.0.0.1,localhost,ваш-домен

DEBUG = режим отладки

Сохраните изменения в ветку main. Проект будет автоматичесмки протестирован, доставлен на ваш сервер и развернут.
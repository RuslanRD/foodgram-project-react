# praktikum_new_diplom
### Описание проекта:
Проект «Продуктовый помощник». Данный сервис позволяет пользователям публиковать рецепты, подписываться на публикации других пользователей, добавлять понравившиеся рецепты в список «Избранное», а перед походом в магазин скачивать сводный список продуктов, необходимых для приготовления одного или нескольких выбранных блюд.
### Технологии
Python 3.8.5
Django 3.0.5
Docker 20.10.12
### Шаблон наполнения env-файла:
```DB_ENGINE=django.db.backends.postgresql # указываем, что работаем с postgresql
```
```
DB_NAME=postgres # имя базы данных
POSTGRES_USER=postgres # логин для подключения к базе данных
```
```
POSTGRES_PASSWORD=postgres # пароль для подключения к БД (установите свой)
```
```
DB_HOST=db # название сервиса (контейнера)
```
```
DB_PORT=5432 # порт для подключения к БД
```
### Развертывание на удаленном сервере (ubuntu):
* Выполните вход на свой удаленный сервер по ssh ключу:
```
ssh your_login@pu.bl.ic.ip
```
* Обновите системы командой:
```
sudo apt update
```
* Обновите установленные в системе пакеты и установите обновления безопасности:
```
sudo apt upgrade -y
```
* На сервер нужно установить:
  * менеджер пакетов pip;
  * утилиту для создания виртуального окружения venv;
  * систему контроля версий git, чтобы клонировать ваш проект;
  * docker;
  * docker-compose.
  Выполните команды:
```
sudo apt install python3-pip python3-venv git -y
sudo apt install docker.io
sudo curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
```
* Склонируйте репозиторий на удаленныый сервер:
```
https://github.com/RuslanRD/foodgram-project-react.git
```
* Перейдите в директорию с проектом. Активируйте виртуальное окружение и установите пакеты из requirements.txt:
```
cd foodgram-project-react
python3 -m venv venv
source venv/bin/activate
python -m pip install -r requirements.txt
```
* Перейдите в директорию foodgram-project-react/infra. 
```
cd foodgram-project-react/infra 
```
* Cоздайте .env файл:
```
sudo nano .env
```
* Наполните .env следюущими данными:
```
DB_ENGINE=<django.db.backends.postgresql>
DB_NAME=<имя базы данных postgres>
DB_USER=<пользователь бд>
DB_PASSWORD=<пароль>
DB_HOST=<db>
DB_PORT=<5432>
SECRET_KEY=<секретный ключ проекта django>
```
* Из директории foodgram-project-react/infra выполните следующие команды для развертывания проекта:
```
sudo docker-compose up -d --build
sudo docker-compose exec backend python manage.py migrate
sudo docker-compose exec backend ./manage.py collectstatic --no-input
sudo docker-compose exec backend python manage.py loaddata data/data_for_project.json
# если хотите заполнить проект своими данными - команду loaddata выполнять не нужно.
sudo docker-compose exec backend python manage.py createsuperuser
```
### Адрес проекта:
http://178.154.225.6/recipes или
http://foodgramrrd.hopto.org/recipes
### Автор проекта:
https://github.com/RuslanRD
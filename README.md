## Пример использования ```nginx-proxy-manager```
В данном примере покажу настройку связки nginx-proxy-manager и Вашего docker контейнера

В примере приведены 2 любых приложения (PHP + Nginx)

По логике nginx-proxy будет прокидывать трафик в контейнер nginx

---------------

Для начала нужно настроить nginx-proxy-manager.

Для этого заходим в proxy. Редактируем файл (docker-compose.yml) - меняя данный для DB. Вызываем ```docker-compose up -d``` - флаг -d нужен, чтобы запустить процес в фоновом режиме.

Далее запускаем свой проект, к примеру first_app. И так же запускаем проект через ```docker-compose up -d --build```. В итоге у нас поднято два проекта (важно что бы у них была одна сеть с nginx-proxy-manager, в примере это default)
Переходим по адресу localhost:81 (или "IP адрес сервера":81) и настраиваем админ панель

---------------

Добавляем домен к нашему nginx-proxy

![first](https://user-images.githubusercontent.com/69340849/166409142-f9c2fe85-a627-4def-9f9c-f1183b18cea8.png)


Добавляем SSL Сертификат

![second](https://user-images.githubusercontent.com/69340849/166409174-0c60fa2c-32b3-49af-aa87-f1a22f549120.png)

Теперь в docker-compose (nginx-proxy) у сервиса app убираем порт 81:81. Сервис теперь будет доступен по адресу "Ваш домер"

Все proxy настроили, теперь нужно проксировать трафик с необходимого домена на нужный контейнер nginx

Возможно будут проблемы с настройкой nginx-proxy-manager, более подробно написано тут https://github.com/NginxProxyManager/nginx-proxy-manager и тут https://nginxproxymanager.com/setup/#running-the-app

---------------

Далее аналогично настраиваем нужный нам домен, и в "Forward Hostname / IP" указываем название контейнера нашего сервиса, к примеру ```nginx-app1``` и порт 80
Теперь nginx-proxy будет направлять весь трафик с данного домена, на nginx в контейнере ```nginx-app1```

Devops Infra
============

Запуск приложения
------

- **Задеплойте сервисы приложения**

Деплой происходит при помощи Docker Compose.  
Образ приложения располагается в приватном Docker реестре, поэтому нужно сперва залогиниться в нем.  

```
cd docker_compose/
docker login registry.gitlab.com
docker-compose up
```  

Docker Compose поднимет три контейнера с бд, редисом и приложением в подсети `app_net`.  
Редис и бд будут складывать свои данные с вольюмы `redis-data` и `postgres-data` соответственно.  

Откройте приложение в браузере по адресу `127.0.0.1:8080`

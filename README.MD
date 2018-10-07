Devops Infra
============

Cборка
------
- **Установите go**  

Подойдет go 1.11, следуйте инструкциям https://golang.org/doc/install
- **Скачайте исходники приложения**  

Простой способ - установить переменную `GOPATH` на нужную директорию,  и скачать с помощью `go get`:  
 ```
 mkdir devops_infra
 export GOPATH=/path/to/devops_infra
 cd devops_infra
 go get gitlab.com/tfs18f-ekb-devops/public/application.git
 ```  
- **Соберите приложение**  

 Перейдите в проект и соберите его:
 ```
 cd src/gitlab.com/tfs18f-ekb-devops/public/application.git  
 go build
 ```
   
 При успешной компиляции в корне проекта появится файл `application.git`

Запуск
------
- **Поднимите Redis**

Если у вас еще не установлен Redis, следуйте инструкции https://redis.io/topics/quickstart

- **Поднимите и настройте Postgres**

Если у вас еще не установлен и не запущен Postgres, следуйте инструкции https://www.postgresql.org/download/  
Войдите в консоль под дефолтным пользователем, создайте роль *feed* и бд *feed*: 
```
psql postgres
postgres=# create role feed with login password 'feed';
postgres=# alter role feed createdb;
postgres=# create database feed;
```  

- **Запустите приложение**

Перейдите в папку с собранным приложением и запустите его:
```
./application.git --log-level info
```

Откройте приложение в браузере по адресу `0.0.0.0:8080` 
# Социальная сеть

В социальной сети есть пользователи, которые могут зарегистрироваться, создавать, обновлять и удалять посты, получать свою стену с постами, просматривать стены с постами других пользователей, 
ставить лайки и смотреть статистику по постам виде количества лайков и просмотров, а также оставлять комментарии к постам и просматривать их.

### Поэтапная реализация:

1) Написать c4 диаграммы контекста и контейнеров в коде с помощью plantuml:
   
    1.1 Главный сервис, который отвечает за клиентское API и за регистрацию и аутентификацию пользователей. Главный сервис ходит в два других по gRPC. Главный сервис предоставляет REST api для фронта.
    
    1.2 Сервис статистики для подсчета лайков и просмотров. События с просмотрами и лайками отправляются через брокер сообщений в сервис статистики (kafka).
    
    1.3 Сервис (постов/задач) и комментариев.   

Каждый сервис будет реализован на Python и завернут в docker образ. На диаграмме контейнеров должны быть отображены СУБД, у каждого сервиса должны быть своя БД, для сервиса статистики буду использовать clickhouse

2) Реализовать REST api для основного сервиса.
   
   Регистрация нового пользователя в системе через логин и пароль. Обновление своих данных. Аутентификация в системе по логину и паролю.
   
3) Написать yml файл с open api спецификацией, где описаны все три метода и добавить docker-compose файл, где описан запуск СУБД и запуск сервиса пользователей.
   
4) Разработка gRPC api сервиса с логикой:
   
    4.1 Реализация gRPC api сервиса работы с постами/задачами
   
    4.2 Dockerfile для создания образа нового сервиса
   
    4.3 Реализация 5 gRPC методов (Создание поста/задачи, Обновление поста/задачи, Удаление поста/задачи, Получение поста/задачи по ID, Получение списка постов/задач с пагинацией)
   
    4.4 В методах обновления, удаления, получения необходимо сделать проверку на права, только пользователь, который создавал задачу или пост может работать с данными
   
    4.5 У сервиса должна быть своя БД
   
    4.6 Добавить в главный сервис новые REST методы, которые должны под капотом вызывать соответсвующие методы gRPC
   
    4.7 Добавить в docker-compose.yml новый сервис, которые предоставляет gRPC api
   
    4.8 Добавить в docker-compose.yml БД для нового сервиса
   
   

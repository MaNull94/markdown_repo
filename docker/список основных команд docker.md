# список основных команд docker

## список основных команд docker--Ссылки
[[Docker]] [[video_ca8e490b-30d3-4982-a74e-9d11aa016569]]
[url](https://youtu.be/TJg7QpqCH70?t=1637)

создаем образ
`docker build -t %имя_образа%`

запускаем контейнер из образа
`docker run %имя_образа% --name %имя_контейнера%`
можно также добавить ключ `--rm` чтобы по выходу из контейнера он удалялся, что для тестов будет удобно
если ключ не указывать то удалять придется руками
`docker rm %имя_контейнера%`

для удаления образа
`docker rmi %имя_образа%`

`docker rm $(docker ps -aq)` - удалить контейнеры по ID
`docker rmi $(docker images -q)` - удалить все образы по ID

`docker rm -v $(docker ps -aq -f status=exited)` - удаляет все остановленные контейнеры

`docker exec -it %имя контейнера% %команда%` - отправка команды непосредственно в контейнер. ‼️ использовать для дебага или просмотра. не делать изменения в контейнере

`docker start|stop|restart %имя_контейнера%` - нет нужды писать run каждый раз. Для управления созданных контейнеров есть отдельная команда



Источник
[[Видео]]: 02. Что такое Docker? Вечерняя школа Слёрма по Kubernetes. [URL](https://www.youtube.com/watch?v=TJg7QpqCH70&t=86s&ab_channel=%D0%A1%D0%BB%D1%91%D1%80%D0%BC)

## Заметка

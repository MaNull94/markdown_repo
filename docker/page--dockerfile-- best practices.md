[[Dockerfile]] [[BestPractice]]

## Чем чаще изменяется слой, тем ниже его расположение, так можно сэкономить время сборки образа


## FROM
Указывать тег образа, а еще лучше указывать конкретный sha256 ключ образа
`FROM openjdk:11-jre-slim`

```Dockerfile
FROM openjdk:11.0.16-jdk-nanoserver@sha256:fa330da75ee3277dd0098a86878f77d46e25aae40dc730546faddb81a4e3a740
```

### multi-stage build
для экономии места и обеспечения безопасности стоит разделить билд проекта на несколько этапов: сборка и запуск
![[dockerfile--multistage build - java]]

## WORKDIR
Нет нужды писать RUN mkdir а после WORKDIR. Достаточно одной команды
`WORKDIR %dir_name%`

## RUN
каждая команда внутри dockerfile создает слой контейнера, поэтому для оптимизации стоит осуществлять установку различных пакетов и очистку временных данных за одну RUN-команду:
```Dockerfile
RUN apt-get update && apt-get install -y \
  bzr \
  cvs \
  git \
  mercurial \
  subversion \
  && rm -rf /var/lib/apt/lists/*
```
[[docker RUN в одну строку]]

## связка ENTRYPOINT и CMD
![[dockerfile--cmd перезапись аргументов в момент docker run]]

2
# Лабораторная работа 4.

Для решения понадобится установить Docker. Можно это делать как в виртуальной машине с установленным Linux, так и через WSL (главное на линукс подобной системе).
## Решение задания
Создаем файл `Dockerfile` с помощью команды `touch` или `nano`. Заходим в этот файл с помощью команды `gedit Dockerfile`.  
Внутри Dockerfile мы пишем  
```
FROM ubuntu:latest  
  
RUN apt-get update && apt-get install -y libaa-bin inetutils-ping && apt-get clean && rm -rf /var/lib/apt/lists/*  
  
CMD ["aafire"]  
```
Мы указали образ, на основе которого все будет работать. Далее указываем, что мы хотим запустить, а именно мы обновляем пакетный менеджер и устанавливаем ПО под названием libaa-bin.  
Dockerfile готов, сохраняем и запускаем команду сборки образа с тегом `my-aafire`.  

![Uploading изображение.png…]()

Далее создаем контейнеры  


Запустить в контейнере приложение “aafire”. Обратите внимание, что оно бесконечное и контейнер не будет автоматически отключаться.  
Приложить скриншот в процессе работы контейнера.  

Далее в рамках лабораторной работы необходимо самостоятельно настроить сеть между двумя контейнерами, также как в предыдущей работе вы настраивали связь между двумя виртуальными машинами.  

Для проверки сети между контейнерами вам потребуется утилита ping. Поскольку контейнеры очень маленькие и в них нет ничего лишнего (по сравнению с виртуальными машинами) - ping там не установлен. В вашем образе нужно будет установить пакет с этой утилитой, помимо aafire.  

Далее запустите два контейнера с aafire и оставьте их в работающем состоянии.  
Откройте ещё одно окно терминала и создайте сеть при помощи команды 
```
docker network create myNetwork
```
После этого нужно будет подключить контейнеры к вашей сети. Названия контейнеров можно увидеть при выводе списка действующих контейнеров у вас на машине.
```
docker network connect myNetwork mycontainer1
docker network connect myNetwork mycontainer2
```
Теперь при помощи следующей команды вы можете увидеть настройки созданной вами сети.
```
docker network inspect myNetwork
```
Далее вам нужно самостоятельно протестировать соединение между контейнерами утилитой ping и приложить скриншот.

### Как успешно сдать работу?

Создать свой репозиторий из шаблона этого. Как это делается - "Use this template" -> "Create a new repository" и сделайте его public. 

Находясь уже в своем репозитории - создайте новый файл формата .md и там оформляйте отчет. В отчете опишите все шаги которые вы делали, чтобы получить финальный результат работы.

Что вам нужно знать, чтобы успешно защитить работу:

Как создавать и управлять - докерфайлом (команды, оптимизация), образами (создание, запуск, принцип работы), контейнерами (запуск, отслеживание, объединение); виртуализация и контейнеризация. 

## Источники

[Источник где можно найти все](https://google.com)

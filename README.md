![изображение](https://github.com/user-attachments/assets/3135e4f8-7825-4064-9d99-1ecebe482720)2
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

![photo_2024-12-05_14-29-18](https://github.com/user-attachments/assets/aa588d0a-0834-4c1d-be2b-fae4e4b59205)

Далее создаем контейнеры  
```
sudo docker run -it --name my-aafire-1 my-aafire
sudo docker run -it --name my-aafire-2 my-aafire
```
![photo_2024-12-05_14-36-19](https://github.com/user-attachments/assets/c1004d81-6020-4a96-9b9e-2481560e727d)
Если мы хотим еще раз запустить эти контейнеры то пишем команду `sudo docker start my-aafire-1`, если же еще мы хотим увидеть повторно огонь, то прописываем еще `sudo docker exec -it my-aafire-1 aafire`.  

Чтобы создать сеть между контейнерами, нужно запустить оба контейнера с `aafire` и оставить их в рабочем состоянии. Далее создаем 3-е окно в терминале и создаем сеть с помощью команды  
```
docker network create myNetwork
```
После этого подключаем контейнеры к только что созданной сети `myNetwork`  
```
docker network connect myNetwork my-aafire-1
docker network connect myNetwork my-aafire-2
```
После этого нужно будет подключить контейнеры к вашей сети. Названия контейнеров можно увидеть при выводе списка действующих контейнеров у вас на машине.
```
docker network connect myNetwork mycontainer1
docker network connect myNetwork mycontainer2
```
При помощи команды `ping` мы проверяем подключение к сетям  
```
docker exec -it my-aafire-1 ping my-aafire-2
docker exec -it my-aafire-2 ping my-aafire-1
```
![photo_2024-12-05_18-13-03](https://github.com/user-attachments/assets/cfd1a1b5-5704-4dab-bc65-de92a6a2782b)

### Как успешно сдать работу?

Создать свой репозиторий из шаблона этого. Как это делается - "Use this template" -> "Create a new repository" и сделайте его public. 

Находясь уже в своем репозитории - создайте новый файл формата .md и там оформляйте отчет. В отчете опишите все шаги которые вы делали, чтобы получить финальный результат работы.

Что вам нужно знать, чтобы успешно защитить работу:

Как создавать и управлять - докерфайлом (команды, оптимизация), образами (создание, запуск, принцип работы), контейнерами (запуск, отслеживание, объединение); виртуализация и контейнеризация. 

## Источники

[Источник где можно найти все](https://google.com)

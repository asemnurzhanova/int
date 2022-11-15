# Задание 1
1. Написать Dockerfile
2. Собрать образ при помощи Dockerfile
```sh
docker build -t asemn00/golang_app_intern:latest /path/to/project
```
3. Создать и запустить контейнер из образа
```sh
docker run -d -p 3000:3000 asemn00/golang_app_intern:latest
```
4. Загрузить созданный образ в репозиторий
```sh
docker push asemn00/golang_app_intern:latest
```
# Задание 2
1. Написать файл Playbook
2. Перейти в каталог проекта
```sh
cd /path/to/project
```
3. Установить библиотеку виртуального окружения
```sh
python3 -m pip install virtualenv
```
4. Создать и активировать виртуальное окружение
```sh
python3 -m virtualenv ansible
source ansible/bin/activate
```
5. Установить библиотеки, необходимые для запуска Playbook
```sh
pip install -r requirements.txt
```
6. Запустить Playbook
```sh
ansible-playbook golang.yaml
```
# Задание 3
```sh
minikube start
helm create golang-app
cd golang-app
```
Отредактировать файл values.yaml
```sh
helm install --values values.yaml golang-app .
```
###### kubectl get pods (проверить запустился ли контейнер)

NAME                         | READY  | STATUS   | RESTARTS  | AGE 
---------------------------- | ------ | -------- | --------- |--- 
golang-app-77658fc567-jwkl9  | 1/1    | Running  | 0         | 97s

###### export NODE_PORT=$(kubectl get --namespace default -o jsonpath="{.spec.ports[0].nodePort}" services golang-app)
###### export NODE_IP=$(kubectl get nodes --namespace default -o jsonpath="{.items[0].status.addresses[0].address}")
###### curl http://$NODE_IP:$NODE_PORT
###### Получили Hello !

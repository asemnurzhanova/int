# Задание 1
1. Перейти в каталог проекта
```sh
cd /path/to/project
```
2. Отредактировать `Dockerfile`
3. Собрать образ при помощи Dockerfile
```sh
docker build -t asemn00/golang_app_intern:latest .
```
4. Создать и запустить контейнер из образа
```sh
docker run -d -p 3000:3000 asemn00/golang_app_intern:latest
```
5. Открыть ссылку <http://localhost:3000> в браузере для проверки приложения
# Загрузка образа в репозиторий
1. Войти в реестр Docker Hub
```sh
export DOCKER_REGISTRY=https://index.docker.io/v1/
export DOCKER_USER=asemn00 # пользователь registry
read -s DOCKER_PASSWORD # пароль от registry
echo $DOCKER_PASSWORD | docker login -u ${DOCKER_USER} --password-stdin ${DOCKER_REGISTRY}
```
2. Загрузить созданный образ в репозиторий
```sh
docker push asemn00/golang_app_intern:latest
```
3. Выйти из рееста
```sh
docker logout
```
Output:
```
Removing login credentials for https://index.docker.io/v1/
```
# Задание 2
1. Написать Playbook `golang.yaml`
2. Установить библиотеку виртуального окружения
```sh
python3 -m pip install virtualenv
```
3. Создать и активировать виртуальное окружение
```sh
python3 -m virtualenv ansible
source ansible/bin/activate
```
4. Записать в `requirements.txt` библиотеки, необходимые для запуска Playbook
5. Установить их
```sh
pip install -r requirements.txt
```
6. Запустить Playbook
```sh
ansible-playbook golang.yaml
```
# Задание 3
1. Установить [Инструмент командной строки Kubernetes](https://kubernetes.io/ru/docs/tasks/tools/install-kubectl/),  [Minikube](https://kubernetes.io/ru/docs/tasks/tools/install-minikube/), [Helm](https://helm.sh/ru/docs/intro/install/)
2. Запустить minikube
```sh
minikube start
```
3. Создать чарт в каталоге golang-app
```sh
helm create golang-app
```
4. Перейти в каталог чарта
```sh
cd golang-app
```
5. Отредактировать файл values.yaml
6. Развернуть чарт
```sh
helm install --values values.yaml golang-app .
```
7. Проверить запустился ли контейнер
```sh
kubectl get pods
```
Output:
```
NAME                          READY   STATUS    RESTARTS   AGE  
golang-app-77658fc567-jwkl9   1/1     Running   0          97s
```
8. Получить URL приложения
```sh
export NODE_PORT=$(kubectl get --namespace default -o jsonpath="{.spec.ports[0].nodePort}" services golang-app)
export NODE_IP=$(kubectl get nodes --namespace default -o jsonpath="{.items[0].status.addresses[0].address}")
echo https://$NODE_IP:$NODE_PORT
```
9. Проверить приложение
```sh
curl http://$NODE_IP:$NODE_PORT
```
Output:
```
Hello !
```

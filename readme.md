
# Написать докерфайл
###### docker build -t asemn00/golang_app_intern:latest /path/to/project
###### docker run -d -p 3000:3000 asemn00/golang_app_intern:latest
###### docker push asemn00/golang_app_intern:latest
# Написать файл yaml
###### cd /path/to/project
###### python3 -m pip install virtualenv
###### python3 -m virtualenv ansible
###### source ansible/bin/activate
###### pip install -r requirements.txt
###### ansible-playbook golang.yaml
###### minikube start
###### helm create golang-app
# Отредактировать файл values.yaml
###### cd golang-app
###### helm install --values values.yaml golang-app .
###### kubectl get pods (проверить запустился ли контейнер)
NAME                          READY   STATUS    RESTARTS   AGE
golang-app-77658fc567-jwkl9   1/1     Running   0          97s

###### export NODE_PORT=$(kubectl get --namespace default -o jsonpath="{.spec.ports[0].nodePort}" services golang-app)
###### export NODE_IP=$(kubectl get nodes --namespace default -o jsonpath="{.items[0].status.addresses[0].address}")
###### curl http://$NODE_IP:$NODE_PORT
###### Получили Hello !

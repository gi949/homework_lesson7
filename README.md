# homework_lesson7
Провести настройку аутентификации доступа к yandex cloud-id, введя в консоли:

export YC_TOKEN=$(yc iam create-token)

export YC_CLOUD_ID=$(yc config get cloud-id)

export YC_FOLDER_ID=$(yc config get folder-id)

Ввести в консоли команды:

Инициализация terraform

terraform init

Проверка сценария

terraform terraform plan

Создание и настройка кластера описана в

https://github.com/gi949/homework_lesson4

Настраивать кластер OpenSearch и Dashboards будем на ВМ нашего веб приложения.

Три ноды кластера OpenSearch на web1, web2, bs1, Dashboards на bs2.

В файле elk/inventories/opensearch/hosts настраиваем внешние и внутренние ip для нод кластера OpenSearch и Dashboards,
а также роли нод кластера OpenSearch.

Устанавливаем java на ноды кластера OpenSearch:

ansible-playbook jv_ins.yml

Устанавливаем и настраиваем кластер OpenSearch и Dashboards:

ansible-playbook elk/opensearch.yml -i elk/inventories/opensearch/hosts --extra-vars "admin_password=<пароль> kibanaserver_password=<пароль> logstash_password=<пароль> fluentbit_password=<пароль>" -b

Устанавливаем и настраиваем fluent-bit на ВМ нашего веб приложения:

ansible-playbook fluent.yml

Подключаемся к веб-интерфейсу Dashboards по <внешний ip:5601> под логином admin.

Проверяем, что логи от nginx, php-fpm и mysql поступают:


![index-all](https://github.com/gi949/homework_lesson7/assets/94520051/9b8b04ca-590c-40b6-8634-5c31151f8d7f)




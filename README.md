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

Создаем индекс для nginx

![index-nginx-1](https://github.com/gi949/homework_lesson7/assets/94520051/ce95a68c-2435-4a08-a2b1-cdae0a03125e)

![index-nginx-2](https://github.com/gi949/homework_lesson7/assets/94520051/6e504d73-89d8-4f51-8f3b-0be5fafd044b)

![index-nginx-3](https://github.com/gi949/homework_lesson7/assets/94520051/bb458582-6c62-4ac1-897a-256d8483a309)

В меню Discover смотрим логи nginx

![index-nginx-5](https://github.com/gi949/homework_lesson7/assets/94520051/60248636-28f1-4e22-ae5f-b6541075734d)

Аналогично создаем индексы для php-fpm и mysql, меню Discover смотрим логи php-fpm и mysql:

![index-mysql](https://github.com/gi949/homework_lesson7/assets/94520051/0f3f544a-ba43-43ff-8fa8-fe0acf9ea77b)

![index-php](https://github.com/gi949/homework_lesson7/assets/94520051/313b83fb-a491-4376-8f8d-8d233d555b97)


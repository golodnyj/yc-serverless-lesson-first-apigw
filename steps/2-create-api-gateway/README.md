# Yandex API Gateway
## Создание спецификации

Создадим спецификацию `hello-world.yaml` и используем ее для инициализации:

    yc serverless api-gateway create \
    --name hello-world \
    --spec=hello-world.yaml \
    --description "hello world"

В результате успешного создания API-шлюза получим `domain`:
    
    yc serverless api-gateway list
    yc serverless api-gateway get --name hello-world

Скопируем служебный домен, чтобы проверить работоспособность API-шлюза. Вставьте адрес в браузер и добавьте в конце допишите /hello. Должно получиться следующее:

    https://<ID API Gateway>.apigw.yandexcloud.net/hello

Теперь давайте протестируем запрос с параметрами. Добавьте к предыдущему запросу `?user=my_user`. Должно получиться следующее:

    https://<ID API Gateway>.apigw.yandexcloud.net/hello?user=my_user
    
В первом случае в окне браузера вы получите `Hello, world!` во втором `Hello, my_user!`.

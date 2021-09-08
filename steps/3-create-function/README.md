# Создание Функции

До этого момента мы использовали рантайм `python37`, однако с версии рантайма `python39` библиотеки необходиомо указывать явно. Для работы с `requirements.txt` есть удобная python библиотека `pipreqs`. Для генерации `requirements.txt` с помощью `pipreqs` достаточно указать рабочий каталог. В большинстве интерпритаторов linux для указания текущего каталога есть переменная `$PWD`. Если файл `requirements.txt` уже есть и его нужно актуализировать то используется флаг `--force`, например:  

    pip install pipreqs
    pipreqs $PWD --print
    pipreqs $PWD --force

Для того, чтобы создать функцию проверим, что нам доступны переменные для инициации подключения: `CONNECTION_ID`, `DB_USER`, `DB_HOST` мы их создавали в предыдущей работе с помощью следующих команд:

    echo "export CONNECTION_ID=<CONNECTION_ID>" >> ~/.bashrc && . ~/.bashrc
    echo "export DB_USER=<DB_USER>" >> ~/.bashrc && . ~/.bashrc
    echo "export DB_HOST=<DB_HOST>" >> ~/.bashrc && . ~/.bashrc

Создадим нашу функцию `function-for-user-requests.py`, при этом сразу зададим все необходимые переменные и сервисный аккаунт:

    yc serverless function create \
    --name  function-for-user-requests \
    --description "function for respons to user"

    yc serverless function version create \
    --function-name=function-for-user-requests \
    --memory=256m \
    --execution-timeout=5s \
    --runtime=python37 \
    --entrypoint=function-for-user-requests.handler \
    --service-account-id $SERVICE_ACCOUNT_ID \
    --environment VERBOSE_LOG=True \
    --environment CONNECTION_ID=$CONNECTION_ID \
    --environment DB_USER=$DB_USER \
    --environment DB_HOST=$DB_HOST \
    --source-path function-for-user-requests.py

Проверим работоспособность функции: 

    yc serverless function version list --function-name function-for-user-requests
    yc serverless function invoke --name function-for-user-requests

    yc serverless function delete --name function-for-user-requesrt
    yc serverless api-gateway delete --name hello-world

Успешное вызов функции приводит к измерению времени ответа сайта и формировании записи в базе данных.



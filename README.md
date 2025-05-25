# Njinx
1. openssl genrsa -out rootCA.key 2048

Сгенерировать RSA ключа (genrsa) в файл (-out rootCA.key) длиной 2048 бит

2. openssl req -x509 -new -nodes -key rootCA.key -sha256 -days 1024 -out rootCA.pem

Создание (req) самоподписанного корневого сертификата (-x509) 
нового (-new) без шифрования паролем (-nodes), 
указав ключ (-key rootCA.key), алгоритмом хэширования ( -sha256) 
на 1024 дней (-days 1024) в файл (-out rootCA.pem)


3. openssl req -new -nodes -keyout task-service.local.key -out task-service.local.csr -config task-service.local.conf

Создание (req) нового запроса на сертификат (-new) без шифрования паролем (-nodes),
сохранение приватного ключа в файл (-keyout task-service.local.key),
вывод запроса в файл (-out task-service.local.csr),
с использованием конфигурационного файла (-config task-service.local.conf)

4. openssl x509 -req -in task-service.local.csr -CA rootCA.pem -CAkey rootCA.key -CAcreateserial -out task-service.local.crt -days 365

Подписание сертификата (x509) на основе запроса (-req -in task-service.local.csr),
с указанием корневого сертификата (-CA rootCA.pem) и его ключа (-CAkey rootCA.key),
с автоматическим созданием серийного номера (-CAcreateserial),
сохранение подписанного сертификата в файл (-out task-service.local.crt)
с сроком действия 365 дней (-days 365)s 365

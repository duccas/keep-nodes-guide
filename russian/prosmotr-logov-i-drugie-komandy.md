# Просмотр логов и другие команды

### Просмотр логов

Существует несколько вариантов просмотра логов.

1. Посмотреть запущенные контейнеры

```text
docker ps -a
```

![](../.gitbook/assets/image%20%2818%29.png)

   2. Полные логи Beacon и ECDSA нод:

```text
sudo docker logs keep-client -f --since 1m
sudo docker logs keep-ecdsa -f --since 1m
```

   3. Вывод только подключенных пиров \(number of connected peers\):

{% code title="\#ДЛЯ BEACON НОДЫ" %}
```text
sudo docker logs -f keep-client --tail 1000 2>&1 | grep "number of connected peers:"
```
{% endcode %}

{% code title="\#ДЛЯ ECDSA НОДЫ" %}
```text
sudo docker logs -f keep-ecdsa --tail 1000 2>&1 | grep "number of connected peers:"
```
{% endcode %}

![](../.gitbook/assets/image%20%2821%29.png)

### Дополнительные команды

1. Остановка и удаление контейнера:

```text
sudo docker stop keep-client && sudo docker rm keep-client
sudo docker stop keep-ecdsa && sudo docker rm keep-ecdsa
```

   2. Очистка содержимого файла:

```text
echo -n > $HOME/keep-nodes/data/eth-address.txt
echo -n > $HOME/keep-nodes/data/keep_wallet.json
```

### Сохранить логи в файл

Сохранение логов контейнера в файл за последние 30 минут:

```text
sudo docker logs keep-ecdsa --since 30m >& ecdsa.log
```


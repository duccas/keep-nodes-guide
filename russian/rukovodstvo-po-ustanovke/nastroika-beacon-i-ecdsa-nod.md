---
description: Подробное описание установки двух нод (Beacon и ECDSA) на одном VPS сервере.
---

# Настройка и Запуск Beacon и ECDSA нод

### 1. Подготовка

Запускаем терминал нашего сервера на сайте, где создан сервер либо через специальные программы описанные в разделе:

{% page-ref page="../../getting-started/technical-requirements.md" %}

### 2. Настройка Ubuntu

Обновляем пакеты на сервере до новейших версий:

```text
sudo apt update
```

Устанавливаем пакет git, если он не установлен на сервере:

```text
sudo apt install git
```

Установим Докер:

```text
sudo apt install docker.io curl -y
```

Активируем Докер:

```text
sudo systemctl start docker
sudo systemctl enable docker
```

### 3. Настройка Фаервола

Открываем порты 22, 3919 и 3920 и активируем Firewall:

```text
sudo ufw allow 22 && sudo ufw allow 3919 && sudo ufw allow 3920 && yes | sudo ufw enable
```

Проверяем статус открытых портов командой:

```text
sudo ufw status
```

### 4. Настройка нод

Для начала скачаем на сервер github репозиторий со всеми папками и конфигами для запуска двух нод командой:

```text
git clone https://github.com/icohigh/keep-nodes.git
```

1. Заменяем в командах ниже "ВАШ ETH АДРЕС" на адрес вашего ETH кошелька.
2. "ВАШ ПАРОЛЬ" на пароль от ETH кошелька.
3. "СОДЕРЖИМОЕ ФАЙЛА UTC--2020-08-24T16-27-57" на содержимое файла, скачанного при создании ETH кошелька.
4. Вводим все эти команды.

```text
echo 'ВАШ ETH АДРЕС' >> $HOME/keep-nodes/data/eth-address.txt
echo 'ВАШ ПАРОЛЬ' >> $HOME/keep-nodes/data/eth-address-pass.txt
echo 'СОДЕРЖИМОЕ ФАЙЛА UTC--2020-08-24T16-27-57' >> $HOME/keep-nodes/data/keep_wallet.json
```

Выглядеть это должно вот так:

{% code title="\#ПРИМЕР" %}
```text
echo '0x208E233b930aacC7E17768F02106b6429B822133' >> $HOME/keep-nodes/data/eth-address.txt
echo 'qwerty123' >> $HOME/keep-nodes/data/eth-address-pass.txt
echo '{"version":3,"id":"d01c210a-1206-4754-9202-9f3g87472afe","address":"0x208E233b930aacC7E17768F02106b6429B822133","crypto":{"ciphertext":"85b53ab95e6fbea53f123123b5p234ujdce2122b08f6a73310f2d131e700","cipherparams":{"iv":"13d3efdead3523501ae8ede4328duwh4158"},"cipher":"aes-128-ctr","kdf":"scrypt","kdfparams":{"dklen":32,"salt":"ffad567d42eb5b3f1907e91023478fhs234r720234fs21a0a324cffc9e6c119137","n":131072,"r":8,"p":1},"mac":"c3b300aa4db1531add1c7c78d73d88f75a387485627g46539f1027999c66517"}}' >> $HOME/keep-nodes/data/keep_wallet.json
```
{% endcode %}

Записываем в файл .profile данные экспорта вашего Пароля и IP сервера путем ввода команд:

```text
echo 'export ETH_PASSWORD=$(cat $HOME/keep-nodes/data/eth-address-pass.txt)' >> $HOME/.profile
echo 'export SERVER_IP=$(curl ifconfig.co)' >> $HOME/.profile
```

Теперь нам нужно добавить в конфиг файл INFURA ID от вашего аккаунта [https://infura.io/](https://infura.io/) созданного ранее.   
Всмавляем вместо "ВАШ\_ИНФУРА\_ID\_БЕКОН\_НОДЫ" и "ВАШ\_ИНФУРА\_ID\_ECDSA\_НОДЫ" соответственно ID Beacon и ECDSA ноды.

```text
grep -rl INFURA_BEACON_ID $HOME/keep-nodes/beacon/config* | xargs perl -p -i -e 's/INFURA_BEACON_ID/ВАШ_ИНФУРА_ID_БЕКОН_НОДЫ/g'
```

```text
grep -rl INFURA_ECDSA_ID $HOME/keep-nodes/ecdsa/config* | xargs perl -p -i -e 's/INFURA_ECDSA_ID/ВАШ_ИНФУРА_ID_ECDSA_НОДЫ/g'
```

Выглядеть это должно вот так:

{% code title="\#ПРИМЕР" %}
```text
grep -rl INFURA_BEACON_ID $HOME/keep-nodes/beacon/config* | xargs perl -p -i -e 's/INFURA_BEACON_ID/6e6a4ed128a5f7s82bcc470710fb0/g'
grep -rl INFURA_ECDSA_ID $HOME/keep-nodes/ecdsa/config* | xargs perl -p -i -e 's/INFURA_ECDSA_ID/a888cf7gy6e888b0d21ee96b4201e0/g'
```
{% endcode %}

Теперь сделаем экспорт пароля командой:

```text
export ETH_PASSWORD=$(cat $HOME/keep-nodes/data/eth-address-pass.txt)
```

Все готово к запуску!

### 5. Запуск Beacon ноды

Запуск Бекон ноды будем производить командой ниже:

```text
sudo docker run -d \
--entrypoint keep-client \
--restart always \
--volume $HOME/keep-nodes/data:/mnt/data \
--volume $HOME/keep-nodes/beacon/config:/mnt/beacon/config \
--volume $HOME/keep-nodes/beacon/persistence:/mnt/beacon/persistence \
--env KEEP_ETHEREUM_PASSWORD=$ETH_PASSWORD \
--env LOG_LEVEL=debug \
--name keep-client \
-p 3919:3919 \
keepnetwork/keep-client:v1.3.0-rc.3 --config /mnt/beacon/config/config.toml start
```

### 6. Запуск ECDSA ноды

Запуск ECDSA ноды будем производить следующей командой:

```text
sudo docker run -d \
--entrypoint keep-ecdsa \
--restart always \
--volume $HOME/keep-nodes/data:/mnt/data \
--volume $HOME/keep-nodes/ecdsa/config:/mnt/ecdsa/config \
--volume $HOME/keep-nodes/ecdsa/persistence:/mnt/ecdsa/persistence \
--env KEEP_ETHEREUM_PASSWORD=$ETH_PASSWORD \
--env LOG_LEVEL=debug \
--name keep-ecdsa \
-p 3920:3919 \
keepnetwork/keep-ecdsa-client:v1.2.0-rc.4 --config /mnt/ecdsa/config/config.toml start
```

### 7. Остановка и удаление

1. Остановка и удаление контейнера производится следующими командами:

```text
sudo docker stop keep-client && sudo docker rm keep-client
sudo docker stop keep-ecdsa && sudo docker rm keep-ecdsa
```

### 8. ВАЖНО!

{% page-ref page="../obnovlenie-nody.md" %}


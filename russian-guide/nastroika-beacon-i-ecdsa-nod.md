---
description: Подробное описание установки двух нод (Beacon и ECDSA) на одном VPS сервере.
---

# Настройка Beacon и ECDSA нод

### Подготовка

Запускаем терминал нашего сервера на сайте, где создан сервер либо через специальные программы описанные в разделе:

{% page-ref page="../getting-srarted/technical-requirements.md" %}

### Настройка Ubuntu

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

### Настройка Фаервола

Открываем порты 22, 3919 и 3920 и активируем Firewall:

```text
sudo ufw allow 22 && sudo ufw allow 3919 && sudo ufw allow 3920 && sudo ufw enable
```

После ввода команды нажимаем английскую "y" и Enter для подтверждения активирования фаервола.

Проверяем статус открытых портов командой:

```text
sudo ufw status
```

### Настройка нод

Для начала скачаем на сервер github репозиторий со всеми настройками для запуска двух нод командой:

```text
git clone https://github.com/icohigh/keep-nodes.git
```




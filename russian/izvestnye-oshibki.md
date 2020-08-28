# Известные ошибки

### Ошибка 1

Если у вас возникает ошибка, как на скриншоте ниже, то первым делом нужно проверить авторизованы ли контракты в дашборде KEEP - [https://dashboard.test.keep.network/applications/random-beacon](https://dashboard.test.keep.network/applications/random-beacon).   
Если все авторизовано, то проблема скорее всего в Infura аккаунте. 

![](../.gitbook/assets/image%20%2824%29.png)

1. Нужно войти в ваш Infura аккаунт
2. Выбрать проект BEACON NODE \(у вас он может быть назван как угодно\)

![](../.gitbook/assets/image%20%2820%29.png)

   3. Зайти в настройки проекта

![](../.gitbook/assets/image%20%2823%29.png)

   4. И в поле ALLOWLIST CONTRACT ADDRESSES вставить свой ETH адрес и нажать ADD

![](../.gitbook/assets/image%20%2819%29.png)

   5. Тоже самое проделать и для проекта ECDSA ноды.  
   6. Готово.

### Ошибка 2

Если после запуска мы видим подобный текст в логах, значит у нас проблема с паролем. 

> FATAL keep-main error reading config file: password is required; set in the config file, set environment variable KEEP\_ETHEREUM\_PASSWORD to the password, or set the same environment variable to 'prompt' to be prompted for the password at startup

![](../.gitbook/assets/image%20%2826%29.png)

1.  Повторно сделаем экспорт пароля командой:

```text
export ETH_PASSWORD=$(cat $HOME/keep-nodes/data/eth-address-pass.txt)
```

   2. Если же это не помогает, то нужно непосредственно в команду запуска прописать ваш пароль как на скриншоте ниже вместо $ETH\_PASSWORD:

![&#x417;&#x430;&#x43C;&#x435;&#x43D;&#x438;&#x442;&#x435; $ETH\_PASSWORD &#x43D;&#x430; &#x432;&#x430;&#x448; &#x43F;&#x430;&#x440;&#x43E;&#x43B;&#x44C; &#x43E;&#x442; &#x43A;&#x43E;&#x448;&#x435;&#x43B;&#x44C;&#x43A;&#x430;](../.gitbook/assets/image%20%2825%29.png)

   3. Можно запускать.


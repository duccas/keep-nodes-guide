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


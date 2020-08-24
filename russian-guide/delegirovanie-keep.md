# Делегирование KEEP

Для того чтобы делегировать токены KEEP нужно перейти на сайт Keep Token Dashboard - [https://dashboard.test.keep.network/tokens/delegate](https://dashboard.test.keep.network/tokens/delegate)

Жмем подключиться через Metamask и мы попадаем на вкладку Delegate Tokens.

Видим, что у нас есть грант с номером 409 и 300к KEEP на счету.

### Делегируем токены для стейкинга

1. В поле "Token amount" вводим 300,000
2. В полях Authorizer Address/Operator Address/Beneficiary Address вводим свой эфирный адрес
3. Жмем "DELEGATE STAKE"

![](../.gitbook/assets/image%20%288%29.png)

   4. Во всплывшем окне в поле для ввода пишем DELEGATE и жмем кнопку DELEGATE

![](../.gitbook/assets/image%20%286%29.png)

   5. Подтверждаем транзакцию в Metamask

   6. Ждем пока транзакция подтвердится. Если все прошло хорошо, получаем сообщение SUCCESS.

### Авторизация контрактов

Теперь нужно авторизовать контракты в дашборде. 

1. Переходим по меню в  Applications -&gt; Random Beacon \([https://dashboard.test.keep.network/applications/random-beacon](https://dashboard.test.keep.network/applications/random-beacon)\) и авторизуем контракт Keep Random Beacon Operator Contract нажатием на кнопку AUTHORIZE и подтверждаем транзакцию в Metamask. 

![](../.gitbook/assets/image%20%2812%29.png)

   2. Далее переходим по меню в  Applications -&gt; tBTC \([https://dashboard.test.keep.network/applications/tbtc](https://dashboard.test.keep.network/applications/tbtc)\) и авторизуем контракты BondedECDSAKeepFactory и TBTCSystem.

![](../.gitbook/assets/image%20%2811%29.png)

   3. Теперь нам нужно добавить тестовый эфир полученный ранее с помощью крана ETH. Жмем ниже кнопку "ADD ETH".

![](../.gitbook/assets/image%20%2814%29.png)

   4. В поле ввода пишем сколько эфира нужно добавить. Минимум 0.5 ETH и жмем кнопку "ADD ETH". Далее подтверждаем транзакцию.

![](../.gitbook/assets/image%20%289%29.png)

   5. Готово.


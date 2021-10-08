# php-deployer-bitrix24
PHP рецепт для деплоера (https://github.com/deployphp/deployer), который отправляет сообщения о деплоях в Битрикс24.

# Пример работы

// Настройки для уведомлений в битрикс

set('bitrix_webhook', 'https://mybitrix.bitrix24.ru/rest/111/5w9s2qatn1xqtkve/imbot.message.add.json');

set('bitrix_bot_id', 1111);

set('bitrix_client_id', 'q94zphhebaob8h1yymwzs3xun69gpkf6');

set('bitrix_chat_id', 'chat11111');


// Сообщения в битрикс

set('bitrix_text', 'Запустили деплой на сервер.');

set('bitrix_success_text', 'Деплой на сервер успешно завершён.');

set('bitrix_failure_text', 'Деплой на сервер не удался.');


// Bitrix24

before('deploy:prepare', 'bitrix:notify');

after('success', 'bitrix:notify:success');

after('deploy:failed', 'bitrix:notify:failure');

# Настройки
### Настройка вебхука битрикса
set('bitrix_webhook', 'https://mybitrix.bitrix24.ru/rest/111/5w9s2qatn1xqtkve/imbot.message.add.json');

После ссылки на вебхук, необходимо указать метод битрикса, принимающих сообщения.

В данном случае: `https://mybitrix.bitrix24.ru/rest/111/5w9s2qatn1xqtkve/` - ссылка, `imbot.message.add.json` - метод.

### Настройка ID бота
set('bitrix_bot_id', 1111);

Здесь указывается ID бота, который будет отправлять сообщения в чат битрикса. Сам бот создается внутри битрикса.

### Настройка ID чата
set('bitrix_chat_id', 'chat11111');

Здесь указывается ID чата, в котором будут отображатся сообщения о деплоях.

Внутри битрикса ID чата можно узнать, зайдя в нужный чат и ввести команду `/getDialogId`

### Настройка ID клиента
set('bitrix_client_id', 'q7lzphdnugrb8h1ymamhs8xun34gkvf6');

Здесь указывается ID клиента, который появляется после создания бота в битриксе

# Виды сообщений
`bitrix_text` - Текст для обычного сообщения, например для сообщения о начале деплоя

`bitrix_success_text` - Текст сообщения об успешном завершении деплоя

`bitrix_failure_text` - Текст сообщения о неудачном завершении деплоя

# Методы для отправки сообщений
`bitrix:notify` - Метод для отправки сообщений, например перед началом деплоя

`bitrix:notify:success` - Метод отправки сообщения об успешно завершенном деплое

`bitrix:notify:failure` - Метод отправки сообщения о неудобном завершении деплоя

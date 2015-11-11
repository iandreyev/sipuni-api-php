# Примеры использования Sipuni API на PHP

### Перед запуском

В личном кабинете Sipuni в разделе Интеграция скопируйте ключ.

В файле config/config.php впишите ваш ключ.

Теперь можно запускать примеры из папки examples.

```
$php allocate_static
```

### Работа с классом-оберткой для Sipuni API

Для работы, помимо файла SipuniApi.class.php необходимо подключить архив httpful.phar.
Это библиотека для работы с REST API. Ее можно подключать также при помощи composer.
Подробнее читайте на сайте библиотеки [phphttpclient.com](http://phphttpclient.com).

 ```
 require_once ('../lib/httpful.phar');
 require_once ('../lib/SipuniApi.class.php');
 use sipuni\SipuniApi;
 ```

 В конструктор класса подайте API ключ, как его получить читайте в разделе Перед запуском.
 ```
 $api = new SipuniApi($key);
 ```

 Найдите нужный объект range. Например, чтобы найти диапазон для номеров 499
 ```
 $range = $api->findRange('499');
 ```
 Результат:
 ```
 stdClass Object
 (
    [id] => 1
    [title] => Москва 499
 )
 ```

 Теперь можно выделить статический номер и сделать переадресацию на номер 74997778899.
 ```
 $number = $api->allocateStatic($range->id, '74997778899', 'For newspapers');
 ```
 Результат, выделен номер:
 ```
 '74995550000'
 ```

 Когда номер больше не нушен, его нужно освободить.
 ```
 $success = $api->releaseStatic('74995550000');
 ```
 Результат:
  ```
  true
  ```

 Все методы создают исключение \\Exception, в случае ошибок.



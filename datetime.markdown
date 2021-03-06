# Работа с датой и временем

<!-- http://www.webmasters.by/articles/web-programming/1487-working-with-dates-and-times-php-mysql.html -->

Работать с датами и временем в коде на PHP приходится регулярно. Редкое приложение обходится без того, чтобы каким-либо образом сохранять, преобразовывать или вычислять эти данные в рамках своей бизнес-логики. Помимо этого даты и время — постоянный гость любых сопутствующих данных приложений: логи, профайлинг, запуск по расписанию.

Рассмотрим основные инструменты, которые предоставляет PHP в этой области.

http://php.net/manual/ru/ref.datetime.php

## time()

http://php.net/manual/ru/function.time.php

Эта функция возвращает так называемое текущее абсолютное время. Это число равно количеству секунд, которое прошло с полуночи 1 января 1970 года (с начала эпохи UNIX). Значение не зависит от часового пояса (UTC). Значение, возвращаемое функцией `time` часто называют `timestamp` (таймстэмп).

На практике использовать время в секундах от определенного момента в прошлом оказывается действительно удобно. Посмотрим несколько примеров использования.

    <?php

    // посчитаем значение timestamp будет ровно через сутки
    $tomorrow = time() + (24 * 60 * 60);
    echo 'Завтра: '. date('Y-m-d', $tomorrow);

    // узнаем абсолютное время через 7 дней, 24 часа, 60 минут, 60 секунд
    $nextWeek = time() + (7 * 24 * 60 * 60);
    echo 'Сейчас:           '. date('Y-m-d') ."\n";
    echo 'Следующая неделя: '. date('Y-m-d', $nextWeek) ."\n";

## date()

http://php.net/manual/ru/function.date.php

`date` точно может претендовать на лидера в рейтинге функций для работы с датой и временем. Ее задача — форматирование, т.е. вывод в нужном формате, переданного значения времени.

Формат задается отдельным параметром в виде строки-шаблона. Внутри шаблона можно достаточно гибко указать все виды вывода лет, месяцев, дней, часов, минут и дат целиком. Полный список символов, доступных в шаблоне есть в документации.

Выше мы уже применяли функцию `date`, чтобы отформатировать значения, полученные с помощью `time`, в понятный человеку вид. Если `date` не передать параметр времени в секундах, она будет использовать текущее время.

    <?php
    // Monday
    echo date("l");

    // Monday 8th of August 2005 03:12:46 PM
    echo date('l jS \of F Y h:i:s A');

    // July 1, 2000 is on a Saturday
    echo "July 1, 2000 is on a " . date("l", mktime(0, 0, 0, 7, 1, 2000));

В строке формата желательно избегать ставить не связанные с шаблоном слова и символы, так как без правильной обработки вывод может быть неожиданным — символы превратятся в кусочки даты.

    <?php
    // Wednesday the 15th
    echo date('l \t\h\e jS');

    // лучше заменить на
    echo date('l') . ' the ' . date('jS');

Имейте в виду, что вывод `date` зависит от текущей таймзоны, указанной в настройках.

## mktime()

Еще одна функция для получения заветного timestamp.

    <?php
    // функция поймет, что 32 декабря — это 1 января следующего года
    echo date("M-d-Y", mktime(0, 0, 0, 12, 32, 1997));
    // и 13-ый месяц ее не испугает
    echo date("M-d-Y", mktime(0, 0, 0, 13, 1, 1997));
    echo date("M-d-Y", mktime(0, 0, 0, 1, 1, 1998));
    echo date("M-d-Y", mktime(0, 0, 0, 1, 1, 98));

Из-за своих особенностей `mktime` часто удобно использовать для вычислений со временем.

## strtotime()

Эта функция конвертирует английское строковое представление времени в timestamp. Отличается умом и сообразительностью. Часто выручает, когда дату мы получаем из внешнего источника, и до сохранения в базу ее надо преобразовать.

    <?php
    echo strtotime("now"). "<br />;
    echo strtotime("10 September 2000"). "<br />;
    echo strtotime("+1 day"). "<br />;
    echo strtotime("+1 week"). "<br />;
    echo strtotime("+1 week 2 days 4 hours 2 seconds"). "<br />;
    echo strtotime("next Thursday"). "<br />;
    echo strtotime("last Monday"). "<br />;


## Часовые пояса

Попробуйте, что выведет вам код из примера ниже.

    <?php
    echo date('H:i:s');

    date_default_timezone_set('America/New_York');
    echo date('H:i:s');

PHP достаточно умен и сообразителен, чтобы понимать, что в разных часовых поясах время разное. Поэтому целый ряд функций полагается на настройку текущей таймзоны. В настройках самого PHP в файл `php.ini` для этого есть настройка `date.timezone`. Если вам проще управлять часовым поясом из кода, то поможет функция `date_default_timezone_set`.

## DateTime
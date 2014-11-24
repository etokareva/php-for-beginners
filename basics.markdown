# Базовый синтаксис

## Введение

Изучение любого языка программирования начинается с классической и самой простой программы “Hello, world”:


    <?php
    echo "Hello, world!";

Любой PHP-скрипт начинается с открывающего тэга `<?php`. Не надо писать другой код на одной строке с открывающим тэгом (из этого правила есть исключения, но о них позже). С помощью конструкции `echo` происходит отображение информации. 

Попробуем немного расширить первый пример:

    <?php
    $myName = 'Jack';
    echo 'Hello, world! My name is ' . $myName . ' I am the new superstar!';

`$myName` – это переменная. Их используют для осуществления доступа к данным. В ходе выполнения программы значение переменных можно изменять. Попробуйте, например, изменить значение в кавычка на свое имя.

Обратите внимание на текст после оператора `echo` в данном примере. `.` — это знак конкатенации, он отвечает за соединение нескольких строк в одну. Заодно с его помощью можно объединять со строкой и переменные.

PHP можно использовать не только для написания отдельных скриптов. Он спроектирован таким образом, что код можно вставлять прямо в html-код.

    <!DOCTYPE html>
    <html>
        <head>
            <meta charset="utf-8">
            <title>PHP Test</title>
        </head>
        <body>
            <?php echo '<p>Hello World</p>'; ?> 
        </body>
    </html>

Использование html-тэга `<meta charset="utf-8">` обеспечит корректное отображение русского текста в браузере. При этом важно проследить, чтобы ваш текстовый редактор сохранял файлы в кодировке utf-8.

В этом примере мы как раз видим исключения из правила «не писать другой код на одной строке с открывающим php тэгом». Если все, что мы хотим сделать, это вывести какую-то строку через PHP внутри html, то написание на одной строке — оптимальный вариант.

## Тэги

Как уже было показано выше, код на PHP окружается в специальные тэги. Рекомендуется использовать стандартные тэги:


    <?php 
    echo "code goes here";
    ?>

Стандартные тэги нельзя отключить в конфигурации, поэтому они гарантировано будут работать всегда.

Важно заметить, что закрывающий тэг необязательно и нежелательно ставить, если в файле содержится только PHP код.

В отличии от стандартных тэгов, короткие можно отключить в конфиге PHP (с помощью директивы `short_open_tag`). Поэтому их использования лучше избегать.


    <?
    ... code
    ?>


У коротких тэгов есть еще одна вариация, которая является сокращением для `echo`, совмещенного с тэгами PHP:


    <?=$variable ?>
    <?php echo $variable; ?>

Эти конструкции идентичны с точки зрения PHP.

## Переменные

Выше уже упоминалсь про переменные и для чего они нужны. Вот несколько правил, которым должны подчиняться переменные в PHP:

* переменные обозначаются значком `$`
* имя переменной содержит только латинские буквы, символ _ и цифры
* имя переменной НЕ может начинаться с цифры

Переменные очень желательно называть осмысленно, т.е. так, чтобы их название тем или иным образом отражало, что именно содержится в самой переменной.

Посмотрим несколько примеров задания переменных и их названия:


    <?php
    $typical_variable_name = 'Типичное название переменной с разделением через подчеркивание.';
    $camelCaseStyleVariableName = 'Немного другой стиль именования.';
    $_anotherOne = 42;
    $_anotherOne2Or3 = true;

В PHP переменная может быть одного из 8 типов:

* Скалярные (простые): `boolean`, `string`, `integer`, `float`.
* Составные: `array`, `object`.
* Специальные: `resource`, `null`.

Интерпретатор языка сам определяет, какой тип у переменной, специально задавать это не нужно. Более того, он будет сам переводить переменные из одного типа в другой в зависимости от данных или производимых операций, но об этом еще будет позже. Пока посмотрим, как задаются переменные скалярных типов:


    <?php
    // boolean отвечает за хранение true или false
    $booleanVariable = true;

    // в integer само собой хранятся целые числа
    $integerVariable = 42;

    // float позволяет хранить дробные значения
    $floatOne = 1.05;

    // string говорит сам за себя
    $stringOfCourse = 'текст сообщения';

    // сразу глянем и на array, позволяющий работать с наборами данных
    // тут приведен синтаксим массивов для PHP, начиная с версии 5.4
    $arrayOfValues = [
        'name' => 'Neo',
        'fullName' => 'Mr. Anderson',
        'friends' => [
            'Trinity',
            'Morpheus',
        ],
    ];

    // специальный тип null означает пустоту, т.е. незаданное значение
    // часто используется для того, чтобы подготовить переменную для будущего использования
    $forFutureUse = null;

Про resource и object мы еще поговорим отдельно.

## Комметарии к коду

В примере кода задания переменных комментарии уже присутствовали. Там был пример однострочных комментариев, т.е. действующих только на ту строку, в которой они присутствует. Ниже будут другие примеры того, как можно оформлять и использовать комментарии к коду:


    <?php
    // Комментарий в одну строчку

    /* Многострочные комментарии 
    оформляются
    таким образом */

    /**
    * API Documentation Example – так оформляются описания к методам и функциям
    *
    * @param string $bar
    */
    function foo($bar) { }

    $comments = true;  /* Чем больше комментариев, тем проще разобраться потом. 
    Но код надо стараться писать так, чтобы он был понятен и без комментариев. */

    /* В этом случае сначала следует комментарий, на следующей строчке действие */
    $action_first = 0;

    $action_first = 1;  // на одной строке действие идет первым

А вот пример распространненных ошибок при работе с комментариями:


    <?php
    /* this is 
    commented */ but this is not */


    // This is also a single line comment 
    // New line comment ?> Here new line comment dont work, and this will be printed


## Операторы

Операторами в PHP, как и многих других языках программирования, называются по сути элементарные действия, которые могут принимать одно или несколько значений или выражений и преобразовывать их к новому результату. Звучит сложнее, чем есть на самом деле. Операторами, например, называются сложение, умножение и другие подобные действия.

Операторы делят на следующие:

* унарные, т.е. принимающие только одно значение, например, `!` – логический оператор «не»
* бинарные соответственно принимающие два параметра, таких большинство: `+`, `*` и многие другие
* тернарный оператор только один и он является сокращением условного оператора: `? :`

### Арифметические операторы

Работают так же, как и в привычных математических выражениях.


    <?php
    echo 2 + 2; // 4
    echo 3 - 2; // 1
    echo 1 * 2; // 2
    echo 4 / 2; // 2
    echo -2; // -2
    echo 3 % 2; // 1 (Остаток от деления)

Стоит отметить, что оператор `/` будет возвращать значение типа `float`. Исключением будет ситуация, когда оба операнда (делимое и делитель) будут типа `integer`, при этом результат деления будет целым числом без дробной части, тогда тип результата будет `integer`.

При попытке деления на ноль будет выводиться ошибка: `PHP Warning: Division by zero`.

Операнды остатка от деления `%` конвертируются в `integer` за счет отбрасывания дробной части до выполнения операции. А результат деления по модулю будет того же знака, что и делимое, т.е. результат `$a % $b` будет того же знака, что и `$a`.

### Присвоение

Оператор присвоения обозначается `=`, примеры работы с ним уже были выше. Используют его для задания значений переменным. Т.е. операнду слева от оператора присваивается значение выражения справа.

Присвоение может комбинироваться с арифмитическими операторами или конкатенацией строк. Например:


    <?php
    $a = 3;
    $a += 5; // 8

    $a *= 7; // 56

Отдельно стоит рассмотреть присваивание по ссылке. В отличии от предыдущих примеров в этом случае в новой переменной будет содержаться не копия предыдущего значения, а именно ссылка на него. Это проще понять на примере:


    <?php
    $a = 3;
    $b = &$a; // $b — ссылка на $a

    print "$a\n"; // 3
    print "$b\n"; // 3

    $a = 4; // изменим $a

    print "$a\n"; // 4
    print "$b\n"; // 4 , так как $b — это ссылка на $a


### Операторы сравнения

Как понятно из названия следующий набор операторов позволяет сравнивать значения. Результатом работы оператора всегда будет значение типа `boolean`, т.е. либо `true`, либо `false`.


    <?php
    $a == $b; // равенство — TRUE если $a равно $b после приведения типов.
    $a === $b; // идентичность — TRUE если $a равно $b, и они обе одного типа.
    $a != $b; // не равны — TRUE если $a не равно $b после приведения типов
    $a !== $b; // не идентичны — TRUE если $a не равно $b, или они оба разных типов
    $a < $b;
    $a > $b;
    $a <= $b;
    $a >= $b;

При сравнение есть несколько нюансов, про которые полезно знать:

* при сравнении числа и строки (или, если сравнение содержит строку, содержимое которой представляет собой число), оба операнда будут приводиться к числу
* при сравнении с помощью `===` и `!==` приведение типов, конечно, происходить не будет

При сравнении переменных (или просто данных) разных типов будут работать следующие правила приведения типов:

* `null` и `string` — `null` будет конвертироваться в пустую строку `''`
* `bool` или `null` со всем остальным — будет конвертацию в `boolean`

Небольшое предупреждение. Из-за того, как работают переменные типа `float` изнутри, не следует сравнивать две числа с плавающей точкой на равенство, так как результат может быть неправильным.


### Оператор управления ошибками

PHP supports one error control operator: the at sign @. When prepended to an expression in PHP, any error messages that might be generated by that expression will be ignored.

If you have set a custom error handler function with set_error_handler() then it will still get called, but this custom error handler can (and should) call error_reporting() which will return 0 when the call that triggered the error was preceded by an @.

If the track_errors feature is enabled, any error message generated by the expression will be saved in the variable $php_errormsg. This variable will be overwritten on each error.

Note: The @ works only on expressions. A simple rule of thumb is: if you can take the value of something, you can prepend the @ operator to it. For instance, you can prepend it to variables, function and include calls, constants, and so forth. You cannot prepend it to function or class definitions, or conditional structures such as if and foreach, and so forth.

Warning: Currently the @ error-control operator prefix will even disable error reporting for critical errors that will terminate script execution. Among other things, this means that if you use @ to suppress errors from a certain function and either it isn’t available or has been mistyped, the script will die right there with no indication as to why.

### Операторы инкремента/декремента

PHP унаследовал от языка программирования `C` многое, в том числе и операторы инкремента и декремента.

* `++$a` (преинкремент) — сначала увеличивает значение `$a` на единицу, затем возвращает значение `$a`
`$a++` (постинкремент) — сначала возвращает значение `$a`, затем увеличивает его на единицу
`--$a` (pre-decrement) — same as pre-increment, but decrement
`$a--` (post-decrement) — same as post-increment, but decrement
PHP follows Perl’s convention when dealing with arithmetic operations on character variables. For example, in PHP and Perl $a = ‘Z’; $a++; turns $a into ‘AA’. Note that character variables can be incremented but not decremented and even so only plain ASCII characters (a-z and A-Z) are supported. Incrementing/decrementing other character variables has no effect, the original string is unchanged.

Note: The increment/decrement operators do not affect boolean values. Decrementing NULL values has no effect too, but incrementing them results in 1.

### Логические операторы

$a and $b (And) — TRUE if both $a and $b are TRUE.
$a or $b (Or) — TRUE if either $a or $b is TRUE.
$a xor $b (Xor) — TRUE if either $a or $b is TRUE, but not both.
! $a (Not) — TRUE if $a is not TRUE.
$a && $b (And) — TRUE if both $a and $b are TRUE.
$a || $b (Or) — TRUE if either $a or $b is TRUE.
The reason for the two different variations of and and or operators is that they operate at different precedences, && and || operators have more precedence level then and and or.

### Строковые операторы

Для работы со строками существует всего два просты оператора. Первый из них — оператор конкатенации `.`, который мы уже видели выше в усложненном примере "Hello, world". Он возвращает объединение аргументов слева и справа от него.

Второй строковый оператор комбинированный: конкатенация с присвоением `.=`. С его помощью можно присоединить значение переменной справа к переменной слева.

    <?php
    $text = "What a strange word concatenation.";
    $text .= " But who the hell cares.";


### Приоритет операторов

Еще один важный момент — это приоритет выполнения операторов. Например, в выражении `1 + 5 * 3` ответ будет `16`, а не `18`, потому что приоритет у умножения выше, чем у сложения. Управлять приоритетом можно с помощью скобок. Тогда выражение `(1 + 5) * 3` равно 18.

Подробнее о приоритетах операторов можно посмотреть в [официальном мануале](http://ru.php.net/manual/ru/language.operators.precedence.php).


## If

Конструкция `if` — одна из наиболее часто используемых и важных практически в любом языке программирования. С помощью нее можно в зависимости от значения выражения в условии выполнять тот или иной фрагмент кода.




### Тернарный оператор

Another conditional operator is the ?: (or ternary) operator. The expression (expr1) ? (expr2) : (expr3) evaluates to expr2 if expr1 evaluates to TRUE, and expr3 if expr1 evaluates to FALSE. Since PHP 5.3, it is possible to leave out the middle part of the ternary operator. Expression expr1 ?: expr3 returns expr1 if expr1 evaluates to TRUE, and expr3 otherwise.

Please note that the ternary operator is a statement, and that it doesn’t evaluate to a variable, but to the result of a statement. This is important to know if you want to return a variable by reference. The statement return $var == 42 ? $a : $b; in a return-by-reference function will therefore not work and a warning is issued in later PHP versions.

It is recommended that you avoid “stacking” ternary expressions. PHP’s behaviour when using more than one ternary operator within a single statement is non-obvious.

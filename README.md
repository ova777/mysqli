# mysqli
MYSQLi extension library

### 1. Подключение к БД
```php
$db = new \ova777\MYSQLi\Connection('localhost', 'user', 'password', 'database');
```

### 2. Запросы на получение данных
```php
$rows = $db->command('SELECT * FROM table')->queryAll();
$row = $db->command('SELECT * FROM table')->queryRow();
$column = $db->command('SELECT * FROM table')->queryColumn();
$value = $db->command('SELECT * FROM table')->queryScalar();
```

### 3. Привязка значений к запросу
```php
//Один параметр
$rows = $db->command('SELECT * FROM table WHERE id=?')
    ->bind('i', 1)
    ->queryAll();
    
//Несколько параметров
$rows = $db->command('SELECT * FROM table WHERE id=? AND foo=?')
    ->bind('is', array(1, 'bar'))
    ->queryAll();
```

### 4. INSERT, UPDATE, DELETE запросы
```php
$db->command('INSERT INTO table SET int_col=?, str_col=?')
    ->bind('is', array(1, 'foo'))
    ->execute();
```

### 5. Повторное использование подготовленных запросов
```php
$cmd = $db->command('INSERT INTO table SET a=?,b=?');
$cmd->bind('is', array(1, 'foo'))->execute();
$cmd->bind('is', array(2, 'bar'))->execute();
//При повторном вызове bind можно не передавать типы значений
$cmd->bind(array(3, 'xyz'))->execute();
...
$cmd->close();
```
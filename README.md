# Шпаргалка по созданию CRUD-операций с использованием PHP и PDO (PHP Data Objects):
1. Подключение к базе данных:
```injectablephp
<?php
$servername = "localhost";
$username = "ваше_имя_пользователя";
$password = "ваш_пароль";
$dbname = "ваша_база_данных";

try {
    $conn = new PDO("mysql:host=$servername;dbname=$dbname", $username, $password);
    $conn->setAttribute(PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION);
    echo "Подключение к базе данных успешно";
} catch (PDOException $e) {
    echo "Ошибка подключения: " . $e->getMessage();
}
?>
```
2. Создание записи (Create):
```injectablephp
<?php
// Пример для таблицы "users"

$name = "Имя пользователя";
$email = "user@example.com";

try {
    $sql = "INSERT INTO users (name, email) VALUES (:name, :email)";
    $stmt = $conn->prepare($sql);

    $stmt->execute([
        'name' => $name,
        'email' => $email
    ]);
    
    echo "Запись успешно добавлена";
} catch (PDOException $e) {
    echo "Ошибка: " . $e->getMessage();
}
?>
```
3. Чтение записи (Read):
```injectablephp
<?php
// Пример для таблицы "users"

try {
    $sql = "SELECT id, name, email FROM users";
    $stmt = $conn->prepare($sql);
    $stmt->execute();

    // Получение результата в виде ассоциативного массива
    $result = $stmt->fetchAll(PDO::FETCH_ASSOC);

    // Вывод результатов
    foreach ($result as $row) {
        echo "ID: " . $row['id'] . ", Имя: " . $row['name'] . ", Email: " . $row['email'] . "<br>";
    }
} catch (PDOException $e) {
    echo "Ошибка: " . $e->getMessage();
}
?>
```
4. Обновление записи (Update):
```injectablephp
<?php
// Пример для таблицы "users"

$id = 1;
$newName = "Новое имя";

try {
    $sql = "UPDATE users SET name = :name WHERE id = :id";
    $stmt = $conn->prepare($sql);

    $stmt->execute([
        'name' => $name,
        'id' => $id
    ]);

    echo "Запись успешно обновлена";
} catch (PDOException $e) {
    echo "Ошибка: " . $e->getMessage();
}
?>

```
5. Удаление записи (Delete):
```injectablephp
<?php
// Пример для таблицы "users"

$idToDelete = 2;

try {
    $sql = "DELETE FROM users WHERE id = :id";
    $stmt = $conn->prepare($sql);

    $stmt->execute([
        'id'=>$idToDelete    
    ]);

    echo "Запись успешно удалена";
} catch (PDOException $e) {
    echo "Ошибка: " . $e->getMessage();
}
?>

```
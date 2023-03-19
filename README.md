<h1 align="center">Крестики - нолики 3x3</h1>
ASP.NET (C#) REST API для игры "Крестики - нолики 3x3" для двух игроков. Все игровые данные сохраняются в файлике. Игра написана на C# и использует веб-API ASP.NET. Игроки по очереди расставляют свои метки (X или O) на поле. Первый игрок, который поставит три метки подряд (по горизонтали, вертикали или диагонали), побеждает в игре.
<h2 align="center">Описание REST API</h2>
POST /api/game

Ход игры всегда начинается с X!

Этот запрос позволяет вам сделать ход на поле. Чтобы сделать ход, вы должны отправить объект Move в теле запроса. Объект Move имеет два свойства: Row и Column, которые указывают место, где вы хотите разместить свою метку на доске.

Если перемещение действительно (т.е. указанное место еще не занято), API обновит поле и вернет сообщение "Move successful" в теле ответа. 
Если ход недействителен, API вернет ответ "Bad Request" с сообщением об ошибке.

Если ход привел к победе, API вернет сообщение "Player {X/O} has won!" в теле ответа.
Если ходы обоих игроков привели к ничье, API вернет сообщение "The game ended in a tie." в теле ответа.

Чтобы начать игру заново, нужно перезагрузить API.
<h2 align="center">Докеризация проекта</h2>
Процесс докеризации включает в себя создание Dockerfile для каждого сервиса и файла docker-compose.yml для оркестровки контейнеров.

<h3 align="center">Условия</h3>
Убедитесь, что у вас установлены следующие ПО:

1. Docker
2. docker-compose
3. Visual Studio 2022
<h3 align="center">Запуск и остановка проекта</h3>
Чтобы запустить проект с помощью Docker и Visual Studio 2022, выполните следующие шаги:

1. Клонируйте репозиторий и откройте проект в Visual Studio 2022
2. В Visual Studio нажмите F5, чтобы запустить проект и контейнер, который создаётся вместе с запуском проекта.

Чтобы остановить проект, в Visual Studio повторно нажмите F5.
<h2 align="center">Доступ к контейнеру через Swagger</h2>
Чтобы получить доступ к контейнеру, откройте веб-браузер и перейдите по адресу http://localhost:<port>/swagger/index.html
<h2 align="center">Тестирование кода с помощью Swagger</h2>
Чтобы протестировать код игры Крестики - Нолики с помощью Swagger, выполните следующие действия:

1. Откройте проект в Visual Studio.
2. Запустите проект, нажав клавишу F5.
3. Откройте веб-браузер и перейдите по адресу https://localhost:<port>/swagger/index.html, где <port> - это номер порта, указанный в свойствах проекта.
4. Раскройте конечную точку "Game" и нажмите "Try it out".
5. Введите значения строк и столбцов для вашего хода в разделе "Тело запроса".
6. Нажмите "Выполнить", чтобы увидеть ответ игры.

<h3 align="center">Пример</h3>
Запрос:

```POST /api/game HTTP/1.1
Content-Type: application/json

{
    "Row": 1,
    "Column": 2
}
```
Ответ:

```HTTP/1.1 200 OK
Content-Type: text/plain; charset=utf-8

Move successful
```
<h2 align="center">Сохранение данных в JSON</h2>
Код игры сохраняет данные игрового поля в файл JSON с именем data.json. Этот файл находится в корневом каталоге проекта.

Каждый раз, когда игрок делает ход, код сериализует игровое поле в строку JSON и записывает ее в файл data.json с помощью метода System.IO.File.WriteAllText().

Чтобы просмотреть данные игрового поля, откройте файл data.json в текстовом редакторе или в программе просмотра JSON. Данные будут в формате двумерного списка, где нулевые значения представляют пустые клетки, а значения "X" и "O" - ходы, сделанные соответствующими игроками.


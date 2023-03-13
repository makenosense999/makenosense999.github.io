<h1 align="center">Крестики - нолики 3x3</h1>
ASP.NET (C#) REST API для игры "Крестики - нолики 3x3" для двух игроков. Все игровые данные сохраняются в файлике. Игра написана на C# и использует веб-API ASP.NET. Игроки по очереди расставляют свои метки (X или O) на поле. Первый игрок, который поставит три метки подряд (по горизонтали, вертикали или диагонали), побеждает в игре.
<h2 align="center">Описание REST API</h2>
POST /api/game
Этот запрос позволяет вам сделать ход на доске Tic Tac Toe. Чтобы сделать ход, вы должны отправить объект Move в теле запроса. Объект Move имеет два свойства: Row и Column, которые указывают место, где вы хотите разместить свою метку на доске.

Если перемещение действительно (т.е. указанное место еще не занято), API обновит поле и вернет сообщение "Move successful" в теле ответа. 
Если ход недействителен, API вернет ответ "Bad Request" с сообщением об ошибке.

Если ход привел к победе, API вернет сообщение "Игрок {X/O} победил!" в теле ответа.
<h2 align="center">Пример</h2>
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

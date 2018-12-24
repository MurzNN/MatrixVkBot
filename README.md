Бот позволяет получать и отправлять сообщения VK находясь в Matrix

Бот не требует наличия собственного matrix-сервера, он работает просто как бот.
Логика работы следующая:
1. Пользователь добавляет в матрице бота к себе в контаты
2. авторизует бота в ВК
3. При поступлении новых сообщений в ВК - бот создаёт новую комнату, приглашает туда пользователя и переименовывает эту комнату по названию диалога в ВК ну и сообщения туда шлёт из ВК :-)
4. Пользователь может (через команды) попросить бота вывести список всех диалогов в ВК и открыть нужный диалог в матрице (через создание новой комнаты как в п.2)
5. Если диалог - это групповой чат, то бот к каждой реплике в комнате группового чата добавляет префиксом ФИО отправителя.

Настройка:

1. Заводим обычную учётку для бота в матрице на каком-либо сервере матрицы (вида @botvk:matrix.org)
2. Скачиваем себе бота:  git clone https://github.com/progserega/MatrixVkBot.git
3. Копируем конфиг: cp config.py.example config.y
4. Правим в этом конфиге логин-пароль для учётки бота (с п.1)
5. Запускаем бота: ./bot.py 
6. Добавляем бота к себе в контакты
7. Пишем ему команду: !login
8. Следуем инструкциям от бота (для логина команду: !login).

Для авторизации бот попросит (после ввода команды !login) провести следующий диалог:
1. попросит создать VKapp в ВК (даст ссылку)
2. Зайти в настройки VKapp и скопировать его id
3. отправить этот ID боту
4. бот в ответ отправит ссылку по которой пользователь должен зайти в браузере и согласиться на доступ.
5. После соглашения произойдёт редирект на страничку с предупреждающим текстом
6. Скопировать адрес этой странички и отправить её боту
7. После этого, если всё пройдёт удачно - бот сообщит, что вы вошли под "Ваше ФИО"

Использование:
1. Новые сообщения в диалогах из ВК будут приниматься ботом и отправляться во вновь созданные комнтаты в матрице с именем диалога в ВК
2. Для того, чтобы отправить сообщение в диалог в ВК, нужно передать боту команду: !dialogs
3. Бот выведет список диалогов и их порядковые номера
4. Необходимо в ответном сообщении боту отправить номер нужного диалога 
5. Бот создаст новую комнату (если её нет для этого диалога) и пригласит туда пользователя

Недоработки:
1. Пока не реализована команда !logout
2. В случае, если пользователь вышел из комнаты, связанной с диалогом в ВК - бот это не отслеживает и "диалог потеряется". Нужно добавлять обработчик на выход пользователя из комнаты и чистку структуры этой комнаты в боте. Пока это можно решить удалением файла data.json в директории бота, где бот хранит временные структуры. Но тогда придётся заново проходить процедуру логина. Наверное это самая неприятная недоработка.
3. Пока поддерживается отправка/приём только чистого текста. Без поддержки ответов и т.п.



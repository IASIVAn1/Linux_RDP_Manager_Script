# Linux_RDP_Manager_Script

RDP-менеджер вроде mRemoteNG или RDCMan, только ввиде файлов и в командной строке - как и весь GNU/Linux.
В нём можно сохранить часто используемые, доступные по RDP узлы с IP-адресами, именами пользователя, и при желании, паролями(не безопасно).

### Зависимости
Всего лишь `xfreerdp`, `bash`, `grep`, `tmux`, `echo`. <br>
Они должны вызываться по этим именам. Установите их через пакетный менеджер, либо вручную и добавьте
в path или сделайте alias - как угодно.

### Инструкция
1. Создайте папку, в которой Вы будете хранить файлы сохранённых узлов.
```
mkdir ~/lrdpms
cd ~/lrdpms
```
2. Скачайте lrdpms в эту папку и сделайте его исполняемым. Это шаблон.
```
curl https://gitverse.ru/api/repos/IASIVAn/Linux_RDP_Manager_Script/raw/branch/master/lrdpms -O
chmod +x lrdpms
```
3. Копируйте шаблон, и назовите копию именем узла.
```
cp lrdpms ias-arbuz
```
4. Редактируйте новый файл. В строках после заголовка "Данные для входа" укажите IP-адрес или имя узла,
имя пользователя, домен, пароль.
```
nano ias-arbuz
```
5. Запустите только что созданный файл узла чтобы подключиться, введите данные, если они будут
запрошены.
```
./ias-arbuz
```
6. Приложение xfreerdp, что является RDP-клиентом запущено в эмуляторе терминала tmux. По сути
терминал в терминале. Не закрывая сессию, можете свернуть tmux нажав `ctrl+b`, затем `d`, и
паралельно запустить другой фал - подключиться у ещё одному узлу. Любое количество узлов одновременно.
Можете смотреть список активных сессий `tmux ls` и переключиться к любой из них `tmux attach -t ias-arbuz`.
Сессии tmux называются так же как Вы назвали файлы узлов.

### О настройках
Если не хотитите сохранять что-то из этого - просто
закоментируйте строку. Если этот параметр потребуется при подключении, он будет
запрошен в интеравтином режиме. <br>
Не трогайте `/u:`, `/d:`, и `/p:` - это ключи, указывающие приложению xfreerdp на
назначения поля.
```
#!/bin/bash
#       +------------------+
#       | Данные для входа |
#       +------------------+
export host='127.0.0.1'
export login='/u:nastya'
export domian='/d:ias-home'
#export password='/p:123'
```
Здесь указаны
<br>
Адрес узла: `127.0.0.1`
<br>
Имя пользователя: `nastya`
<br>

Домен: `ias-home`
<br>
Строка с паролем закомментированна, пароль будет запрошен интерактивно при подключении.
<br>
Адрес узла нужно обязательно указать. Имя пользователя - если не указать его, будет
использовано имя учётной записи, от имени которой запущен скрипт. Домен - если целевой узел не
входит в Active Dirrectory, то можно указывать всё что угодно или вовсе закоментировать.
<br>
Если разбираетесь в приложении xfreerdp - чуть ниже можете править команду параметры, с которыми
его запускает скрипт.
<br>

### Концепция
Создавайте файлы узлов, которые вам часто нужны чтобы подключаться к ним быстрее.
Сортируйте их по папкам. Делитесь ими с коллегами.
Назначайте права, если это многопользовательская система.
Обращайтесь с ними как с обычными файлами.
lrdpms портативный и не требует установки.
<br><br>
Демонстрация [Видео](https://iasivan.ru/share/%d0%94%d0%b5%d0%bc%d0%be%d0%bd%d1%81%d1%82%d1%80%d0%b0%d1%86%d0%b8%d1%8f%20lrdp.mp4)

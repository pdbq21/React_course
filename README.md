Step 1. Подготовка
    - Cтруктурa файлов i папок
        +-- js
        |    +-- react
        |        +-- react-dom.js (скопируйте из архива из папки build)
        |        +-- react.js (скопируйте из архива из папки build)
        |    +-- app.js
        +-- index.html
        +-- package.json
        +-- server.js
    
    - Локальный сервер
        -- package.json
            {
              "name": "React-course",
              "version": "1.0.0",
              "description": "React tutorial",
              "main": "index.html",
              "scripts": {
                "start": "node server.js"
              },
              "author": "Ruslan",
              "license": "MIT"
            }
       
        -- Локальный сервер:
            Создадим с помощью Node.js* и express локальный сервер
                npm install express --save-dev
                При использовании флага --save-dev, пакет express добавится в список зависимостей нашего проекта.
                
        -- server.js
                var express = require('express');
                var app = express();
                
                app.set('port', (process.env.PORT || 3000));
                
                app.use('/', express.static(__dirname));
                
                app.listen(app.get('port'), function() {
                  console.log('Server started: http://localhost:' + app.get('port') + '/');
                });
            
        -- index.html
            <!DOCTYPE html>
            <html>
              <head>
                <title>React Tutorial</title>
              </head>
              <body>
                <div id="root">Привет, я #root</div>
              </body>
            </html>
            
        -- Запустите наш сервер node server.js
            npm start
            это возможно, потому что у нас в файле package.json есть секция scripts, в которой указана команда start.
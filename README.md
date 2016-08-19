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
                Note:
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
            Note:
                это возможно, потому что у нас в файле package.json есть секция scripts, в которой указана команда start.
            
                        
Step 2. Подключаем react 

    - index.html
        ...
            <script src="js/react/react.js"></script>
            <script src="js/react/react-dom.js"></script>
            <script src="js/app.js"></script>
          </body>
        </html>
        
    - js/app.js
        ReactDOM.render(
          React.createElement('h1', null, 'Hello, Word!'),
          document.getElementById('root')
        );
        Or
        ReactDOM.render(
                  <h1>Hello, world!</h1>,   // JSX
                  document.getElementById('root')
                );
        Note:
            ReactDOM.render, принимает первым аргументом - реакт-компонент, а вторым - элемент DOM дерева, куда мы хотим добавить react.
    - babel
        -- browser.min.js - CDN:https://cdnjs.cloudflare.com/ajax/libs/babel-core/5.8.23/browser.min.js
    
    - index.html
        <script src="js/react/react.js"></script>
            <script src="js/react/react-dom.js"></script>
            <script src="js/react/browser.min.js"></script>
            <script type="text/babel" src="js/app.js"></script>
          </body>
        </html>
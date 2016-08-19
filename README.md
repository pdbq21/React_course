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
            ...
            <script src="js/react/react.js"></script>
            <script src="js/react/react-dom.js"></script>
            <script src="js/react/browser.min.js"></script>
            <script type="text/babel" src="js/app.js"></script>
          </body>
        </html>
        
    
Step 3. Создание компонента
    
    - js/app.js
        var App = React.createClass({
          render: function() {
            return (
              <div className="app">
                Всем привет, я компонент App!
              </div>
            );
          }
        });
        
        ReactDOM.render(
          <App />,
          document.getElementById('root')
        );
        
        Node: 
            I instal:
                npm install --save-dev babel-cli;
                npm install babel-preset-es2015 --save-dev
            Create:
                .babelrc
                    {
                      "presets": ["es2015"]
                    }
    - js/app.js
        var News = React.createClass({
          render: function() {
            return (
              <div className="news">
                К сожалению, новостей нет.
              </div>
            );
          }
        });
        
        var Comments = React.createClass({
          render: function() {
            return (
              <div className="comments">
                Нет новостей - комментировать нечего
              </div>
            );
          }
        });
        
        var App = React.createClass({
          render: function() {
            return (
              <div className="app">
                Всем привет, я компонент App! Я умею отображать новости.
                <News />
                <Comments />
              </div>
            );
          }
        });
        
        ReactDOM.render(
          <App />,
          document.getElementById('root')
        );
        
    - install React Developer Tools
        https://chrome.google.com/webstore/detail/react-developer-tools/fmkadmapgofadopljbjfkapdkoienihi
        
        
        

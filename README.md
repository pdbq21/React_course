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
        
        
        
Step 4. Использование props
        
    - Node:
        -- У каждого компонента могут быть свойства. Они хранятся в this.props, и передаются компоненту как атрибуты, только для чтения.
        -- комментарии внутри JSX пишутся в фигурных скобках: {/* текст комментария */}
        -- запомнить - внутри return всегда должен возвращаться DOM-узел (то есть, что угодно, обернутое в родительский тэг).
        -- Самый идеальный key — это id
        
    - js/app.js
        var my_news = [
            {
                author: 'Саша Печкин',
                text: 'В четчерг, четвертого числа...'
            },
            {
                author: 'Просто Вася',
                text: 'Считаю, что $ должен стоить 35 рублей!'
            },
            {
                author: 'Гость',
                text: 'Бесплатно. Скачать. Лучший сайт - http://localhost:3000'
            }
        ];
        
        var News = React.createClass({
            render: function() {
                var data = this.props.data;
                var newsTemplate = data.map(function(item, index) {
                    return (
                        <div key={index}>
                            <p className="news__author">{item.author}:</p>
                            <p className="news__text">{item.text}</p>
                        </div>
                    )
                });
        
                return (
                    <div className="news">
                        {newsTemplate}
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
                        <News data={my_news} />
                        <Comments />
                    </div>
                );
            }
        });
        
        ReactDOM.render(
            <App />,
            document.getElementById('root')
        );
        

Step 5. If-else, тернарный оператор

    - css/app.css
        .none {
            display: none !important;
        }
    
    - index.html
            ...
            <link rel="stylesheet" href="css/app.css">
        </head>
        ...
        
    - js/app.js        
        var my_news = [
            {
                author: 'Саша Печкин',
                text: 'В четчерг, четвертого числа...'
            },
            {
                author: 'Просто Вася',
                text: 'Считаю, что $ должен стоить 35 рублей!'
            },
            {
                author: 'Гость',
                text: 'Бесплатно. Скачать. Лучший сайт - http://localhost:3000'
            }
        ];
        
        var News = React.createClass({
            render: function() {
                var data = this.props.data;
                var newsTemplate;
        
                if (data.length > 0) {
                    newsTemplate = data.map(function(item, index) {
                        return (
                            <div key={index}>
                                <p className="news__author">{item.author}:</p>
                                <p className="news__text">{item.text}</p>
                            </div>
                        )
                    })
                } else {
                    newsTemplate = <p>К сожалению новостей нет</p>
                }
        
                return (
                    <div className="news">
                        {newsTemplate}
                        <strong className={data.length > 0 ? '':'none'}>Всего новостей: {data.length}</strong>
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
                        <News data={my_news} />
                        <Comments />
                    </div>
                );
            }
        });
        
        ReactDOM.render(
            <App />,
            document.getElementById('root')
        );
        
        
Step 6. Порефакторим...        
        
    - css/app.css
        .none {
          display: none !important;
        }
        
        body {
          background: rgba(0, 102, 255, 0.38);
          font-family: sans-serif;
        }
        
        p {
          margin: 0 0 5px;
        }
        
        .article {
          background: #FFF;
          border: 1px solid rgba(0, 89, 181, 0.82);
          width: 600px;
          margin: 0 0 5px;
          box-shadow: 2px 2px 5px -1px rgb(0, 81, 202);
          padding: 3px 5px;
        }
        
        .news__author {
          text-decoration: underline;
          color: #007DDC;
        }
        .news__count {
          margin: 10px 0 0 0;
          display: block;
        }            
    
    - js/app.js
        var my_news = [
          {
            author: 'Саша Печкин',
            text: 'В четчерг, четвертого числа...'
          },
          {
            author: 'Просто Вася',
            text: 'Считаю, что $ должен стоить 35 рублей!'
          },
          {
            author: 'Гость',
            text: 'Бесплатно. Скачать. Лучший сайт - http://localhost:3000'
          }
        ];
        
        var Article = React.createClass({
          render: function() {
            var author = this.props.data.author,
                text = this.props.data.text;
        
            return (
              <div className='article'>
                <p className='news__author'>{author}:</p>
                <p className='news__text'>{text}</p>
              </div>
            )
          }
        });
        
        var News = React.createClass({
          render: function() {
            var data = this.props.data;
            var newsTemplate;
        
            if (data.length > 0) {
              newsTemplate = data.map(function(item, index) {
                return (
                  <div key={index}>
                    <Article data={item} />
                  </div>
                )
              })
            } else {
              newsTemplate = <p>К сожалению новостей нет</p>
            }
        
            return (
              <div className='news'>
                {newsTemplate}
                <strong className={'news__count ' + (data.length > 0 ? '':'none') }>Всего новостей: {data.length}</strong>
              </div>
            );
          }
        });
        
        var App = React.createClass({
          render: function() {
            return (
              <div className='app'>
                <h3>Новости</h3>
                <News data={my_news} />
              </div>
            );
          }
        });
        
        ReactDOM.render(
          <App />,
          document.getElementById('root')
        );               
                
            
Step 7. React.propTypes
    - Node:
        React.createClass({
          propTypes: {
            // Вы можете указать, каким примитивом должно быть свойство
            optionalArray: React.PropTypes.array,
            optionalBool: React.PropTypes.bool,
            optionalFunc: React.PropTypes.func,
            optionalNumber: React.PropTypes.number,
            optionalObject: React.PropTypes.object,
            optionalString: React.PropTypes.string,
        
            // Вы может указать, что свойство можеть быть одни из ...
            optionalUnion: React.PropTypes.oneOfType([
              React.PropTypes.string,
              React.PropTypes.number,
              React.PropTypes.instanceOf(Message)
            ]),
        
            // Вы можете указать, конкретную структуру объекта свойства
            optionalObjectWithShape: React.PropTypes.shape({
              color: React.PropTypes.string,
              fontSize: React.PropTypes.number
            }),
        
            // Вы можете указать, что свойство ОБЯЗАТЕЛЬНО
            requiredFunc: React.PropTypes.func.isRequired,
        
            // Если нужно указать, что свойство просто обязательно, и может быть любым примитивом
            requiredAny: React.PropTypes.any.isRequired,
        
          }
        });
        
        
Step 8. Использование state
        
    - Note:
         -- Как вы помните, свойства (this.props) следует использовать только для чтения, 
            а для динамических свойств нужно использовать так называемое "состояние" (state).
         -- Если вы определяете какое-то изменяемое свойство в компоненте, необходимо указать начальное состояние (в терминологии react.js - initial state). 
            Для этого, у компонента указывается метод getInitialState
         -- Чтобы обработать клик, нам необходимо указать атрибут onClick у элемента.
         -- Для изменения состояния, нужно обязательно использовать метод setState, а не просто перезаписывать значение переменной.
     
    - js/app.js               


Step 8.1. Продвинутое использование state

    - Note:
        -- первое правило: нельзя вызывать setState в render: 
           реакт видит изменилось состояние - начинает перерисовывать компонент - видит что изменилось состояние - начинает перерисовывать компонент...
        -- Второе правило: render - дорогостоящая операция, поэтому внимательно относитесь к тому, где вы вызываете setState, и что это за собой влечет.    
        -- this.setState({counter: ++this.state.counter })
        -- setState() - не изменяет this.state немедленно, а создает очередь изменений состояния. 
           Доступ к this.state после вызова метода, потенциально может вернуть имеющееся (что равносильно - бывшее) значение.
    - js/app.js
           
           
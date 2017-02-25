Init
====
    npm init -y
В созданной папке пока что лежит одинокий файл package.json. 
-----
Писать код мы будем в спецификации ES6. 
Хотя Node начиная с версии 4.0.0 поддерживает много возможностей ES6, 
необходимые нам модули все же остались за бортом. 
Поэтому нам нужно добавить в наш проект Babel, чтобы мы могли воспользоваться всей мощью ES6 и транспилировать 
код в ES5
    npm install --save-dev babel-core babel-cli babel-preset-es2015

Также нам понадобятся библиотеки для написания unit тестов: 
-----
    npm install --save-dev mocha chai

В качестве фреймворка для тестирования будем использовать Mocha. Внутри тестов будем использовать Chai в роли библиотеки для проверки ожидаемого поведения и состояний. Запускать тесты мы будем с помощью команды mocha:

    ./node_modules/mocha/bin/mocha --compilers js:babel-core/register --recursive

После этого Mocha будет рекурсивно искать все тесты проекта и запускать их. Для транспилинга ES6-кода перед его запуском будет использоваться Babel. Для удобства можно хранить эту команду в package.json:

    package.json
    "scripts": {
      "test": "mocha --compilers js:babel-core/register --recursive"
    },

Теперь нам нужно включить в Babel поддержку ES6/ES2015. Для этого активируем уже установленный нами пакет babel-preset-es2015. Далее просто добавим в package.json секцию "babel":
    
    package.json
    "babel": {
      "presets": ["es2015"]
    }
    
Теперь с помощью команды npm мы можем запускать наши тесты:

    npm run test

Команда test:watch может использоваться для запуска процесса, отслеживающего изменения в нашем коде и запускающего тесты после каждого изменения:

    package.json
    "scripts": {
      "test": "mocha --compilers js:babel-core/register --recursive",
      "test:watch": "npm run test -- --watch"
    },

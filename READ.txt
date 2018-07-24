https://github.com/JeffreyWay/laravel-mix
https://github.com/JeffreyWay/laravel-mix/tree/master/docs#readme
https://laravel.com/docs/5.6/mix


1. Этот пункт выполняем для Windows, и если еще не установлен
глобально пакет cross-env

    npm install --global cross-env


2. В корне проекта открываем GitBash и набираем поочередно команды

npm init -y
npm i -D laravel-mix
cp -r node_modules/laravel-mix/setup/webpack.mix.js  ./

В корне проекта появиться файл webpack.mix.js


3. В файл  package.json  секция  scripts выглядит так


===================== Для Windows ====================
  "scripts": {
    "dev": "cross-env NODE_ENV=development node_modules/webpack/bin/webpack.js --progress --hide-modules --config=node_modules/laravel-mix/setup/webpack.config.js",
    "watch": "cross-env  NODE_ENV=development node_modules/webpack/bin/webpack.js --watch --progress --hide-modules --config=node_modules/laravel-mix/setup/webpack.config.js",
    "hot": "cross-env  NODE_ENV=development webpack-dev-server --inline --hot --config=node_modules/laravel-mix/setup/webpack.config.js",
    "production": "cross-env  NODE_ENV=production node_modules/webpack/bin/webpack.js --progress --hide-modules --config=node_modules/laravel-mix/setup/webpack.config.js"
  }

=================  MacOS =================

  "scripts": {
    "dev": "NODE_ENV=development node_modules/webpack/bin/webpack.js --progress --hide-modules --config=node_modules/laravel-mix/setup/webpack.config.js",
    "watch": "NODE_ENV=development node_modules/webpack/bin/webpack.js --watch --progress --hide-modules --config=node_modules/laravel-mix/setup/webpack.config.js",
    "hot": "NODE_ENV=development webpack-dev-server --inline --hot --config=node_modules/laravel-mix/setup/webpack.config.js",
    "production": "NODE_ENV=production node_modules/webpack/bin/webpack.js --progress --hide-modules --config=node_modules/laravel-mix/setup/webpack.config.js"
  }


4. В корне проекта создаем
 - файл index.html
 - каталоги  src, dist, i, fonts
 - в каталоге src  создаем  каталог scss и в нем style.scss


5.  webpack.mix.js
----------------------------------------------
let mix = require('laravel-mix');

mix.copy('src/*.html', 'dist/')
   .copyDirectory('src/i', 'dist/i/')
   .copyDirectory('src/fonts', 'dist/fonts/')
   .sass('src/scss/style.scss', 'dist/css/')
   .combine([
        'browserDetect.js',
        'ssm.min.js',
        'script.js'
    ], 'dist/script.js')
   //.js('src/js/app.js', 'dist/js/')
   .browserSync({
        proxy: "",
        server: "dist",
        files: ["dist/css/**/*.css", "dist/js/**/*.js", 'dist/*.html']
   })
   .options({
        processCssUrls: false
    })
   .setPublicPath('dist');

------------------------------------------------
6. Команды для работы
   npm run watch
   npm run production

!!! При первом, после установки,  запуске сначала запустится установка дополнительніх зависимосмей
Будет сообщение
   Additional dependencies must be installed. This will only take a moment.

Послу установки появиться сообщение
   Finished. Please run Mix again.

Теперь можно работать, запуская вышеописанные команды


============================= Help
----------- X-UA-Compatible
http://xiper.net/manuals/html/meta-tags/http-equiv/x-ua-compatible







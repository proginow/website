---
title: Router
description: Routing And Router Library
published: true
date: 2024-02-27T05:48:07.634Z
tags: framework, proginow, router, routing
editor: markdown
dateCreated: 2024-02-27T05:48:03.581Z
---

# Router
[Source Code On Github](https://github.com/proginow/router/)
[Package On Packagist](https://packagist.org/packages/proginow/router/)
## Installation
```
composer require proginow/router
```
## Usage


 1. Enable URL rewriting on your web server

    * Apache (in `.htaccess` or `httpd.conf`)

      ```
      RewriteEngine On
      RewriteCond %{REQUEST_FILENAME} !-f
      RewriteRule . index.php [L]
      ```

    * Nginx (in `nginx.conf`)

      ```
      try_files $uri /index.php;
      ```

 2. Create a new `Router` instance

    * for the web root

      ```php
      $router = new \Proginow\Router\Router();
      ```

    * for any subdirectory

      ```php
      $router = new \Proginow\Router\Router('/my/base/path');
      ```

 3. Add some routes and map them to anonymous functions or closures

    * Static route:

      ```php
      $router->get('/', function () {
          // do something
      });
      ```

    * Dynamic route (with parameters):

      ```php
      $router->get('/users/:id/photo', function ($id) {
          // get the photo for user `$id`
      });
      ```

      The values of parameters matched in the URL can be captured as arguments in the callback.

    * Route with multiple supported request methods:

      ```php
      $router->any([ 'POST', 'PUT' ], '/users/:id/address', function ($id) {
          // update the address for user `$id`
      });
      ```

 4. Map routes to controller methods instead for more complex callbacks

    ```php
    // use static methods
    $router->get('/photos/:id/convert/:mode', [ 'PhotoController', 'myStaticMethod' ]);

    // or

    // instance methods
    $router->get('/photos/:id/convert/:mode', [ $myPhotoController, 'myInstanceMethod' ]);
    ```

 5. Inject arguments for access to further values and objects (prepended to those matched in the route)

    ```php
    class MyController {

        public static function someStaticMethod($database, $uuid) {
            // do something
        }

    }
    ```

    and

    ```php
    $database = new MyDatabase();

    // ...

    $router->delete('/messages/:uuid', [ 'MyController', 'someStaticMethod' ], [ $database ]);
    ```

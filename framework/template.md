---
title: Template
description: Template Engine Library
published: true
date: 2024-02-26T10:48:48.429Z
tags: framework, blade, laravel, engine
editor: markdown
dateCreated: 2024-02-26T10:48:44.727Z
---

# Template
[Source Code On Github](https://github.com/proginow/template/)
[Package On Packagist](https://packagist.org/packages/proginow/template/)
## Installation
```
composer require proginow/template
```
## Usage
```php
<?php

require __DIR__.'/vendor/autoload.php';

use Proginow\Blade\Blade;

$views = __DIR__ . '/views';
$cache = __DIR__ . '/cache';

$blade = new Blade($views, $cache);
echo $blade->view()->make('hello')->render();
```

You can use all blade features as described in the Laravel documentation:
https://laravel.com/docs/master/blade
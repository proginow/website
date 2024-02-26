---
title: Cookie
description: Cookie And Session Library
published: true
date: 2024-02-26T09:03:16.963Z
tags: cookie, framework, proginow, session
editor: markdown
dateCreated: 2024-02-26T09:00:31.488Z
---

# Cookie
[Source Code On Github](https://github.com/proginow/cookie/)
[Package On Packagist](https://packagist.org/packages/proginow/cookie/)
## Installation
```
composer require proginow/cookie
```
## Usage

### Static method

This library provides a static method that is compatible to PHP’s built-in `setcookie(...)` function but includes support for more recent features such as the `SameSite` attribute:

```php
\Proginow\Cookie\Cookie::setcookie('SID', '31d4d96e407aad42');
// or
\Proginow\Cookie\Cookie::setcookie('SID', '31d4d96e407aad42', time() + 3600, '/~rasmus/', 'example.com', true, true, 'Lax');
```

### Builder pattern

Instances of the `Cookie` class let you build a cookie conveniently by setting individual properties. This class uses reasonable defaults that may differ from defaults of the `setcookie` function.

```php
$cookie = new \Proginow\Cookie\Cookie('SID');
$cookie->setValue('31d4d96e407aad42');
$cookie->setMaxAge(60 * 60 * 24);
// $cookie->setExpiryTime(time() + 60 * 60 * 24);
$cookie->setPath('/~rasmus/');
$cookie->setDomain('example.com');
$cookie->setHttpOnly(true);
$cookie->setSecureOnly(true);
$cookie->setSameSiteRestriction('Strict');

// echo $cookie;
// or
$cookie->save();
// or
// $cookie->saveAndSet();
```

The method calls can also be chained:

```php
(new \Proginow\Cookie\Cookie('SID'))->setValue('31d4d96e407aad42')->setMaxAge(60 * 60 * 24)->setSameSiteRestriction('None')->save();
```

A cookie can later be deleted simply like this:

```php
$cookie->delete();
// or
$cookie->deleteAndUnset();
```

**Note:** For the deletion to work, the cookie must have the same settings as the cookie that was originally saved – except for its value, which doesn’t need to be set. So you should remember to pass appropriate values to `setPath(...)`, `setDomain(...)`, `setHttpOnly(...)` and `setSecureOnly(...)` again.

### Reading cookies

 * Checking whether a cookie exists:

   ```php
   \Proginow\Cookie\Cookie::exists('first_visit');
   ```

 * Reading a cookie’s value (with optional default value):

   ```php
   \Proginow\Cookie\Cookie::get('first_visit');
   // or
   \Proginow\Cookie\Cookie::get('first_visit', \time());
   ```

### Managing sessions

Using the `Session` class, you can start and resume sessions in a way that is compatible to PHP’s built-in `session_start()` function, while having access to the improved cookie handling from this library as well:

```php
// start session and have session cookie with 'lax' same-site restriction
\Proginow\Cookie\Session::start();
// or
\Proginow\Cookie\Session::start('Lax');

// start session and have session cookie with 'strict' same-site restriction
\Proginow\Cookie\Session::start('Strict');

// start session and have session cookie without any same-site restriction
\Proginow\Cookie\Session::start(null);
// or
\Proginow\Cookie\Session::start('None'); // Chrome 80+
```

All three calls respect the settings from PHP’s `session_set_cookie_params(...)` function and the configuration options `session.name`, `session.cookie_lifetime`, `session.cookie_path`, `session.cookie_domain`, `session.cookie_secure`, `session.cookie_httponly` and `session.use_cookies`.

Likewise, replacements for

```php
session_regenerate_id();
// and
session_regenerate_id(true);
```

are available via

```php
\Proginow\Cookie\Session::regenerate();
// and
\Proginow\Cookie\Session::regenerate(true);
```

if you want protection against session fixation attacks that comes with improved cookie handling.

Additionally, access to the current internal session ID is provided via

```php
\Proginow\Cookie\Session::id();
```

as a replacement for

```php
session_id();
```

### Reading and writing session data

 * Read a value from the session (with optional default value):

   ```php
   $value = \Proginow\Cookie\Session::get($key);
   // or
   $value = \Proginow\Cookie\Session::get($key, $defaultValue);
   ```

 * Write a value to the session:

   ```php
   \Proginow\Cookie\Session::set($key, $value);
   ```

 * Check whether a value exists in the session:

   ```php
   if (\Proginow\Cookie\Session::has($key)) {
       // ...
   }
   ```

 * Remove a value from the session:

   ```php
   \Proginow\Cookie\Session::delete($key);
   ```

 * Read *and then* immediately remove a value from the session:

   ```php
   $value = \Proginow\Cookie\Session::take($key);
   $value = \Proginow\Cookie\Session::take($key, $defaultValue);
   ```

   This is often useful for flash messages, e.g. in combination with the `has(...)` method.

### Parsing cookies

```php
$cookieHeader = 'Set-Cookie: test=php.net; expires=Thu, 09-Jun-2016 16:30:32 GMT; Max-Age=3600; path=/~rasmus/; secure';
$cookieInstance = \Proginow\Cookie\Cookie::parse($cookieHeader);
```

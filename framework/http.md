---
title: Http
description: HTTP Utilities Library
published: true
date: 2024-02-26T10:34:15.981Z
tags: framework, http, curl, response
editor: markdown
dateCreated: 2024-02-26T10:34:15.981Z
---

# HTTP
[Source Code On Github](https://github.com/proginow/http/)
[Package On Packagist](https://packagist.org/packages/proginow/http/)
## Installation
```
composer require proginow/http
```
## Usage

### Response headers

 * Retrieving a header (with optional value prefix)

   ```php
   $header = \Proginow\Http\ResponseHeader::get('Content-Type');
   // or
   $header = \Proginow\Http\ResponseHeader::get('Content-Type', 'text/html');
   ```

 * Setting a header (overwriting other headers with the same name)

   ```php
   \Proginow\Http\ResponseHeader::set('X-Frame-Options', 'sameorigin');
   ```

 * Adding a header (preserving other headers with the same name)

   ```php
   \Proginow\Http\ResponseHeader::add('Vary', 'User-Agent');
   ```

 * Removing a header (with optional value prefix)

   ```php
   $success = \Proginow\Http\ResponseHeader::remove('X-Powered-By');
   // or
   $success = \Proginow\Http\ResponseHeader::remove('X-Powered-By', 'PHP');
   ```

 * Retrieving and removing a header at once (with optional value prefix)

   ```php
   $header = \Proginow\Http\ResponseHeader::take('Set-Cookie');
   // or
   $header = \Proginow\Http\ResponseHeader::take('Set-Cookie', 'mysession=test');
   ```

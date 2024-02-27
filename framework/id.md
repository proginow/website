---
title: ID
description:  ID Encode/Decode Library
published: true
date: 2024-02-26T10:59:08.120Z
tags: framework, proginow, id
editor: markdown
dateCreated: 2024-02-26T10:22:01.592Z
---

# ID
[Source Code On Github](https://github.com/proginow/id/)
[Package On Packagist](https://packagist.org/packages/proginow/id/)
## Installation
```
composer require proginow/id
```
## Usage

### Creating an instance

```php
$generator = new \Proginow\Ids\Id();
```

### Encoding and decoding IDs

```php
$generator->encode(6); // => "43Vht7"
$generator->decode('43Vht7'); // => 6
```

### Shortening a number without obfuscating it

```php
$generator->shorten(3141592); // => "vJST"
$generator->unshorten("vJST"); // => 3141592
```

### Obfuscating a number without shortening it

```php
$generator->obfuscate(42); // => 958870139
$generator->deobfuscate(958870139); // => 42
```
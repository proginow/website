---
title: Base64
description: Base64 Encode/Decode Library
published: true
date: 2024-02-26T11:18:43.272Z
tags: framework, proginow, base64
editor: markdown
dateCreated: 2024-02-26T10:59:48.684Z
---

# Base64
[Source Code On Github](https://github.com/proginow/base64/)
[Package On Packagist](https://packagist.org/packages/proginow/base64/)
## Installation
```
composer require proginow/base64
```
## Usage

### Standard

 * Encoding data

   ```php
   \Proginow\Base64\Base64::encode('test');
   ```

 * Decoding data

   ```php
   \Proginow\Base64\Base64::decode('R2FsbGlhIGVzdCBvbW5pcyBkaXZpc2EgaW4gcGFydGVzIHRyZXM=');
   ```

### URL-safe

 * Encoding data

   ```php
   \Proginow\Base64\Base64::encodeUrlSafe('test');
   ```

 * Decoding data

   ```php
   \Proginow\Base64\Base64::decodeUrlSafe('z4DOrM69z4TOsSDPh8-Jz4HOteG_liDOus6x4b22IM6_4b2QzrThvbLOvSDOvM6tzr3Otc65IOKApg~~');
   ```

### URL-safe without padding

 * Encoding data

   ```php
   \Proginow\Base64\Base64::encodeUrlSafeWithoutPadding('test');
   ```

 * Decoding data

   ```php
   \Proginow\Base64\Base64::decodeUrlSafeWithoutPadding('z4DOrM69z4TOsSDPh8-Jz4HOteG_liDOus6x4b22IM6_4b2QzrThvbLOvSDOvM6tzr3Otc65IOKApg');
   ```

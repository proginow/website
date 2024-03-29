---
title: Upload
description: File Upload Library
published: true
date: 2024-02-27T06:00:22.128Z
tags: framework, proginow, upload, file
editor: markdown
dateCreated: 2024-02-27T06:00:17.809Z
---

# Upload
[Source Code On Github](https://github.com/proginow/upload/)
[Package On Packagist](https://packagist.org/packages/proginow/upload/)
## Installation
```
composer require proginow/upload
```

## Usage

 * [File uploads](#file-uploads)
   * [Limiting the maximum permitted file size](#limiting-the-maximum-permitted-file-size)
   * [Reading the maximum permitted file size](#reading-the-maximum-permitted-file-size)
   * [Restricting the allowed file types or extensions](#restricting-the-allowed-file-types-or-extensions)
   * [Reading the allowed file types or extensions](#reading-the-allowed-file-types-or-extensions)
   * [Reading the target directory](#reading-the-target-directory)
   * [Defining the target filename](#defining-the-target-filename)
   * [Reading the target filename](#reading-the-target-filename)
   * [Reading the name of the input field](#reading-the-name-of-the-input-field)
 * [Base64 uploads](#base64-uploads)
   * [Limiting the maximum permitted file size](#limiting-the-maximum-permitted-file-size-1)
   * [Reading the maximum permitted file size](#reading-the-maximum-permitted-file-size-1)
   * [Defining the filename extension](#defining-the-filename-extension)
   * [Reading the filename extension](#reading-the-filename-extension)
   * [Reading the target directory](#reading-the-target-directory-1)
   * [Defining the target filename](#defining-the-target-filename-1)
   * [Reading the target filename](#reading-the-target-filename-1)
   * [Reading the Base64 data](#reading-the-base64-data)
 * [Data URI uploads](#data-uri-uploads)
   * [Limiting the maximum permitted file size](#limiting-the-maximum-permitted-file-size-2)
   * [Reading the maximum permitted file size](#reading-the-maximum-permitted-file-size-2)
   * [Restricting the allowed MIME types and extensions](#restricting-the-allowed-mime-types-and-extensions)
   * [Reading the allowed MIME types and extensions](#reading-the-allowed-mime-types-and-extensions)
   * [Reading the target directory](#reading-the-target-directory-2)
   * [Defining the target filename](#defining-the-target-filename-2)
   * [Reading the target filename](#reading-the-target-filename-2)
   * [Reading the data URI](#reading-the-data-uri)

### File uploads

```php
$upload = new \Proginow\FileUpload\FileUpload();
$upload->withTargetDirectory('/my-app/users/' . $userId . '/avatars');
$upload->from('my-input-name');

try {
    $uploadedFile = $upload->save();

    // success

    // $uploadedFile->getFilenameWithExtension()
    // $uploadedFile->getFilename()
    // $uploadedFile->getExtension()
    // $uploadedFile->getDirectory()
    // $uploadedFile->getPath()
    // $uploadedFile->getCanonicalPath()
}
catch (\Proginow\FileUpload\Throwable\InputNotFoundException $e) {
    // input not found
}
catch (\Proginow\FileUpload\Throwable\InvalidFilenameException $e) {
    // invalid filename
}
catch (\Proginow\FileUpload\Throwable\InvalidExtensionException $e) {
    // invalid extension
}
catch (\Proginow\FileUpload\Throwable\FileTooLargeException $e) {
    // file too large
}
catch (\Proginow\FileUpload\Throwable\UploadCancelledException $e) {
    // upload cancelled
}
```

#### Limiting the maximum permitted file size

```php
$upload->withMaximumSizeInBytes(4194304);

// or

$upload->withMaximumSizeInKilobytes(4096);

// or

$upload->withMaximumSizeInMegabytes(4);
```

#### Reading the maximum permitted file size

```php
// e.g. int(4194304)
$upload->getMaximumSizeInBytes();

// or

// e.g. int(4096)
$upload->getMaximumSizeInKilobytes();

// or

// e.g. int(4)
$upload->getMaximumSizeInMegabytes();
```

#### Restricting the allowed file types or extensions

```php
$upload->withAllowedExtensions([ 'jpeg', 'jpg', 'png', 'gif' ]);
```

**Note:** By default, a set of filename extensions is used that is relatively safe for PHP applications and common on the web. This may be sufficient for some use cases.

#### Reading the allowed file types or extensions

```php
// e.g. array(4) { [0]=> string(4) "jpeg" [1]=> string(3) "jpg" [2]=> string(3) "png" [3]=> string(3) "gif" }
$upload->getAllowedExtensionsAsArray();

// or

// e.g. string(16) "jpeg,jpg,png,gif"
$upload->getAllowedExtensionsAsMachineString();

// or

// e.g. string(19) "JPEG, JPG, PNG, GIF"
$upload->getAllowedExtensionsAsHumanString();

// or

// e.g. string(21) "JPEG, JPG, PNG or GIF"
$upload->getAllowedExtensionsAsHumanString(' or ');
```

#### Reading the target directory

```php
// e.g. string(24) "/my-app/users/42/avatars"
$upload->getTargetDirectory();
```

#### Defining the target filename

```php
$upload->withTargetFilename('my-picture');
```

**Note:** By default, a random filename will be used, which is sufficient (and desired) in many cases.

#### Reading the target filename

```php
// e.g. string(10) "my-picture"
$upload->getTargetFilename();
```

#### Reading the name of the input field

```php
// e.g. string(13) "my-input-name"
$upload->getSourceInputName();
```

### Base64 uploads

```php
$upload = new \Proginow\FileUpload\Base64Upload();
$upload->withTargetDirectory('/my-app/users/' . $userId . '/avatars');
$upload->withData($_POST['my-base64']);

try {
    $uploadedFile = $upload->save();

    // success

    // $uploadedFile->getFilenameWithExtension()
    // $uploadedFile->getFilename()
    // $uploadedFile->getExtension()
    // $uploadedFile->getDirectory()
    // $uploadedFile->getPath()
    // $uploadedFile->getCanonicalPath()
}
catch (\Proginow\FileUpload\Throwable\InputNotFoundException $e) {
    // input not found
}
catch (\Proginow\FileUpload\Throwable\InvalidFilenameException $e) {
    // invalid filename
}
catch (\Proginow\FileUpload\Throwable\InvalidExtensionException $e) {
    // invalid extension
}
catch (\Proginow\FileUpload\Throwable\FileTooLargeException $e) {
    // file too large
}
catch (\Proginow\FileUpload\Throwable\UploadCancelledException $e) {
    // upload cancelled
}
```

#### Limiting the maximum permitted file size

```php
$upload->withMaximumSizeInBytes(4194304);

// or

$upload->withMaximumSizeInKilobytes(4096);

// or

$upload->withMaximumSizeInMegabytes(4);
```

#### Reading the maximum permitted file size

```php
// e.g. int(4194304)
$upload->getMaximumSizeInBytes();

// or

// e.g. int(4096)
$upload->getMaximumSizeInKilobytes();

// or

// e.g. int(4)
$upload->getMaximumSizeInMegabytes();
```

#### Defining the filename extension

```php
$upload->withFilenameExtension('png');
```

**Note:** This defines the filename extension of the file *to be uploaded*, which is a property of the `FileUpload` instance. It does *not* change the extension of any file *already* uploaded, which would be represented in a `File` instance. By default, the filename extension `bin` for arbitrary (binary) data will be used, which may be sufficient in some cases.

#### Reading the filename extension

```php
// e.g. string(3) "png"
$upload->getFilenameExtension();
```

**Note:** This retrieves the filename extension of the file *to be uploaded*, which is a property of the `FileUpload` instance. It does *not* read the extension of any file *already* uploaded, which would be represented in a `File` instance.

#### Reading the target directory

```php
// e.g. string(24) "/my-app/users/42/avatars"
$upload->getTargetDirectory();
```

#### Defining the target filename

```php
$upload->withTargetFilename('my-picture');
```

**Note:** By default, a random filename will be used, which is sufficient (and desired) in many cases.

#### Reading the target filename

```php
// e.g. string(10) "my-picture"
$upload->getTargetFilename();
```

#### Reading the Base64 data

```php
// e.g. string(20) "SGVsbG8sIFdvcmxkIQ=="
$upload->getData();
```

### Data URI uploads

```php
$upload = new \Proginow\FileUpload\DataUriUpload();
$upload->withTargetDirectory('/my-app/users/' . $userId . '/avatars');
$upload->withUri($_POST['my-data-uri']);

try {
    $uploadedFile = $upload->save();

    // success

    // $uploadedFile->getFilenameWithExtension()
    // $uploadedFile->getFilename()
    // $uploadedFile->getExtension()
    // $uploadedFile->getDirectory()
    // $uploadedFile->getPath()
    // $uploadedFile->getCanonicalPath()
}
catch (\Proginow\FileUpload\Throwable\InputNotFoundException $e) {
    // input not found
}
catch (\Proginow\FileUpload\Throwable\InvalidFilenameException $e) {
    // invalid filename
}
catch (\Proginow\FileUpload\Throwable\InvalidExtensionException $e) {
    // invalid extension
}
catch (\Proginow\FileUpload\Throwable\FileTooLargeException $e) {
    // file too large
}
catch (\Proginow\FileUpload\Throwable\UploadCancelledException $e) {
    // upload cancelled
}
```

#### Limiting the maximum permitted file size

```php
$upload->withMaximumSizeInBytes(4194304);

// or

$upload->withMaximumSizeInKilobytes(4096);

// or

$upload->withMaximumSizeInMegabytes(4);
```

#### Reading the maximum permitted file size

```php
// e.g. int(4194304)
$upload->getMaximumSizeInBytes();

// or

// e.g. int(4096)
$upload->getMaximumSizeInKilobytes();

// or

// e.g. int(4)
$upload->getMaximumSizeInMegabytes();
```

#### Restricting the allowed MIME types and extensions

```php
$upload->withAllowedMimeTypesAndExtensions([
    'image/jpeg' => 'jpg',
    'image/png' => 'png',
    'image/gif' => 'gif'
]);
```

**Note:** By default, a set of MIME types is used that is relatively safe for PHP applications and common on the web. This may be sufficient for some use cases.

#### Reading the allowed MIME types and extensions

```php
// e.g. array(3) { [0]=> string(10) "image/jpeg" [1]=> string(9) "image/png" [2]=> string(9) "image/gif" }
$upload->getAllowedMimeTypesAsArray();

// or

// e.g. string(30) "image/jpeg,image/png,image/gif"
$upload->getAllowedMimeTypesAsMachineString();

// or

// e.g. string(32) "image/jpeg, image/png, image/gif"
$upload->getAllowedMimeTypesAsHumanString();

// or

// e.g. string(34) "image/jpeg, image/png or image/gif"
$upload->getAllowedMimeTypesAsHumanString(' or ');

// or

// e.g. array(3) { [0]=> string(3) "jpg" [1]=> string(3) "png" [2]=> string(3) "gif" }
$upload->getAllowedExtensionsAsArray();

// or

// e.g. string(11) "jpg,png,gif"
$upload->getAllowedExtensionsAsMachineString();

// or

// e.g. string(13) "JPG, PNG, GIF"
$upload->getAllowedExtensionsAsHumanString();

// or

// e.g. string(15) "JPG, PNG or GIF"
$upload->getAllowedExtensionsAsHumanString(' or ');
```

#### Reading the target directory

```php
// e.g. string(24) "/my-app/users/42/avatars"
$upload->getTargetDirectory();
```

#### Defining the target filename

```php
$upload->withTargetFilename('my-picture');
```

**Note:** By default, a random filename will be used, which is sufficient (and desired) in many cases.

#### Reading the target filename

```php
// e.g. string(10) "my-picture"
$upload->getTargetFilename();
```

#### Reading the data URI

```php
// e.g. string(43) "data:text/plain;base64,SGVsbG8sIFdvcmxkIQ=="
$upload->getUri();
```


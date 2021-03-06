[![StyleCI](https://styleci.io/repos/106752684/shield?branch=master)](https://styleci.io/repos/106752684) [![Maintainability](https://api.codeclimate.com/v1/badges/0c615c480aa201e6214f/maintainability)](https://codeclimate.com/github/marcus-campos/maestro/maintainability)
[![MIT licensed](https://img.shields.io/badge/license-MIT-blue.svg)](./LICENSE)

# Maestro

A light client built on [Guzzle](http://docs.guzzlephp.org/en/latest/) that simplifies the way you work with micro-services. It is based on method definitions and parameters for your URLs.

# Requirements

* PHP 7.0 or greater
* Composer

# Installation

Composer way

```
composer require marcus-campos/maestro
```

Or add manually to your composer.json:

```
"marcus-campos/maestro": "dev-master"
```

# Running the test suite

## Using Docker

```
docker build -t maestro .
docker run maestro
```

# Basic Usage

```php

<?php

namespace App\Platform\V1\Domains\App;


use Maestro\Rest;

class Products extends Rest
{
    protected $url = 'https://mydomain.com/api/v1/'; // http://mydomain.com:9000/api/v1

    /**
     * @return array
     */
    public function getProducts()
    {
        return $this
            ->get()
            ->setEndPoint('products')
            ->headers([
                'Content-Type' => 'application/json'
            ])
            ->body( [
                'ids' => [1,2,3,4,5]
            ])
            ->send()
            ->parse();
    }

    /**
     * @return array
     */
    public function getProduct()
    {
        return $this
            ->get()
            ->setEndPoint('product')
            ->send()
            ->parse();
    }

    /**
     * @return array
     */
    public function postNotification()
    {
        return $this
            ->get()
            ->setEndPoint('package/')
            ->headers([
                'Content-Type' => 'application/json'
            ])
            ->body([
                'message' => 'Tanks for all.',
                'id' => [1]
            ])
            ->sendAsync()
            ->wait()
            ->parse()
            ->name;
    }
}
```

# Response data

By default the returns is a `StdClass`, which gives you the freedom to treat the data the way you want. See the examples:


The way of Laravel

```php
 public function getProducts()
 {
     return collect(
         $this
         ->get()
         ->setEndPoint('products')
         ->headers([
             'Content-Type' => 'application/json'
         ])
         ->body([
             'ids' => [1,2,3,4,5]
         ])
         ->send()
         ->parse());
 }
```

You can choose assoc return.

Assoc way
```php
 public function postNotification()
 {
     return $this
         ->get()
         ->setEndPoint('package/')
         ->headers([
             'Content-Type' => 'application/json'
         ])
         ->body([
             'message' => 'Tanks for all.',
             'id' => [1]
         ])
         ->send()
         ->assoc()
         ->parse()
         ->name;
 }
```

Other way
```php
 public function postNotification()
 {
     return $this
         ->get()
         ->setEndPoint('package/')
         ->headers([
             'Content-Type' => 'application/json'
         ])
         ->body([
             'message' => 'Tanks for all.',
             'id' => [1]
         ])
         ->sendAsync()
         ->wait()
         ->parse()
         ->name;
 }
```

## Senders
You can send in 2 ways: synchronous or asynchronous. See the examples:


Synchronous: `->send()`
```php
 public function getProducts()
 {
     return collect($this
         ->get()
         ->setEndPoint('products')
         ->headers([
             'Content-Type' => 'application/json'
         ])
         ->body([
             'ids' => [1,2,3,4,5]
         ])
         ->send()
         ->parse());
 }
```

Asynchronous: `->sendAsync()`
```php
 public function postNotification()
 {
     return $this
         ->get()
         ->setEndPoint('package/')
         ->headers([
             'Content-Type' => 'application/json'
         ])
         ->body([
             'message' => 'Tanks for all.',
             'id' => [1]
         ])
         ->sendAsync()
         ->wait()
         ->parse()
         ->name;
 }
```



## Supported Methods

- [x] GET    `->get()`
- [x] POST   `->post()`
- [x] PUT    `->put()`
- [x] PATCH  `->patch()`
- [x] DELETE `->delete()`
- [x] COPY `->copy()`
- [x] HEAD `->head()`
- [x] OPTIONS `->options()`
- [x] LINK `->link()`
- [x] UNLINK `->unlink()`
- [x] PURGE `->purge()`
- [x] LOCK `->lock()`
- [x] UNLOCK `->unlock()`
- [x] PROPFIND `->propfind()`
- [x] VIEW `->view()`



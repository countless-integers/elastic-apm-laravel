# Elastic APM 

Elastic APM agent for v2 intake API. Compatible with Laravel 5.5+.

## Installation

Require this package with composer:

    composer require arkaitzgarro/elastic-apm-laravel

Add the ServiceProvider class to the providers array in `config/app.php`:

```php
'providers' => [
    // ... more providers
    \AG\ElasticApmLaravel\ServiceProvider::class,
],
```

And register the [global middleware](https://laravel.com/docs/5.5/middleware#global-middleware) that will be called on every request in `app/Http/Kernel.php`:

```php
protected $middleware = [
    // ... more middlewares
    \AG\ElasticApmLaravel\Middleware\RecordTransaction::class,
];
```

## Agent configuration

The following environment variables are supported in the default configuration:

| Variable          | Description |
|-------------------|-------------|
|APM_ACTIVE         | `true` or `false` defaults to `true`. If `false`, the agent will collect, but not send, transaction data. |
|APM_APPNAME        | Name of the app as it will appear in APM. |
|APM_APPVERSION     | Version of the app as it will appear in APM. |
|APM_SERVERURL      | URL to the APM intake service. |
|APM_SECRETTOKEN    | Secret token, if required. |
|APM_QUERYLOG       | `true` or `false` defaults to 'true'. Set to `false` to completely disable query logging, or to `auto` if you would like to use the threshold feature. |
|APM_THRESHOLD      | Query threshold in milliseconds, defaults to `200`. If a query takes longer then 200ms, we enable the query log. Make sure you set `APM_QUERYLOG=auto`. |
|APM_BACKTRACEDEPTH | Defaults to `25`. Depth of backtrace in query span. |
|APM_RENDERSOURCE   | Defaults to `true`. Include source code in query span. |

You may also publish the `elastic-apm-laravel.php` configuration file to change additional settings:

```bash
php artisan vendor:publish --tag=config
```

Once published, open the `config/elastic-apm-laravel.php` file and review the various settings.

## include
1. Redis
    How to install redis ?
    - composer require predis/predis
    - add .env REDIS_HOST=127.0.0.1
               REDIS_PASSWORD=null
               REDIS_PORT=6379
               REDIS_CLIENT=redis
               REDIS_CACHE_DB=0

               CACHE_DRIVER=redis
     - php artisan config:cache
     - php artisan cache:clear
     - add routes/web.php
                        use Illuminate\Support\Facades\Redis;
                        Route::get('/', function () {
                            $p = Redis::incr('p');
                            return $p;
                        });

                        Route::get("users_with_cache", "UserController@index");
                        Route::get("users_with_query", "UserController@getUser");

2. Package Debugger
  How to Install ?
  - composer require barryvdh/laravel-debugbar --dev
  - add config/app.php
    - Barryvdh\Debugbar\ServiceProvider::class,
    - 'Debugbar' => Barryvdh\Debugbar\Facade::class,
  - php artisan vendor:publish --provider="Barryvdh\Debugbar\ServiceProvider"

## UNIT TEST
## create lumen project
## composer install

## How to hit endpoint in unit test
 $parameters = ['param' => 'value'];
 $header = [ 'HTTP_Authorization' => 'value'];

 $this->get($url, $header);
 $this->post($url, $parameters, $header);
 $this->put($url, $parameters, $header);
 $this->delete($url, $parameters, $header);

## Expect Response Unit Test
$this->seeStatusCode(200);
$this->seeJson([ 'error' => false ]);
$this->seeJsonStructure([
    'error',
    'status',
    'message',
    'data'    => ['\*' =>
        [
            'product_name',
            'product_description',
            'created_at',
            'updated_at'
        ]
    ],

]);
# remove \ at \*

## uncomment bootstrap/app.php
 $app->withEloquent();
 $app->withFacades();

 create DB manually
 php artisan make:migration create_products_table
 php artisan migrate
 - create model
 - create faker/ factory
 - create seed
 php artisan db:seed

## install fractal, library untuk response JSON
 composer require league/fractal
 create routes, transformer, controller

## - running test
./vendor/bin/phpunit tests //test all our endpoints

#in older version
./vendor/bin/phpunit tests --filter=testShouldReturnAllProducts // test specified unit test

// Full repo: https://github.com/stephenjude/ProductAPI
// Source: https://medium.com/@stephenjudeso/testing-lumen-api-with-phpunit-tests-555835724b96
// phpunit doc: https://github.com/laravel/browser-kit-testing
## END UNIT TEST

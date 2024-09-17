## Credits

This code is taken from [laravel-g4t-swagger-auto-generate](https://github.com/hussein4alaa/laravel-g4t-swagger-auto-generate) by [hussein4alaa](https://github.com/hussein4alaa), he started the whole thing, I mixed up some non optimized code to generate response schemas based on Resources

# Swagger Laravel Autogenerate Package

The Swagger Laravel Autogenerate Package is a convenient tool that automatically generates Swagger documentation for your Laravel APIs based on your route definitions. It eliminates the need for manually documenting your API endpoints, saving you time and effort.

![Swagger Laravel Autogenerate Package](https://www.scottbrady91.com/img/logos/swagger-banner.png)

## Features

- Automatically generates Swagger documentation for Laravel APIs.
- Extracts route information, including URI, HTTP methods, route names, middleware, and more.
- Supports request validations and parameter definitions.
- Generates JSON output conforming to the Swagger/OpenAPI specification.
- Easy integration and configuration within Laravel projects.

## Installation

Install the Swagger Laravel Autogenerate Package via Composer:

```
janjacvd/laravel-semiauto-swagger
```

## Usage

#### Click here to watch a video on how to use this package

[![Explanatory video on how to use](https://img.youtube.com/vi/bI1BY9tAwOw/0.jpg)](https://www.youtube.com/watch?v=bI1BY9tAwOw)

1. After installing the package, publish the configuration file:

```
php artisan vendor:publish --provider "G4T\Swagger\SwaggerServiceProvider"
```

2. Configure the package by modifying the `config/swagger.php` file according to your needs. This file allows you to specify various settings for the Swagger documentation generation.

3. Access the generated Swagger documentation by visiting the `/swagger/documentation` route in your Laravel application. For example, `http://your-app-url/swagger/documentation`.

4. The issues history page is now included in config/swagger.php, and the default route is `http://your-app-url/swagger/issues`.

5. To add a description in a Swagger route using the ->description() method, you can follow the example you provided and include it in your Laravel application's routes.
   Here's how you can describe a route using the ->description() method in a Swagger route:
   ```php
    Route::get('user', [UserController::class, 'index'])->description('Get list of users with pagination.');
   ```
6. To add a summary in a Swagger route using the ->summary() method, you can follow the example you provided and include it in your Laravel application's routes.
   Here's how you can describe a route using the ->summary() method in a Swagger route:
   ```php
    Route::get('user', [UserController::class, 'index'])->summary('get users.');
   ```
7. To add a Section Description you can use this attribute `#[SwaggerSection('everything about your users')]` in your controller.
   Here's how you can use this attribute in your controller:

   ```php
    <?php

    namespace App\Http\Controllers;

    use G4T\Swagger\Attributes\SwaggerSection;

    #[SwaggerSection('everything about your users')]
    class UserController extends Controller
    {
       // ...
       // ...
       // ...
    }
   ```

## Usage for Responses

In controller, put a doc comment with @resource {absolute path to resource}

```php
 <?php
 namespace App\Http\Controllers;


 class UserController extends Controller
 {
      /**
       * @resource \App\Http\Resources\UserResource
      */
      public function login(LoginRequest $request)
      {
         //Auth logic return the user resource
      }
 }

 // UserResource

 namespace App\Http\Resources;

class UserResource extends JsonResource
{
 /**
  * @resourceModel
  * @attributes {
  *   "id": "number",
  *   "name": "string[]?",
  *   "address": "\App\Http\Resources\AddressResource[]"  <-----Nested resource, array of AddressResource, With absolute path
  * }
  */
 public function toArray(Request $request): array
 {
   //Method implementation
 }}


class AddressResource extends JsonResource
{
 /**
  * @resourceModel
  * @attributes {
  *   "place_id": "string",
  *   "formatted_address": "string?",
  * }
  */
 public function toArray(Request $request): array
 {}}
```

## Contributing

Contributions to the Swagger Laravel Autogenerate Package are always welcome! If you find any issues or have suggestions for improvements, please feel free to open an issue or submit a pull request.

## License

The Swagger Laravel Autogenerate Package is open-source software licensed under the [MIT license](LICENSE.md).

## Configure Auth Provider

1. Publish the config and set your auth provider model.
   ```bash
   php artisan vendor:publish --tag="filament-shield-config"
   ```
   ```php
   // config/filament-shield.php
   return [
       // ...
       'auth_provider_model' => 'App\\Models\\User',
       // ...
   ];
   ```
2. Add the `HasRoles` trait to your auth provider model:
   ```php
   use Spatie\Permission\Traits\HasRoles;

   class User extends Authenticatable
   {
       use HasRoles;
   }
   ```
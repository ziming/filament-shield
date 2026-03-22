## Policies

Shield automatically generates policies for your Resources' Models.

### Configuration
```php
'policies' => [
    'path' => app_path('Policies'),
    'merge' => true,
    'generate' => true,
    'methods' => [
        'viewAny', 'view', 'create', 'update', 'delete', 'deleteAny', 'restore',
        'forceDelete', 'forceDeleteAny', 'restoreAny', 'replicate', 'reorder',
    ],
    'single_parameter_methods' => [
        'viewAny',
        'create',
        'deleteAny',
        'forceDeleteAny',
        'restoreAny',
        'reorder',
    ],
],
```

### Methods
Each policy includes methods defined in the `policies.methods` config. You can customize this list to fit your application's needs. Since Filament Resources typically use a standard set of methods, the default configuration should suffice for most applications. If you have specific resources that require additional methods, you can easily add them to the list. 
However, it would be best to only include methods that are commonly used across your resources and define any resource-specific methods in the `resources.manage` config section. This approach keeps your policies clean and relevant to your application's requirements.

### Merge
When `policies.merge` is set to `true`, Shield will combine the global methods defined in `policies.methods` with any resource-specific methods you define in `resources.manage`. This ensures that each resource's policy includes both the standard methods and any additional ones you need for that particular resource.

### Single Parameter Methods
Some policy methods only require the user instance as a parameter (e.g., `viewAny`, `create`). These are defined in `policies.single_parameter_methods`. Shield will generate these methods accordingly in the policies. When you add new methods or resource-specific methods, ensure to update this list if they also only require the user instance. This helps maintain consistency and clarity in your policy definitions.

### Policy Enforcement
Laravel automatically resolves policies for models, but this is not always the case. For instance, if your models are not in the default `App\Models` namespace, are nested, or are from third-party plugins, you may need to manually register the policies. You can do this in a service provider's `boot()` method: 

```php
Gate::policy(Awcodes\Curator\Models\Media::class, App\Policies\MediaPolicy::class);
```

**Tip** For your in-app resources' models you can add the following method in the `boot()` method to automatically enforce policies, without the need to manually register each policy. This assumes your policies are in the `App\Policies` namespace and follow the naming convention of appending `Policy` to the model class name. Adjust the `str_replace` parameters if your structure differs:

```php
use Illuminate\Support\Facades\Gate;

Gate::guessPolicyNamesUsing(function (string $modelClass) {
    return str_replace('Models', 'Policies', $modelClass) . 'Policy';
});
```
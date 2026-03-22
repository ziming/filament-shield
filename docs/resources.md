## Resources

Shield derives resource permission keys from configured policy methods. Since Filament `Resources`' authorization is handled via policies, generated permissions align with policy methods.

### Configuration
```php
'resources' => [
    'subject' => 'model',
    'manage' => [
        \BezhanSalleh\FilamentShield\Resources\Roles\RoleResource::class => [
            'viewAny',
            'view',
            'create',
            'update',
            'delete',
        ],
    ],
    'exclude' => [
        //
    ],
],
```
### Subject
You can customize the subject used for resource permissions by setting the `subject` key in the `resources` configuration. The subject can be set to either `class` or `model` (default is `model`).

### Manage
You can define resource-specific policy methods in the `resources.manage` configuration. This allows you to tailor the permissions for individual resources (in-app or third-party) based on their unique requirements. When you specify methods here, Shield will generate permissions for these methods in addition to the global methods defined in `policies.methods`, provided that `policies.merge` is set to `true`. This ensures that each resource has a comprehensive set of permissions that reflect both standard and resource-specific actions.

### Exclude
You can exclude specific resources from permission generation by listing them in the `resources.exclude` configuration. This is useful for resources that should always be accessible or do not require permission checks. When a resource is excluded, Shield will skip generating permissions and policy for it.
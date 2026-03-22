## Custom Permissions

Most of the time you will have some ad-hoc permissions that don't fit into the `Resource`, `Page`, or `Widget` categories, or you might not want a policy method for them. You can define these under `custom_permissions` in the config:
```php
'custom_permissions' => [
    'Impersonate:User' => 'Impersonate User',
    'Export:Order' => 'Export Orders',
],
```
They appear in the `Role Resource`'s **Custom Permissions** tab when enabled.
To enable the tab, set `shield_resource.tabs.custom_permissions` to `true` in the config.
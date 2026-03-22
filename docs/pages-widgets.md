## Pages & Widgets

Both **pages** and **widgets** in Filament follow a similar permission model. By default, they require **view** permissions. You can customize their behavior in the configuration, including subject, prefix, exclusions, and enforcement traits.  

### Configuration  

**Pages**  
```php
'pages' => [
    'subject' => 'class',
    'prefix' => 'view',
    'exclude' => [
        \Filament\Pages\Dashboard::class,
    ],
],
```

**Widgets**  
```php
'widgets' => [
    'subject' => 'class',
    'prefix' => 'view',
    'exclude' => [
        \Filament\Widgets\AccountWidget::class,
        \Filament\Widgets\FilamentInfoWidget::class,
    ],
],
```

### Options  

| Option     | Description |
|------------|-------------|
| **Subject** | Determines how the permission subject is generated. <br>• `class` → Uses the class name (default). <br>• `model` → Uses the model name (if the entity has a `static getModel()` method). |
| **Prefix**  | Prepended to permission keys for distinction. <br>• Example for Pages: `Page:IconLibrary` <br>• Example for Widgets: `Widget:IncomeWidget`. |
| **Exclude** | Entities listed here will be skipped during permission generation. <br>Useful for always-accessible entities like dashboards, account widgets, or system info. |

### Permission Enforcement  

Use the appropriate **Shield trait** to automatically enforce permissions. 
When applied, these traits ensure:  
- Navigation or rendering is **hidden** if the user lacks permission.  
- Access to the page/widget is **restricted**.   

**Pages**  
```php
<?php

namespace App\Filament\Pages;

use ...;
use BezhanSalleh\FilamentShield\Traits\HasPageShield;

class MyPage extends Page
{
    use HasPageShield;
    ...
}
```

**Widgets**  
```php
<?php

namespace App\Filament\Widgets;

use ...;
use BezhanSalleh\FilamentShield\Traits\HasWidgetShield;

class IncomeWidget extends LineChartWidget
{
    use HasWidgetShield;
    ...
}
```
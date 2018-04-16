# Drupal - prepare development enviroment

## 1. Set theme debug to true

Find next statement and remove comment tag `#`

```php
$conf['theme_debug'] = TRUE;
```

## 2. Set error reporting level
 
Put at the top of `settings.php`

```php
error_reporting(E_ALL);
ini_set('display_errors', TRUE);
ini_set('display_startup_errors', TRUE);
```

## 3. Install `devel` plugin

Install `devel` plugin.
```
https://www.drupal.org/project/devel
```

Use devel to debug during development e.g.
```php
dvm($output_me);
```

Other commands are described on  http://ratatosk.net/drupal/tutorials/debugging-drupal.html
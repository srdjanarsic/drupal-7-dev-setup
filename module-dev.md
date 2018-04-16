# Module development

## 1. Module initialization

### 1.1 Chose module name

Module name is used in many places including hooks, so first step is to chose unique module name to avoid collision with other modules.

Examples of module names

```info
my_awesome_module
modern_grid_layout
web_form_layout_creator
```

### 1.2 Create module directory

In the example module we're going to use `demo_msg` module name.

Create `sites/all/modules/custom/demo_msg` directory. This will be `demo_msg` root module directory.

### 1.3 .info file

Create `demo_msg.info` file and put following content

```info
name = Demo Messages
description = This module show demo message in its own block
core = 7.x
package = My Message Package
```

### 1.4 .module file

This simple module file contains

* `hook_help` used to add help content and link in the Admin > Modules panel
* `hook_block_info` used to define blocks that are provided by module
* `hook_block_view` return a block content

```php
<?php

/**
 * @file
 * A block module that displays demo message.
 */

/**
 * Implements hook_help().
 *
 * Displays help and module information.
 *
 * @param path
 *   Which path of the site we're using to display help
 * @param arg
 *   Array that holds the current path as returned from arg() function
 */
function demo_msg_help($path, $arg)
{
    switch ($path) {
        case "admin/help#demo_msg":
            return t("Displays demo message");
            break;
    }
}

/**
 * Implements hook_block_info().
 */
function demo_msg_block_info()
{
    $blocks['demo_msg'] = array(
        'info' => t('Demo message'),
        'cache' => DRUPAL_CACHE_PER_ROLE,
    );
    return $blocks;
}

/**
 * Implements hook_block_view().
 *
 * Prepares the contents of the block.
 */
function demo_msg_block_view($delta = '') {
    switch ($delta) {
        case 'demo_msg':
            $block['subject'] = t('Demo message');
            if (user_access('any')) {
                $block['content'] = t('DEMO MESSAGE :)');
            }
        return $block;
    }
}
```
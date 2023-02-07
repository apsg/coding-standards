# Coding standards

## Usage

We can pass the path of the config file to Pint:
https://laravel.com/docs/9.x/pint#configuring-pint

so after this package is installed:

```bash
composer require apsg/coding-standards
```

one can tell Pint to use this config:

```php
./vendor/bin/pint --config vendor/apsg/coding-standards/pint.json
```

Alternatively - one can just copy the `pint.json` file and use it as a template in it's own projects.

## Rules descriptions:

### Namespace
```json
"single_blank_line_before_namespace": false,
"no_blank_lines_before_namespace": true,
"blank_line_after_opening_tag": false,
```
Those three (
[1](https://mlocati.github.io/php-cs-fixer-configurator/#version:3.14|fixer:single_blank_line_before_namespace), 
[2](https://mlocati.github.io/php-cs-fixer-configurator/#version:3.14|fixer:no_blank_lines_before_namespace),
[3](https://mlocati.github.io/php-cs-fixer-configurator/#version:3.14|fixer:blank_line_after_opening_tag)
) 
remove extra line before namespace. We don't look at this part of the file anyway, so this extra line is surplus in my opinion.  

Before
```php
<?php

namespace App\Domains\Admin\Controllers;
```

After:

```php
<?php
namespace App\Domains\Admin\Controllers;
```

### Trait imports

```json
"single_trait_insert_per_statement": true, 
```

Thanks to [single-line trait imports](https://mlocati.github.io/php-cs-fixer-configurator/#version:3.14|fixer:single_trait_insert_per_statement) we immediately see all of them - there is no import that hides in this right-hand side twilight zone.

Also this allows to simply comment out single import while coding/debugging.

Before: 

```php
class Material extends Model implements HasMedia
{
    use HasStates, HasFactory, HasSlug, InteractsWithMedia;
...
```

After:
```php
class Material extends Model implements HasMedia
{
    use HasStates;
    use HasFactory;
    use HasSlug;
    use InteractsWithMedia;
...
```

### Spaces
Rules:
- [negation](https://mlocati.github.io/php-cs-fixer-configurator/#version:3.14|fixer:not_operator_with_successor_space)
- [casts](https://mlocati.github.io/php-cs-fixer-configurator/#version:3.14|fixer:cast_spaces)
- [concats](https://mlocati.github.io/php-cs-fixer-configurator/#version:3.14|fixer:concat_space)

```json
"not_operator_with_successor_space": false,
"cast_spaces": {
    "space": "none"
},
"concat_space": {
    "spacing": "one"
},
```

Before:
```php
if(! $boolVariable) ...

$someString = $a.'-'.$b.'suffix';

$floatVariable = (float) '2.13'; 
```
After:

```php
if(!$boolVariable) ...

$someString = $a . '-' . $b . 'suffix';

$floatVariable = (float)'2.13'; 
```

### Alignment

[Following rule for me is a must](https://mlocati.github.io/php-cs-fixer-configurator/#version:3.14|fixer:binary_operator_spaces) - especially when building large arrays (like in transformers).
It also reduces visual clutter

```json
"binary_operator_spaces": {
    "operators": {
        "=>": "align"
    }
},
```

Before:

```php
return [
    'id' => $attachment->id,
    'name' => $attachment->name,
    'mime' => $attachment->mime,
    'url' => $attachment->downloadUrl(),
    'element' => $attachment->element,
    'copies' => $attachment->copies,
```

After: 

```php
return [
    'id'      => $attachment->id,
    'name'    => $attachment->name,
    'mime'    => $attachment->mime,
    'url'     => $attachment->downloadUrl(),
    'element' => $attachment->element,
    'copies'  => $attachment->copies,
```

Related to previous rule is [another one, that reduces visual clutter in php-docs](https://mlocati.github.io/php-cs-fixer-configurator/#version:3.14|fixer:phpdoc_align):

```json
"phpdoc_align": {
    "align": "vertical",
    "tags": [
        "method",
        "param",
        "property",
        "property-read",
        "property-write",
        "return",
        "throws",
        "type",
        "var"
    ]
},
```

Before:

```php
/**
 * @property int $id
 * @property int $user_id
 * @property string $title
 * @property string $slug
 * @property string|null $description
 * @property-read Collection|Attachment[] $attachments
 * @property-read User $owner
 */
class Material extends Model implements HasMedia
```

After:

```php
/**
 * @property      int                     $id
 * @property      int                     $user_id
 * @property      string                  $title
 * @property      string                  $slug
 * @property      string|null             $description
 * @property-read Collection|Attachment[] $attachments
 * @property-read User                    $owner
 */
class Material extends Model implements HasMedia
```

### Blank lines

[Rule](https://mlocati.github.io/php-cs-fixer-configurator/#version:3.14|fixer:no_extra_blank_lines)

```json
"no_extra_blank_lines": {
    "tokens": [
        "extra",
        "square_brace_block",
        "return"
    ]
}
```

This extends default behaviour (`extra`) and removes surplus blank lines:
- inside of curly braces `[]`
- after `return` statement

# Coding standards

## Rules descriptions:

### Namespace
```json
"single_blank_line_before_namespace": false,
"no_blank_lines_before_namespace": true,
"blank_line_after_opening_tag": false,
```
Those three remove extra line before namespace. We don't look at this part of the file anyway, so this extra line is surplus in my opinion.  

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

Thanks to single-line trait imports we immediately see all of them - there is no import that hides in this right-hand side twilight zone.

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

Following rule for me is a must - especially when building large arrays (like in transformers).
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

Related to previous rule is another one, that reduces visual clutter in php-docs:

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

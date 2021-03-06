# Php input filter

## Installation via Composer

```json
{
	"require": {
		"clsystems/php-filter": "~1.0"
	}
}
```

Alternatively, from the command line:

```sh
composer require clsystems/php-filter
```

## Usage

``` php
use CLSystems\Php\Filter;

// Syntax
Filter::clean($source, $type);

// Example
$source = '<h1>Hello World!</h1>';

// Return 'Hello World!'
$filtered = Filter::clean($source, 'string');

// Source array
$source = [
	'<h1>Hello World!</h1>',
	'<h1>Hello VietNam!</h1>',
];

// Return ['Hello World!', 'Hello VietNam!']
$filtered = Filter::clean($source, 'string');

// Multi-type
$source = '  <h1>Hello World!</h1>  ';

// Return 'Hello World!'
$filtered = Filter::clean($source, ['string', 'trim']);
```
## Filter types

* int
* uint (unsigned int)
* float
* ufloat (unsigned float)
* boolean
* alphaNum (alpha numeric string)
* base64
* string (no HTML tags)
* email
* url
* slug (url alias without slash)
* path (url alias with slash)
* unset (return NULL value)
* jsonEncode
* jsonDecode
* yesNo (return 'Y' or 'N')
* inputName (regex /[^a-zA-Z0-9_]/)
* unique (array unique)
* basicHtml

## Fallback default

``` php

if (function_exists($type))
{
	if (is_array($value))
	{
		$result = array_map($type, $value);
	}
	else
	{
		$result = $type($value);
	}
}
else
{
	$result = $value;
}

```
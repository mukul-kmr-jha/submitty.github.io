---
title: PHP
category: Developer
order: 6
---

__Minimum Version__: 7.2

For PHP, we use a foundation of [PSR-1](https://www.php-fig.org/psr/psr-1/) and
[PSR-12](https://www.php-fig.org/psr/psr-12/), with some slight modifications on
code structure and naming conventions. These customizations are shown below.

### Linting Code

We use a custom standard for the [phpcs](https://github.com/squizlabs/PHP_CodeSniffer) tool,
available at [Submitty/submitty-php-codesniffer](https://github.com/Submitty/submitty-php-codesniffer).
To set up the tool to use it, all you need to do is run `composer install` from within the `site/` directory,
which handles installing the dependencies and setting up the
[phpcs install paths](https://github.com/squizlabs/PHP_CodeSniffer/wiki/Configuration-Options#setting-the-installed-standard-paths).
To run `phpcs`, you can use the following command:

```bash
vendor/bin/phpcs --standard=tests/ruleset.xml [path/to/file/or/directory]
```

where if you leave off the path, it will analyze all files and directories for Submitty.
Additionally, you can apply the automatic fixer to your code by running:

```bash
vendor/bin/phpcbf --standard=tests/ruleset.xml [path/to/file/or/directory]
```

### Classes, Methods

* The opening brace for the class MUST go on the same line as the class name; the closing brace
  for the class MUST go on the next line after the body.
* The opening brace for a method MUST have one space between it and the closing parenthesis.
* The closing brace for a method MUST go on the next line following the body.

```php
class Test {
    public function foo() {
        // code
    }

    public function method(
        $long_arg_name_1,
        $another_long_name,
        $third_long_name
    ) {
        // code
    }
}
```

### Control Structures

* There MUST be one space after the control structure keyword
* There MUST NOT be a space after the opening parenthesis
* There MUST NOT be a space before the closing parenthesis
* There MUST be one space between the closing parenthesis and the opening brace
* The structure body MUST be indented once
* The closing brace MUST be on the next line after the body
* There MUST be one newline between closing brace and the next control structure keyword except for do-while

```php
if ($foo) {
    // code
}
elseif ($bar) {
    // code
}
else {
    // code
}
```

```php
do {
    // code
} while ($foo);
```

### Naming Conventions

* Classes should use `StudlyCaps`
* Functions should use `camelCase`
* Constants should be `UPPERCASE`
* Variables and properties should use `snake_case`

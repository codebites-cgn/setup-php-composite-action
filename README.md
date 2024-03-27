# GithubAction for PHP Composer Projects

## Description

This action efficiently sets up a PHP environment with specified version and extensions, caching both PHP extensions and Composer dependencies for faster workflow runs. It's basically a set of existing actions bundled together for an effecient workflow with PHP Composer projects.

On our projects this action reduced the execution time for a simple Symfony project from 3 minutes down to 1 minute.

I have not been able to test any matrix configurations or different OSes. So if you have problems or want to assist, don't hesitate to open an issue or PR!

## Usage

Available config parameters:

```YAML
php-version: 8.2 # Your desired PHP version. Default: 8.2
php-extensions: # A comma-seperated list of needed php extensions. Default: <empty>
caching: true # Enable or disable the caching. Default: true
composer-params: # Overwrite "composer install" parameters. Default: "-q --no-ansi --no-progress --prefer-dist --no-interaction"
```

Simple linting example using [ECS](https://github.com/easy-coding-standard/easy-coding-standard):

```YAML
name: code-check

on: [push]

jobs:
  ecs:
    steps:
      - uses: actions/checkout@v4
      - uses: codebites-cgn/setup-php-composite-action@v0.1
        with:
          php-version: "8.2"
          php-extensions: sqlsrv, pdo_sqlsrv
      - name: Run ECS Code Check
        run: vendor/bin/ecs check
```

## Credits

- [actions/cache](https://github.com/actions/cache)
- [shivammathur/setup-php](https://github.com/shivammathur/setup-php)
- [shivammathur/cache-extensions](https://github.com/shivammathur/cache-extensions)

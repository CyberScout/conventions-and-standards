# PHP Coding Conventions

PHP benefits from having a comprehensive, familiar, and well-respected set of
[standards put forth by the PHP-FIG](http://www.php-fig.org/psr/). This document
will simply state which PSRs must be followed, along any CyberScout-specific
adjustments or requirements.

## PHP Configuration

PHP version 7.x must be used for all new development.

PHP applications will be deployed under PHP-FPM, running within an Nginx
container/proxy.

## Coding Standard

Follow [PSR-1](http://www.php-fig.org/psr/psr-1/)

## Coding Style

Follow [PSR-2](http://www.php-fig.org/psr/psr-2/)

## Autoloading

PHP Applications should use [Laravel](https://laravel.com/) (or
[Symfony](https://symfony.com/) or a Symfony-based framework). These frameworks
implement or use a PSR-4-compatible autoloader. Beyond those,
[PSR-4](http://www.php-fig.org/psr/psr-4/) must be followed.

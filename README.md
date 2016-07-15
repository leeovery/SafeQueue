## SafeQueue

[![Latest Version on Packagist](https://img.shields.io/packagist/v/maxbrokman/safe-queue.svg?style=flat-square)](https://packagist.org/packages/maxbrokman/safe-queue)
[![Build Status](https://img.shields.io/travis/maxbrokman/SafeQueue.svg?maxAge=2592000?style=flat-square)](https://travis-ci.org/maxbrokman/SafeQueue)
[![Test Coverage](https://img.shields.io/coveralls/maxbrokman/SafeQueue.svg?maxAge=2592000?style=flat-square)](https://coveralls.io/github/maxbrokman/SafeQueue)
[![Software License](https://img.shields.io/badge/license-MIT-brightgreen.svg?style=flat-square)](LICENSE)

A Laravel Queue worker that's safe for use with Laravel Doctrine

#### When to use SafeQueue

- [x] You use Laravel 5
- [x] You use Laravel Doctrine
- [x] Devops say the CPU usage of `queue:listen` is unacceptable
- [x] You want to do `php artisan queue:work --daemon` without hitting cascading `EntityManager is closed` exceptions

#### How it Works

SafeQueue overrides a small piece of Laravel functionality to make the queue worker daemon safe for use with Doctrine.
It makes sure that the worker exits if the EntityManager is closed after an exception. For good measure it also clears the EM
before working each job.

#### Installation

Install using composer

```
composer require maxbrokman/safe-queue
```

Once you've got the codez add the following to your service providers in `app.php`

```
MaxBrokman\SafeQueue\DoctrineQueueProvider::class
```

#### Usage

```
php artisan doctrine:queue:work  connection --daemon -sleep=3 --tries=3 ...
```

All options are identical to Laravel's own `queue:work` method.

#### Contributing

PRs welcome.

```
vendor/bin/php-cs-fixer fix
vendor/bin/phpunit
```

#### Maintenance

I maintain this as part of my day job, please open any issues on Github

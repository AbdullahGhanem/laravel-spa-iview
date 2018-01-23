# Laravel-Vue SPA 


# Laravel 5 Boilerplate / Starter kit with [Iview](https://www.iviewui.com/) .

_Laravel Boilerplate_ provides a very flexible and extensible way of building your custom Laravel 5 applications with vue by Iview.

## Table of Contents

- [Features](#features)
- [Installation](#installation)
- [Development](#development)
- [Production](#production)

## Features

- Laravel 5.5 
- Vue + VueRouter + Vuex + Iview + VueI18n 
- Pages with custom layouts 
- Login, register and password reset
- Authentication with JWT
- Socialite integration

## Installation

1. Install Composer using detailed installation instructions [here](https://getcomposer.org/doc/00-intro.md#installation-linux-unix-osx)
2. Install Node.js using detailed installation instructions [here](https://nodejs.org/en/download/package-manager/)
3. Clone repository
```
$ git clone https://github.com/AbdullahGhanem/laravel-spa-iview.git
```
4. Change into the working directory
```
$ cd laravel-spa-iview
```
5. Copy `.env.example` to `.env` and modify according to your environment
```
$ cp .env.example .env
```
6. Install composer dependencies
```
$ composer install --prefer-dist
```
7. An application key can be generated with the command
```
$ php artisan key:generate
```
8. An application jwt key can be generated with the command
```
$ php artisan jwt:generate
```
9. Execute following commands to install other dependencies
```
$ npm install
$ npm run dev
```
If you get an error like a `PDOException` try editing your `.env` file and change `DB_HOST=127.0.0.1` to `DB_HOST=localhost` or `DB_HOST=mysql` (for *docker-compose* environment).


## Development

```bash
# build and watch
npm run watch

# serve with hot reloading
npm run hot
```

## Production

```bash
npm run production
```

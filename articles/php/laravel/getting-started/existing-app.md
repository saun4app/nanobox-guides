# Starting with an Existing Laravel App

Part of what makes Nanobox so useful is you don't have to have PHP installed on your local machine to run PHP apps. This guide walks through getting an existing Laravel app up and running with Nanobox.

*If you don't have an existing Laravel project, the [Laravel from Scratch](/php/laravel/getting-started/from-scratch) guide would be the best place to start.*

## Build a PHP Dev Environment
Nanobox will create an isolated virtual environment and mount your local codebase inside it. From within this environment you can run the app, artisan commands, or other tasks as you would normally.

### Add a boxfile.yml
The [boxfile.yml](https://docs.nanobox.io/boxfile/) tells Nanobox how to build and configure your environment. Create a `boxfile.yml` at the root of your project that contains the following:

```yaml
code.build:

  # tells nanobox to install php and associated runtimes
  engine: php
  config:

    # sets the php version
    # you can use a difference version if you prefer
    runtime: php-7.0

    # specifies the webserver document_root
    document_root: public

    # enables php extensions
    extensions:

      # required by laravel
      - pdo
      - mbstring
      - tokenizer
      - session

      # required by composer
      - phar
      - filter
      - json
      - hash
      - zip
      - dom

# creates a web component in sim and production environments
web.laravel:

  # commands to start PHP-FPM and Apache
  start:
    fpm: start-php
    apache: start-apache

  # pipes log output in your app's log-stream
  log_watch:
    apache[access]: /data/var/log/apache/access.log
    apache[error]: /data/var/log/apache/error.log
    php[error]: /data/var/log/php/php_error.log
    php[fpm]: /data/var/log/php/php_fpm.log
    laravel[error]: /app/storage/logs/laravel.log
```

#### runtime
Using PHP 7.0 is recommended, but other versions are available. The list of available PHP versions can be found in the [PHP Settings guide](/php/config/php-settings#runtime).

#### extensions
The [PHP engine](https://github.com/nanobox-io/nanobox-engine-php) takes a minimalist approach to including extensions in your PHP environment. Besides a few basic extensions, only extensions specified in your boxfile.yml are included in your PHP runtime.

If you need other extensions, just include them in your boxfile.yml. A list of available extensions can be found in the [PHP Extensions guide](/php/config/extensions).

### Build the Environment
With the your boxfile.yml in place, you're ready to create your dev environment. From the project directory run the following commands:

```bash
# build the code
nanobox build

# start the dev environment
nanobox dev start

# add a convenient way to access your app from the browser
nanobox dev dns add laravel.nanobox.dev
```

## Start PHP-FPM & Apache
Either `exit` out of your dev console or open a new terminal window and run the following to start PHP-FPM and Apache.

```bash
# run the start commands specified in your boxfile.yml
nanobox dev run
```

## View the App in Your Browser
With your app running, you can access it at `laravel.nanobox.dev:8080` in your browser of choice.

## Now What?
Now that you have Laravel running on Nanobox, what's next? Think about what else your application might need and hopefully the topics below will help you get started with the next steps of your development!

* Connecting to a database
* Adding components
* Preparing for production
* Launching your app
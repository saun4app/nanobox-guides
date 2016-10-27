# Existing Sinatra App
Part of what makes nanobox so useful is you don't even need ruby or sinatra installed on your local machine to use them.

This guide will help you get an existing Sinatra app up-and-running with nanobox.

## Create a Ruby Dev Environment
Nanobox creates an isolated virtual environment for your app, mounting the app's codebase inside.

From within this environment you can develop and run your app as you normally would with things like *bundle install* and *rake*.

**IMPORTANT**: Make sure to change directories into your project at this point, as all `nanobox dev` commands will be run from the root of your project.

#### Add a boxfile.yml
The <a href="https://docs.nanobox.io/boxfile/" target="\_blank">boxfile.yml</a> tells nanobox how to build and configure your app's environment. At the root of your project create a `boxfile.yml` telling nanobox you want to use the ruby <a href="https://docs.nanobox.io/engines/" target="\_blank">engine</a> (a set of scripts that configure an environment):

```yaml
code.build:
  engine: ruby
```

#### Start the Environment
You can then start the dev environment:

```bash
nanobox dev start
```

## Configure Sinatra
To allow connections from the host machine into the app's container modify the `myapp.rb` telling sinatra to listen on all available IP's at port 8080:

```ruby
set :bind, "0.0.0.0"
set :port, "8080"
```

Also, add a convenient way to access your app from a browser:

```bash
nanobox dev dns add sinatra.nanobox.dev
```

## Sinatra up-and-running
Console into the dev environment with `nanobox dev console` and run the app like you would normally:

```bash
ruby myapp.rb
```

Once the app has started you can visit it from your favorite browser at `sinatra.nanobox.dev`.

## Now what?
With an app running in a dev environment with nanobox, whats next? Think about what else your app might need and hopefully the topics below will help you get started with the next steps of your development!

* [Add a Database](/ruby/sinatra/add-a-database)
* [Javascript Runtime](/ruby/sinatra/javascript-runtime)
* [Local Environment Variables](/ruby/sinatra/local-evars)
* [Back to Sinatra overview](/ruby/sinatra)
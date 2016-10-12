# Beego from Scratch
Part of what makes nanobox so useful is you don't have to have golang or beego installed on your local machine.

This guide outlines the process used to create the <a href="https://github.com/nanobox-quickstarts/nanobox-beego" target="\_blank">nanobox-beego</a> quickstart app found under <a href="https://github.com/nanobox-quickstarts" target="\_blank">nanobox-quickstarts</a> on github.

## Build a Ruby Dev Environment
Nanobox will create an isolated virtual environment and mount your local codebase inside of. From within this environment you can run the app, a beego console, or even rake tasks as you would normally.

Decide where you want your project to live and create a folder there:

```bash
# create a project folder
mkdir nanobox-beego
```

#### Add a boxfile.yml
The boxfile.yml tells nanobox how to build and configure these environments. Create a `boxfile.yml` at the root of your project that contains the following:

```yaml
# tell nanobox to build a golang runtime. We also need to tell nanobox
# where our package is located.
code.build:
  engine: golang
  config:
    package: nanobox-beego
```

#### Build the Environment

```bash
# build a golang runtime
nanobox build

# deploy the golang runtime into the dev environment
nanobox dev deploy

# add a convenient way to access your app from a browser
nanobox dev dns add beego.nanobox.dev
```

## Create a Beego App

```bash
# console into the dev environment
nanobox dev console

# install beego so we can use it to generate our application
go get github.com/astaxie/beego
go get github.com/beego/bee

# generate the beego app
beego new .
```

#### Make App Accessible
We need to allow connections from the host into the app's container. To do this we need modify the `conf/app.conf` telling beego to listen on all available IP's at port 8080:

```conf
httpaddr = "0.0.0.0"
httpport = 8080
```

## Beego up-and-running
With the app configured the last thing to do is run it:

```bash
# run the app from the nanobox dev console
beego run
```

Visit the app from your favorite browser at: `beego.nanobox.dev:8080`

## Now what?
With an app running in a dev environment with nanobox, whats next? Think about what else your app might need and hopefully the topics below will help you get started with the next steps of your development!

* [Connect a database](connect-a-database.html)
* [Javascript Runtime](javascript-runtime.html)
* [Local Environment Variables](local-evars.html)
* [Back to beego overview](beego.html)
# Notes for the Docker and Docker Machine talk


## What is Docker


  Lightweight virtualisation. It shares a Linux kernel and creates an isolated
virtual FS.

  It doesn't support MacOSX at the moment. It supports Windows since last
release.

  Docker is a service available through a unix socket.  You can access
it's HTTPS interface via port 2376.  It tends to be REST (json) with a twist
when interfacing STDIN, STDERR, STDOUT (pull, attach.)

  That means you can install the official Go client CLI directly in MacOSX
and connect to *any* Docker service you have available (Virtualbox, local,
AWS, DO, Azure, whatever.)


## Differences with other systems

  If you use a linux host machine the main difference is that you don't need
a full virtualised machine to isolate runtimes and processes.

  If you use MacOSX then you have at least one VM that runs a linux kernel so
it can be shared between different Docker containers.

  Vagrant tends to favor one VM per project although there are ways to share
machine for multiple projects since it implements an interface to Docker.
That interface feels to limited for what you can do with Docker.


## Do I really need it?

  If you want a reproducible environment.

  If you want to share apps as bins (remember jar? the good part.)

  If you want to approach your architecture in a unix-ish composable way.

  If you want to make your favourite sysadmin happier. Instead of letting
them fight for app cohexistance (lib clashes, version clashes, learn multiple
language environments) you unify the management interface.


## What is Docker Machine

  A manager for docker-aware environments.  It allows to set up new machines
with docker configured ready to go. It offers a couple of providers like:

  - Virtualbox / Fusion
  - Amazon (AWS)
  - Digital Ocean
  - Google Computer Engine
  - Attach to your own docker-aware server.


## Differences with other systems

  It is an evolution of boot2docker.  Even though is a 0.2 it has been more
reliable than boot2docker as the later tends to hang from time to time; I
suspect it is a Virtualbox condition as Vagrant suffers the same *sometimes*.

  Although Vagrant 1.7 allows you some degree of control to remote hosts it
feels to primitive compared to what docker-machine already offers.


## Workflows

Before a bit of terminology:

* Image
* Container (instance)


### Alone

  Easy one.  Start using Docker by just pulling a public image from
the Docker Registry.

  What to do?

* Play with a new language, with a new version of a language.
* Run scripts with dependencies in isolation.
* Your own image. Building your own image helps speeding up processes.
* Database taste. Composition. Don't expose ports in production.


### Party

* (`build`) Everyone build its own image via Dockerfile.
* (`push`, `pull`) Share images via the Docker Registry.
* Github hooks.
* (`save`, `export`, `import`, `load`) Old friend tarball.


## Pain points

* ENV vars for linked containers.
* Private Docker Registry.
* Slow official docker registry.
* Managing multiple containers all together (fig > docker-compose, make, mustard.)
* When you automate a build, you're no longer able to push images by hand
* Container autodiscovery
* Dockerfile back to hellscript

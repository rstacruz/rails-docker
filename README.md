# Rails on Docker

Here's how to get Rails working on Docker on OSX.

:construction: This guide is tested on the following setup. Your mileage may vary with other versions.

* Docker 1.6.2
* docker-machine 0.2.0
* docker-compose 1.3.0.dev
* Rails 4.2.2
* VirtualBox 4.3.8
* OSX 10.10.2

## Files

- [Dockerfile](Dockerfile)
- [.dockerignore](.dockerignore)
- [config/database.yml](config/database.yml)
- [docker-compose.yml](docker-compose.yml)

## Set up

* Be sure to set up your toolchain first (see [OSX Toolchain Setup](_docs/osx.md)).

* Copy the files (above) to your Rails app. Edit them as you need (start with docker-compose.yml). Be sure to use the supplied database.yml, or modify your database.yml to accomodate it.

* Build the Docker image.

  ```
  docker-compose build
  ```

* Set up your app's database.

  ```
  docker-compose run web rake db:setup
  ```

* Bring them all up.

  ```
  docker-compose up
  ```

* Get your VM IP, and load it in your browser.

  ```
  $ docker-machine ip
  192.168.99.100

  $ open http://192.168.99.100:3000
  ```

## Life cycle

* Use `docker-compose run` to run stuff.

  ```
  docker-compose run web rails console
  docker-compose run web bash
  docker-compose run web rake routes
  docker-compose run web rspec
  ```

* If you added gems, simply use `bundle` inside the container.

  ```
  docker-compose run web bundle
  ```

## When you're done

```
docker-compose stop    # turn off docker containers
docker-machine stop    # turn off docker VM
```

## How it works

You get a development environment in Docker for your Rails app.

 * [docker-compose] is used to manage multiple Docker containers in development. Don't use this in production.

 * Your local directory is synced to the Docker container. That means you can edit files locally as if the server is running on your computer too.

 * database.yml is shared between your your local and in the Docker container.

## Troubleshooting

> Couldn't connect to Docker daemon - you might need to run `boot2docker up`.

You'll need to turn on `docker-machine`. If it's already started, you'll also need to enable it in your shell. (You're not using boot2docker, so don't follow what it says.)

```
docker-machine start
docker-machine env | source
```

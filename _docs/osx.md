# OSX setup

Requisites
----------

 * [docker] client
 * [docker-machine] to manage a VM instance with Docker server running on it
 * [VirtualBox] to run docker-machine
 * [docker-compose] to manage docker multiple images/containers

Toolchain setup
---------------

* Get [VirtualBox].

  ```
  brew install caskroom/cask/brew-cask
  brew cask instal virtualbox
  ```

* Get [docker-compose] 1.3.0 or above. At time of writing, this is a development-only package.

  ```
  brew install rstacruz/docker-compose/docker-compose --HEAD
  ```

* Get [docker] and [docker-machine].

  ```
  brew install docker
  ```

* Set up [docker-machine]. This creates a box called `dev` using the `virtualbox` driver.

  ```
  docker-machine create -d virtualbox dev
  ```

* Set up your shell. This will make `docker` commands connect to the `dev` machine automatically. Consider putting this in your shell's profile.

  ```sh
  docker-machine env dev | source       # bash/zsh
  eval (docker-machine env dev)         # fish
  ```

That's it. Start using docker!

[docker-compose]: http://docs.docker.com/compose/
[docker-machine]: http://docs.docker.com/machine/
[docker]: https://www.docker.com/
[VirtualBox]: http://virtualbox.org/

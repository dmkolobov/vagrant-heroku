This is a [veewee](https://github.com/jedi4ever/veewee) template for building a
[Vagrant](http://vagrantup.com/) box that closely mirrors the heroku Cedar stack. You can build it
yourself by following the directions below or install a prebuilt version from [here](http://dl.dropbox.com/u/1906634/heroku.box).

## Easy Install

I do not plan to maintain a publically available version of this box. Therefore, there is no easy install and you should proceed to the next step.

## Building From Scratch

First, clone the repo and install gems with bundler.

```bash
$ git clone https://github.com/ejholmes/vagrant-heroku.git
$ cd vagrant-heroku
$ bundle install
```

Next, build the box with veewee. Go grab a cup of coffee because this is gonna
take a while.

```bash
$ bundle exec veewee vbox build heroku
```

There is also a 2x dyno box available, just substitute every instance of `heroku` with `heroku-2x`.

And finally, install the box for use with Vagrant.

```bash
$ bundle exec veewee vbox export heroku
$ vagrant box add heroku heroku.box
```

Now all you have to do is setup vagrant in your project.

```bash
$ vagrant init heroku
$ vagrant up
$ vagrant ssh
```

If you wish to skip these steps in the future, upload `heroku.box` to 
the cloud manager of your choice, and add the following to your `Vagrantfile`.

```ruby
Vagrant::Config.run do |config|
  config.vm.box = "heroku"
  config.vm.box_url = "<YOUR BOX URL>"
end
```

## Included Packages

The packages that are included are carefully selected to closely match those on
the Celadon Cedar stack.

* Ubuntu 10.04 64bit
* Ruby 2.0.0-p247 MRI
* RubyGems 2.0.3
* Python with pip, virtualenv, and virtualenvwrapper
* PostgreSQL 9.2.4
* NodeJS latest
* NPM latest
* Foreman https://github.com/ddollar/foreman

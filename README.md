#Boxel
Boxel is a near real-time pixelator and Minecraft codec.

##What does it do?
Boxel pixelates and reduces the color pallete of images, websites and video at up to 24fps.

You can use it to make funky pixelated artwork from existing assets to display wherever you like.
By default, Boxel creates a stream of PNG images along with JSON messages that describe the image.

Boxel was built to act as a codec for Minecraft. You can use the data it creates to build boxelized images,
websites and video from blocks on a Minecraft server.

We've also created a [client library](https://github.com/verizoncraft/Boxel-client) that makes it easy to connect Bukkit compatible Minecraft plugins to a Boxel server.

##Demo app
The best place to start with Boxel is probably the [demo app](https://github.com/VerizonCraft/Boxel-demo).

It provides docker containers for Boxel and each of its dependencies (PhantomJS,
Redis, Crossbar), as well as an example web front-end that will have a Boxel
service running in just a few commands.

##Dependencies
Boxel has three major dependencies:

* [Crossbar](http://crossbar.io/): Used for device discovery, communication
  between the web application and the Minecraft server, and to serve the web
  application we built above.
* [Redis](https://github.com/antirez/redis): Used to push data into a PUB/SUB
  channel that Minecraft servers can subscribe to.
* [PhantomJS](https://github.com/ariya/phantomjs): Used for headless browsing to
  capture images of websites.

####PhantomJS
#####OS X
Installing PhantomJS on OSX with Homebrew is simple:
```bash
$ brew install phantomjs
```

#####Linux
Installing on Linux is unfortunately not as simple. Please refer to the
[official PhantomJS installation guidelines](http://phantomjs.org/build.html) for instructions.

#####Running PhantomJS
Once you've got PhantomJS installed, you will need to start it before running
Boxel:

```bash
$ /usr/local/bin/phantomjs --webdriver=8910
```

If you plan to use a Docker image to install and run your Phantom instance, we
highly recommend using this Docker image: [wernight/phantomjs](https://hub.docker.com/r/wernight/phantomjs/).

####Redis
Next, Boxel requires [Redis](http://redis.io) to send video data over PUB/SUB channels.
Installation will vary depending on your system:

#####OS X
On OS X, redis can be installed with Homebrew:
```bash
$ brew install redis
```

#####Ubuntu / Debian
On a Debian-based system, redis can be installed with apt-get:
```bash
$ sudo apt-get install redis-server
```

##### RHEL / Fedora / CentOS
On RHEL-based systems, the easiest way to get redis installed is to download the
source tarball and perform a make-install:
```bash
$ wget http://download.redis.io/releases/redis-2.8.3.tar.gz
$ tar xzvf redis-2.8.3.tar.gz
$ cd redis-2.8.3
$ make && sudo make install
```

####Crossbar
Finally, Boxel requires a WAMP router for service discovery. We use
[crossbar](http://crossbar.io), which can be installed via pip:

##### OS X / Debian / RHEL
```bash
pip install crossbar
```

##Installing Boxel
After you've installed the dependencies listed above, install Boxel like any other Python
package, with `pip`. 
```bash
# using pip
pip install -e git+https://github.com/VerizonCraft/Boxel.git#egg=boxel
```

##Run it!
Once the above dependencies are installed and running, you should be able to start the Boxel service like so:
```bash
# substitute the correct host/port for your redis server and crossbar router
boxel -W 50 -C palettes/5bit.yml video -R redis://localhost:6379/0 -U ws://localhost:8080/ws
```

##Usage
See [Boxel-client](https://github.com/VerizonCraft/Boxel-client) for code
examples of video and website rendering in Minecraft.

If you want to check out Boxel in action, hop over to
[verizoncraft.github.io](https://verizoncraft.github.io) to see SethBling and
CaptainSparklez build some phones then use them to make video calls in Minecraft.

##Contribute
If you'd like to contribute, check out the [contributing guidelines](https://github.com/VerizonCraft/Boxel/blob/master/CONTRIBUTING.md)

##License
This repository and its code are made available under a BSD 3-Clause license, which can be found [here](https://github.com/VerizonCraft/Boxel/blob/master/LICENSE).


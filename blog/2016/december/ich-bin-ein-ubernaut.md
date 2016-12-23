<!--
Title: Ich bin ein Ubernaut
Author: Jacob Moen
Date: 2016/12/23 11:53
Datetime: 2016-12-23
Description: I have moved my websites from Dreamhost to Uberspace 
View: post
Disqusid: /2016/december/ich-bin-ein-ubernaut
ogimage: ubernaut/uberspace.png
thumb: ubernaut/uberspace_custom.png
Keywords: uberspace, ubernaut, hosting, dreamhost
Tags: hosting, uberspace
blogpost: true
published: true
-->
(inimage:Ich bin ein Ubernaut source:ubernaut/uberspace.png)

I have been a Dreamhost customer for years, on shared hosting, and have been fairly satisfied.

A year ago, I decided to move from shared hosting to a Dreamhost VPS, because I wanted to do more, like running Node.js and configure my server.

The price went from $10 to $15 a month, which I think was quite expensive, considering that Dreamhost VPS does not grant root access, and all in all does not give you a whole lot more than regular shared hosting..

(clearfix:)

Eventually, I had to close my Dreamhost account because of financial issues, and I have been on the lookout for an alternative that I can afford, and that gives me the features I need.

Not surprisingly, I was unable to find a suitable alternative.. 


Until I stumbled upon [Uberspace](https://uberspace.de/)!

## Uberspace ##

*"Uberspace.de is a platform of technicians for technicians and all who want to be. We make hosting for command line enthusiasts, data protectionists, control freaks, Unix friends, DIY's .."*

### Features ###

#### Pay what you want ####

Uberspace is a pay-what-you-want hosting provider.

You simply set the desired monthly fee on your account page.

Currently, the minimum fee is 1 euro, but the recommended fee is between 5 and 10 euros a month.

The rationale behind the 'pay what you want' policy is that everyone ought to have a voice on the net, so if find yourself low on cash, Uberspace is still your host.

You can't use credit card, Paypal or other 'services' to pay for your hosting, only direct money transfer or Bitcoin transaction - for political reasons.

They are concerned about privacy and ethics. And I like that a lot.

The first month is free, so there is nothing to lose. :)

#### Programming languages ####

Perl, Python, PHP, Ruby, node.js, Erlang, Lua, Go, GCC, git, Subversion, Mercurial, ...

You can have a custom `php.ini`, install extensions, PECL, ..

It is possible to install/compile other languages, like Rust. The list above is just what Uberspace provides 'out of the box'.

#### Databases ####

MySQL, PostgreSQL, SQLite, CouchDB, MongoDB, Redis, ...

It was easy to connect to mysql via a ssh tunnel from MySQL Workbench. There is also webbased interfaces, like Adminer and PHPMyAdmin, if you want that.

#### Goodies ####

You add, delete, stop and start daemons (services) easily. They can run scripts, applications, whatever you like.

You can also install software via LinuxBrew, which is awesome!

Uberspace has support for Let's Encrypt - just a matter of running an Uberspace script or two.

#### Lose the GUI ####

No cPanel, no GUI, all command-line.

There are lots of 'uberspace' scripts that can help you configure your Uberspace 'box' the way you want it.

For a command-line geek like me, that is perfect!

#### Have fun ####
As long as you act responsibly, you are actively encouraged to try things out.

They have a very geeky wiki with lots of cool stuff, and they provide lots of freedom.

### Caveats ###
#### German ####
Yes, there is a catch: everything is in German!

I am lucky to be able to understand German so-and-so, and I use Google Translate sometimes, especially when reading the Uberspace wiki.

Luckily, they do English when you contact them for support, and the scripts in the shell also 'speaks English'.

I am working on my German, and am currently at 22% fluency at [DuoLingo](https://www.duolingo.com/jacmoe) :)

#### DNS hosting ####
They do not offer DNS hosting, so if you have your own domain name, you need to find a DNS host first.

### My experience ###
After signing up, all I had to do to log into my shell account was to provide a public ssh key, and I was good to go.

I read up on domains on the [Uberspace wiki](https://wiki.uberspace.de/domain:verwalten), and I ran the following command to add my `jacmoe.dk` domain:
~~~bash
uberspace-add-domain -d jacmoe.dk -w
~~~
I also added `www.jacmoe.dk`, just in case. 
Then, I created a `jacmoe` directory in `/var/virtual/jacmoe`, deployed my site, and created a symlink for the site:
~~~bash
ln -s jacmoe/current/web jacmoe.dk
~~~
After adding the ip adresses to my DNS configuration - at my DNS hosting provider - the site was live.

Adding subdomains was just as easy.

After a day, my main site, and 5 subdomains, were all up and running.

I changed the PHP version to 7.0, and that was just a matter of changing a configuration file in my home directory and rstart PHP.

I also added a service to run my Gogs (Go Git Service) instance - Uberspace is awesome!

Adding Let's Encrypt certificates was also very easy, so all my sites are now secure.

I really am looking forward to experiment with Rust, Erlang, etc. Perhaps even using a C++ web framework! Why not? :)

## Conclusion ##
I highly recommend that you check out [Uberspace](https://uberspace.de/) if you want a web host with a lot of features for an unbeatable price.

I like their ethical standpoints (privacy, transparency, security) and their pay-what-you-want policy, and overall serious attitude, while at the same time they encourage you to have fun and not fear the command-line.

So, yes: ich bin ein Ubernaut!

And I probably will be hosted on asteroids for a long time to come. :)

(clearfix:)

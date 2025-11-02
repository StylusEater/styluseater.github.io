---
layout: post
title:  "Quick PostgreSQL Configuration for Developers"
date:   2020-01-18 15:04:19 -0500
categories: postgres development software
---
Are you a software developer? Do you need to setup a local PostgreSQL server for development on your machine and you’ve struggled with it in the past? Then don’t waste your time. If you follow the directions laid out in the post then you should be up and running quickly.

## Debian GNU/Linux

If you work with Debian GNU/Linux, the best way to install the latest version of PostgreSQL is to use the packages provided by the PostgreSQL project. The latest packages may be found here. Once on the page, you’ll want to choose which version of Debian GNU/Linux you’re using from the drop-down list then add the link to your APT sources list, retrieve and install the key provided by the project to sign packages, then use APT to install the version of PostgreSQL you wish to install. Below this paragraph you will find a sequence of commands that correspond to what I just wrote and an additional set of commands to setup and configure a user, a database and to grant access to your new user for the purpose of developing your application. These rules were taken from a popular response I posted on StackOverflow a while back which you may find here.

as root...

{% highlight bash %}
root@www0:~# echo "deb http://apt.postgresql.org/pub/repos/apt/ wheezy-pgdg main" >> /etc/apt/sources.list

root@www0:~# wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | apt-key add -

root@www0:~# apt-get update

root@www0:~# apt-get install postgresql-9.4        

root@www0:~# su - postgres 

postgres@www0:~$ createuser --interactive -P someuser
Enter password for new role:
Enter it again:
Shall the new role be a superuser? (y/n) n
Shall the new role be allowed to create databases? (y/n) y
Shall the new role be allowed to create more new roles? (y/n) n

postgres@www0:~$ createdb -O someuser database

postgres@www0:~$ psql -U someuser -h 127.0.0.1 database
{% endhighlight %}

## Red Hat

The Red Hat family of distributions includes Red Hat Enterprise Linux, CentOS, Fedora, Scientific Linux, Oracle Linux and others. PostgreSQL is available on these platforms by default. However, each version of the platform normally “snapshots” a specific version of PostgreSQL that is then supported throughout the lifetime of this platform. Since this can often mean a different version than preferred, the PostgreSQL project provides a repository of packages of all supported versions for the most common distributions.

If you work with Red Hat (or GNU/Linux distributions based on Red Hat like CentOS, Oracle Enterprise and etc.) then you may find the latest version of PostgreSQL supported by the distribution using yum. [Here is a link][Here-is-a-link] to the latest instructions given by the PostgreSQL project.

## Ubuntu

Since Ubuntu is based on Debian GNU/Linux, the installation process is very similar to Debian GNU/Linux. You may find the instructions I provided above for Debian GNU/Linux very helpful and the packages on the PostgreSQL project site for Ubuntu equally useful.

## SuSE and Others

PostgreSQL is available in all SuSE versions by default. However, SuSE Linux “snapshots” a specific version of PostgreSQL that is then supported throughout the lifetime of that SuSE version.

I’ve limited experience with installing PostgreSQL on SuSE Linux or other distributions but I suspect the installation process on the PostgreSQL project is sufficient. You may find the one for SuSE here and the one for other distributions [here][here].

If you’ve questions about any of this I encourage you to use the contact form on my website here.

Cheers! and Happy Hacking!

-Adam

P.S. Stay tuned for my next post on building a two node PostgreSQL cluster on AWS EC2!

[Here-is-a-link]: https://www.postgresql.org/download/linux/redhat/ 
[here]: https://www.postgresql.org/download/

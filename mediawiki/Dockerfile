FROM ubuntu:xenial-20180228
MAINTAINER amrita.ojha5@gmail.com

## Tar the configs in the repo dir
## Untar and Copy config tars from repo for service start via supervisord

RUN  set -x \
 &&  mkdir -p /var/www/mediawiki   \
	      /opt/commons/scripts \
	      /var/log/supervisor  \			
## /opt/common/scripts for housing the supervisor start scripts. Include other log directories for http and php.
## Add the Copy statements for untarring the configs

 &&  apt-get update \
 &&  apt-get install -o Dpkg::Options::="--force-confold" --force-yes -y apt-transport-https wget unzip curl gnupg 2 httpd php php-mysql php-gd php-xml

RUN  wget https://releases.wikimedia.org/mediawiki/1.31/mediawiki-1.31.3.tar.gz \
 &&    gpg --verify mediawiki-1.33.0.tar.gz.sig mediawiki-1.33.0.tar.gz  \
 &&    cd /var/www/mediawiki  \
 &&    unzip tar -zxf /home/username/mediawiki-1.33.0.tar.gz \
 &&    ln -s mediawiki-1.33.0/ mediawiki  \
 &&    chown -R apache:apache /var/www/mediawiki-1.33.0 
 &&    rm -rf /var/lib/apt/lists/* \
 &&    apt-get autoclean


EXPOSE 80
#other ports if required

CMD ["/usr/bin/supervisord"]
## Once supervisord starts, it will automatically pickup the rest of the services and start them based on the include parameter for configs
